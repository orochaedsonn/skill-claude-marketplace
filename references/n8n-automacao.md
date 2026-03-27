# Automação n8n + APIs de Marketplace — R9 Marketplace

## Contexto técnico da R9

- n8n auto-hospedado em VPS via Coolify
- Stack atual: Evolution API (WhatsApp), OpenAI GPT-4o-mini, Google Sheets
- Claude API disponível via Anthropic Console
- Infraestrutura: mesma VPS para todos os serviços internos

---

## APIs disponíveis por plataforma

### Mercado Livre — API oficial
- **Documentação**: https://developers.mercadolibre.com.br
- **Autenticação**: OAuth 2.0 (access_token com expiração de 6h + refresh_token)
- **Rate limit**: 200 req/min por usuário

**Endpoints mais úteis:**
```
GET  /items/{item_id}                    → detalhes do anúncio
PUT  /items/{item_id}                    → atualizar anúncio
GET  /orders/search?seller={id}          → listar pedidos
GET  /questions/search?item_id={id}      → perguntas do anúncio
POST /answers                            → responder pergunta
GET  /users/{user_id}/items/search       → listar anúncios do vendedor
GET  /sites/MLB/search?q={query}         → busca pública de produtos
```

### Shopee — API de Parceiros
- **Documentação**: https://open.shopee.com
- **Autenticação**: HMAC-SHA256 signature + partner_id + shop_id
- **Nota**: acesso requer aprovação como parceiro

**Endpoints úteis:**
```
GET  /api/v2/item/get_item_list          → listar produtos
POST /api/v2/item/update_price           → atualizar preço
GET  /api/v2/order/get_order_list        → listar pedidos
POST /api/v2/message/send_message        → enviar mensagem ao comprador
```

---

## Workflows n8n prontos para marketplace

### Workflow 1: Monitor de perguntas ML → resposta automática via IA

**Função**: Monitora novas perguntas no ML e gera resposta automática com GPT-4o-mini, aguardando aprovação humana antes de enviar.

```
[Cron: a cada 15min]
     ↓
[HTTP Request: GET /questions/search?seller_id=X&status=UNANSWERED]
     ↓
[IF: total_results > 0]
     ↓ SIM
[Loop: para cada pergunta]
     ↓
[HTTP Request: GET /items/{item_id}] → busca dados do produto
     ↓
[OpenAI / Claude: gera resposta baseada nos dados do produto]
     ↓
[Google Sheets: salva pergunta + resposta sugerida + status=PENDENTE]
     ↓
[WhatsApp via Evolution API: notifica Edson com a pergunta + resposta sugerida]
     ↓
[Wait for Webhook: aguarda aprovação]
     ↓ APROVADO
[HTTP Request: POST /answers com a resposta]
     ↓
[Google Sheets: atualiza status=ENVIADO]
```

### Workflow 2: Monitor de preço de concorrentes (ML)

**Função**: Monitora o preço dos top 5 concorrentes para um produto e alerta quando o gap de preço ultrapassar um threshold.

```
[Cron: diário às 8h]
     ↓
[Google Sheets: busca lista de produtos monitorados + preço atual]
     ↓
[Loop: para cada produto]
     ↓
[HTTP Request: GET /sites/MLB/search?q={keyword}&limit=5]
     ↓
[Code Node: extrai preços dos top 5, calcula menor preço concorrente]
     ↓
[IF: menor_preço_concorrente < nosso_preço × 0.95]
     ↓ SIM (concorrente mais de 5% mais barato)
[WhatsApp: alerta com produto, nosso preço, menor preço concorrente, gap %]
     ↓
[Google Sheets: registra histórico de preços]
```

### Workflow 3: Relatório semanal automático

**Função**: Coleta dados de vendas da semana e gera flash report formatado.

```
[Cron: toda segunda-feira às 9h]
     ↓
[HTTP Request: GET /orders/search?date_from={semana_anterior}]
     ↓
[Code Node: agrupa por produto, calcula faturamento, ticket médio, top produtos]
     ↓
[Claude API: formata os dados como flash report profissional]
     ↓
[Google Sheets: salva relatório]
     ↓
[WhatsApp / Email: envia relatório ao cliente]
```

### Workflow 4: Atendimento pós-venda automático

**Função**: Após confirmação de entrega, envia mensagem solicitando avaliação.

```
[Cron: a cada 4h]
     ↓
[HTTP Request: GET /orders → filtra status=delivered nas últimas 24h]
     ↓
[Google Sheets: verifica se já foi enviada mensagem para este pedido]
     ↓
[IF: não enviado ainda]
     ↓
[HTTP Request: GET dados do comprador]
     ↓
[WhatsApp ou mensagem na plataforma: envia template de solicitação de review]
     ↓
[Google Sheets: registra envio + data]
```

---

## Autenticação ML no n8n — passo a passo

### Setup inicial
1. Criar app em https://developers.mercadolibre.com.br
2. Configurar redirect URI para: `https://seu-n8n.dominio.com/webhook/ml-callback`
3. Salvar `client_id` e `client_secret`

### Node de renovação de token (obrigatório — token expira em 6h)
```javascript
// Code Node — renovar access_token ML
const clientId = $env.ML_CLIENT_ID;
const clientSecret = $env.ML_CLIENT_SECRET;
const refreshToken = $getWorkflowStaticData('global').ml_refresh_token;

const response = await $http.post('https://api.mercadolibre.com/oauth/token', {
  grant_type: 'refresh_token',
  client_id: clientId,
  client_secret: clientSecret,
  refresh_token: refreshToken
});

// Salvar novos tokens
const staticData = $getWorkflowStaticData('global');
staticData.ml_access_token = response.data.access_token;
staticData.ml_refresh_token = response.data.refresh_token;

return [{ json: { access_token: response.data.access_token } }];
```

---

## Estrutura de credenciais recomendada no n8n

| Variável | Onde usar |
|---|---|
| `ML_CLIENT_ID` | Auth ML |
| `ML_CLIENT_SECRET` | Auth ML |
| `SHOPEE_PARTNER_ID` | Auth Shopee |
| `SHOPEE_PARTNER_KEY` | Auth Shopee |
| `OPENAI_API_KEY` | Nó OpenAI |
| `ANTHROPIC_API_KEY` | Nó Claude (HTTP Request) |

> Todas as chaves via variáveis de ambiente no Coolify — nunca hardcoded no workflow.

---

## Prompt base para IA responder perguntas de produto (ML)

```
Você é um assistente de vendas especializado em [nicho do produto].
Responda a pergunta do cliente de forma cordial, completa e persuasiva.
Use o tom: profissional e amigável, focado em converter a venda.

DADOS DO PRODUTO:
Título: {titulo_anuncio}
Descrição: {descricao_anuncio}
Preço: R$ {preco}
Frete grátis: {sim/não}

PERGUNTA DO CLIENTE:
{pergunta}

REGRAS:
- Responda apenas com base nos dados do produto
- Se a informação não estiver disponível, diga que verificará e retornará
- Nunca mencione concorrentes
- Máximo de 3 parágrafos curtos
- Termine sempre com convite para compra ou próxima pergunta
```
