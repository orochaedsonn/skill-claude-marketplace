# Precificação e Análise de Concorrentes — R9 Marketplace

## Modelo de precificação para marketplace

### Fórmula base de preço mínimo viável
```
Preço Mínimo = Custo do produto
             + Frete (custo real médio)
             + Comissão da plataforma (%)
             + Imposto sobre venda (Simples/MEI/etc.)
             + Custo operacional por pedido
             + Margem mínima desejada (%)
```

### Comissões por plataforma (referência 2024-2025)
| Plataforma | Faixa de comissão | Observação |
|---|---|---|
| Mercado Livre | 11% a 16% | Varia por categoria; Classic vs Premium |
| Shopee | 14% a 20% | Inclui taxa de serviço + frete subsidiado |
| Amazon | 8% a 15% | Varia por categoria |
| Nuvemshop/Shopify | 0% (mensalidade fixa) | Gateway de pagamento cobra à parte (~4%) |

> ⚠️ Sempre confirmar comissões atuais na central do vendedor — mudam com frequência.

---

## Estratégias de precificação

### 1. Precificação pela buybox (conquista de posição)
- Mapeie os top 5 do ranking para o mesmo produto/categoria
- Identifique o menor preço competitivo com boa reputação (4+ estrelas)
- Posicione-se entre o 2º e 3º menor preço, com copy superior
- **Não**: guerra de preço com quem tem margem negativa — deixe sangrar

### 2. Precificação por valor percebido
Para nichos de moda, beleza e fitness premium:
- Preço acima da média do mercado
- Justificado por: fotos profissionais, descrição detalhada, reputação alta, frete rápido
- Funciona quando: diferencial de produto ou branding é claro

### 3. Precificação dinâmica (via automação n8n)
Ver `references/n8n-automacao.md` para workflow de monitoramento de preço.

---

## Como fazer análise de concorrentes

### Quando o usuário colar dados de concorrentes, analisar:

**Estrutura de análise:**
```
PRODUTO: [nome]
PLATAFORMA: [ML / Shopee / Amazon]

TOP 5 CONCORRENTES:
| Vendedor | Preço | Frete | Reputação | Vendas/mês (est.) | Diferencial |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

GAPS ENCONTRADOS:
- Copy fraco nos concorrentes? [sim/não + detalhe]
- Imagens abaixo do padrão? [sim/não]
- Descrição incompleta? [sim/não]
- Preço desposicionado? [sim/não]

RECOMENDAÇÃO DE ENTRADA:
- Preço sugerido: R$ X,XX
- Diferencial a explorar: [...]
- Primeiro passo: [...]
```

---

## Estimativa de volume de vendas

### Método de estimativa no Mercado Livre
1. Acesse o anúncio do concorrente
2. Veja "X vendidos" no anúncio
3. Divida pelo tempo de vida do anúncio (data de criação na URL ou Histórico)
4. Resultado: vendas/mês estimado

### Ferramenta alternativa
- **Nubimetrics** (pago): mais preciso, histórico completo ML + Shopee BR
- **Olist Bseller**: bom para ML
- Manualmente: acompanhar 7 dias e projetar

---

## Estratégia de entrada em nova plataforma

Quando o usuário pedir estratégia de entrada:

### Checklist de lançamento
- [ ] Pesquisa de categoria: volume de busca, sazonalidade, concorrência
- [ ] Mapeamento dos top 10 vendedores: preço, reputação, diferenciais
- [ ] Definição de SKUs prioritários para entrada (os de maior margem e menor concorrência)
- [ ] Precificação inicial: competitiva para gerar vendas rápidas e reputação
- [ ] Meta de reputação: chegar a 4.5+ antes de ajustar preço para cima
- [ ] Calendário promocional: datas como Black Friday, Mês do Consumidor, sazonalidade do nicho

### Plano de 90 dias padrão
- **Dias 1-30**: preço agressivo, foco em reputação e reviews
- **Dias 31-60**: otimização de copy com base nos dados reais de conversão
- **Dias 61-90**: ajuste de margem, ativação de campanhas ADS

---

## Análise de rentabilidade por canal

Quando o usuário quiser comparar canais:

```
PRODUTO: [nome] | CUSTO: R$ [X]

| Canal | Preço venda | Comissão | Frete | Imposto | Lucro líquido | Margem % |
|---|---|---|---|---|---|---|
| ML Classic | R$ | R$ | R$ | R$ | R$ | % |
| ML Premium | R$ | R$ | R$ | R$ | R$ | % |
| Shopee | R$ | R$ | R$ | R$ | R$ | % |
| Loja própria | R$ | R$ | R$ | R$ | R$ | % |

CANAL MAIS RENTÁVEL: [canal]
CANAL MAIS ESTRATÉGICO (volume): [canal]
RECOMENDAÇÃO: [texto]
```
