# Bling + Google Sheets — Integração via API v3

## O que é e para que serve

Integração direta entre o Bling ERP e o Google Sheets via API v3 + Google Apps Script. Permite buscar produtos do Bling por SKU e preencher automaticamente a planilha de precificação sem copiar e colar nada.

---

## Pré-requisitos

- Conta no Bling com acesso de administrador
- Google Sheets com a planilha de precificação R9
- Acesso ao Google Apps Script (Extensões → Apps Script)

---

## Passo 1 — Criar aplicativo no Bling (fazer uma vez)

```
Bling → Central de Extensões → Área do Integrador → Criar aplicativo
```

Configurações:
- **Tipo**: API
- **Visibilidade**: Privado (só para sua conta)
- **Categoria**: Precificação
- **Descrição curta**: qualquer texto
- **Link de redirecionamento**: URL do Web App do Apps Script (ver Passo 3)
- **Escopos**: Produtos → Visualizar (só o pai, não os sub-itens)
- **Contato**: nome, email e celular

Após salvar → aba "Informações do app" → copiar **Client ID** e **Client Secret**

⚠️ **IMPORTANTE**: Client ID e Client Secret são credenciais sensíveis — guardar localmente, nunca compartilhar em chats ou repositórios públicos.

---

## Passo 2 — Configurar o Google Apps Script

No Google Sheets da planilha:
```
Extensões → Apps Script
```

Cole o código completo (arquivo BlingIntegracao_v6.gs) e preencha as 3 constantes:

```javascript
const CLIENT_ID     = 'seu_client_id';
const CLIENT_SECRET = 'seu_client_secret';
const REDIRECT_URI  = 'URL_do_web_app'; // preencher após implantar
```

Salve com `Ctrl+S`.

---

## Passo 3 — Implantar o Web App

```
Implantar → Nova implantação → App da Web
```

Configurações:
- **Descrição**: R9 Bling v1
- **Executar como**: Eu mesmo
- **Quem pode acessar**: Somente eu

Após implantar, copie a **URL do App da Web** (formato `/macros/s/.../exec`) e:
1. Cole no campo `REDIRECT_URI` do código
2. Atualize o **Link de redirecionamento** no Bling (Dados básicos → salvar)
3. Reimplante com nova versão

---

## Passo 4 — Autorizar o acesso

Na planilha (após F5 para recarregar):
```
Menu Bling → Autorizar acesso ao Bling
```

Clique em "Autorizar Bling agora" → faz login no Bling → autoriza → página de sucesso verde aparece automaticamente → fechar aba → pronto!

⚠️ **Não precisa copiar nenhum código** — o redirecionamento é automático.

---

## Como usar no dia a dia

### Buscar produto por SKU
```
Menu Bling → Buscar produto por SKU → digita o SKU → Enter
```
Preenche automaticamente: nome, SKU e custo na próxima linha vazia da planilha.

### Importar catálogo completo
```
Menu Bling → Importar catálogo completo
```
Importa todos os produtos ativos do Bling (máx 50) sem apagar os status de publicação já preenchidos.

### Adicionar colunas de publicação (fazer uma vez)
```
Menu Bling → Adicionar colunas publicação
```
Cria 3 colunas com dropdown **✅ Sim / ❌ Não / ⏳ Pendente**:
- ML Publicado
- Shopee Publicado
- Loja Publicada

---

## Detalhes técnicos da API Bling v3

### Autenticação
A API v3 usa OAuth 2.0 com Basic Auth no header do token:

```javascript
const credentials = Utilities.base64Encode(CLIENT_ID + ':' + CLIENT_SECRET);

// Troca do code pelo token
UrlFetchApp.fetch('https://api.bling.com.br/Api/v3/oauth/token', {
  method: 'POST',
  headers: {
    'Authorization': 'Basic ' + credentials,
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': '1.0'
  },
  payload: 'grant_type=authorization_code&code=XXX&redirect_uri=YYY'
});
```

⚠️ O `redirect_uri` enviado no token **deve ser idêntico** ao cadastrado no Bling.

### Endpoints utilizados

```
# Buscar produto por SKU
GET https://api.bling.com.br/Api/v3/produtos?codigo={sku}
Authorization: Bearer {access_token}
Accept: 1.0

# Listar produtos ativos
GET https://api.bling.com.br/Api/v3/produtos?situacao=A&limite=50

# Renovar token (expira em 6h)
POST https://api.bling.com.br/Api/v3/oauth/token
grant_type=refresh_token&refresh_token={refresh_token}
```

### Tokens
- **Access Token**: expira em 6 horas — o script renova automaticamente
- **Refresh Token**: expira em 30 dias — se expirar, precisa autorizar novamente pelo menu

---

## Erros comuns e soluções

| Erro | Causa | Solução |
|---|---|---|
| `invalid_client` | Client Secret errado no código | Conferir Client Secret no Bling |
| `redirect_uri_mismatch` | URL no Bling diferente do código | Atualizar Link de redirecionamento no Bling com a URL exata do Web App |
| `invalid_grant` / código expirado | Code OAuth expira em 60 segundos | O redirecionamento automático resolve — não copie o código manualmente |
| Bling não autorizado | Token expirado ou não autorizado | Menu Bling → Revogar → Autorizar novamente |
| Produto não encontrado | SKU incorreto ou produto inativo | Verificar SKU no Bling |

---

## Estrutura de arquivos

```
BlingIntegracao_v6.gs  ← código completo do Apps Script
```

Funções principais:
- `onOpen()` — cria o menu Bling
- `doGet(e)` — captura o código OAuth automaticamente
- `mostrarLinkAutorizacao()` — abre modal de autorização
- `trocarCodigoPorToken(code)` — troca code por access/refresh token
- `renovarToken()` — renova automaticamente quando expira
- `getAccessToken()` — retorna token válido (renova se necessário)
- `buscarProduto()` — busca por SKU e preenche planilha
- `preencherCatalogo()` — importa todos os produtos ativos
- `adicionarColunasPublicacao()` — adiciona colunas de status
- `buscarProdutoBling(sku, token)` — função auxiliar da API

---

## Quando reimplantar o Apps Script

Sempre que alterar o código, é obrigatório reimplantar com nova versão:
```
Implantar → Gerenciar implantações → lápis ✏️ → Nova versão → Implantar
```

A URL do Web App **não muda** entre versões — o link de redirecionamento no Bling continua válido.

---

## Configuração do Bling para o Full (fulfillment) — pendente

Quando ativar o Full no ML:
1. Criar filial no Bling com "Tipo de unidade: Fulfillment"
2. Configurar casas decimais para mínimo 4 em: Todas as configurações → Empresa → Geral
3. Instalar integração "Faturador do ML" na Central de Extensões
4. Ativar "Importar XML de NFe (Faturador)" nas regras de operação
5. Vincular produtos entre Bling e ML Fulfillment pelo SKU
