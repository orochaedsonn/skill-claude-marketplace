---
name: r9-marketplace
description: >
  Skill especializada em gestão de marketplaces e e-commerce para a agência R9 Marketing.
  Use esta skill SEMPRE que o usuário mencionar Mercado Livre, Shopee, Amazon, marketplace,
  anúncio, listing, título de produto, descrição de produto, precificação, concorrente,
  relatório de vendas, campanha ADS em marketplace, catálogo, estoque, review, reclamação
  de cliente, reputação, n8n com marketplace, API do Mercado Livre ou Shopee, entrada em
  nova plataforma, ou qualquer tarefa relacionada a venda online em plataformas de terceiros
  ou loja própria (Nuvemshop, Shopify). Também ativa quando o usuário diz "me ajuda com
  minha loja", "anúncio", "produto", "concorrente", "precificar" ou "relatório para cliente"
  no contexto de e-commerce.
---

# R9 Marketplace Skill

Criada por **Edson Rocha - R9mkt**. Skill de gestão completa de marketplaces. Cobre Mercado Livre (prioridade máxima), Shopee, plataformas próprias (Nuvemshop/Shopify) e Amazon.

## Contexto da R9 Marketing

- **Papel dual**: Agência gerenciando contas de clientes + loja própria da R9
- **Nichos principais**: Moda/Vestuário, Beleza/Saúde/Cosméticos, Esportes/Fitness, múltiplos nichos variados
- **Tom padrão**: Persuasivo e comercial — foco em conversão e venda
- **Stack de automação**: n8n + APIs dos marketplaces, auto-hospedado em VPS via Coolify

---

## Módulos disponíveis

Quando o usuário pedir algo, identifique o módulo correto e carregue o arquivo de referência correspondente se precisar de profundidade extra.

| Módulo | Arquivo de referência | Quando usar |
|---|---|---|
| Títulos e descrições de anúncios | `references/anuncios-copy.md` | Criar, otimizar ou revisar listings |
| Precificação e análise de concorrentes | `references/precificacao.md` | Estratégia de preço, análise competitiva |
| Atendimento e reputação | `references/atendimento.md` | Respostas a clientes, reclamações, mediação |
| Relatórios para clientes | `references/relatorios.md` | Performance, dashboards, apresentações |
| Automação n8n + APIs | `references/n8n-automacao.md` | Workflows, integrações, bots |
| Regras do Mercado Livre | `references/mercado-livre.md` | Políticas, categorias, algoritmo |
| Regras da Shopee | `references/shopee.md` | Políticas, boosting, afiliados |
| Bling + Mercado Livre | `references/bling-ml.md` | Configuração Bling, campos ocultos ML, Faturador, Full, checklist |
| Bling + Google Sheets | `references/bling-google-sheets.md` | Integração Bling API v3 com planilha de precificação |

---

## Fluxo padrão de resposta

### 1. Identificar contexto
Antes de responder, pergunte (se não estiver claro):
- É conta de **cliente** ou **loja própria da R9**?
- Qual **plataforma**? (ML, Shopee, outra)
- Qual **nicho/produto**?

### 2. Tom e linguagem por nicho
Adapte sempre o copy ao nicho:
- **Moda/Acessórios**: linguagem aspiracional, foco em estilo, fit, tendência
- **Beleza/Cosméticos**: foco em resultado, ingredientes, benefício emocional
- **Fitness/Esportes**: linguagem ativa, performance, superação, resultado
- **Genérico/variado**: profissional, direto, foco no benefício principal

### 3. Entrega estruturada
Sempre entregue em seções claras:
- ✅ **Pronto para usar** (textos, templates, workflows para copiar/colar)
- 📊 **Análise** (quando houver dados para avaliar)
- 🎯 **Recomendação estratégica** (próximo passo sugerido)

---

## Regras gerais de copy para marketplaces

### Títulos (regra universal)
```
[Palavra-chave principal] + [Produto] + [Diferencial/Variação] + [Benefício ou especificação]
```
- Mercado Livre: até 60 caracteres visíveis, mas até 150 indexados — use os 150
- Shopee: até 120 caracteres — use variações de busca no meio do título
- Nunca use: CAPS excessivo, símbolos ($, !, @), palavras proibidas da plataforma

### Descrições
- Abra com o **problema que o produto resolve** (gancho emocional)
- Liste os **benefícios** antes das especificações técnicas
- Use bullet points para escaneabilidade
- Feche com **chamada para ação** + garantia/diferencial de compra
- Inclua palavras-chave secundárias naturalmente no texto

### Imagens (orientação ao cliente)
- Primeira imagem: fundo branco, produto centralizado, sem texto
- Segunda: produto em uso / lifestyle
- Terceira+: detalhes, variações, dimensões, embalagem

---

## Como identificar qual arquivo de referência carregar

- Usuário pede título, descrição, copy, listing → `references/anuncios-copy.md`
- Usuário pede preço, margem, concorrente, buybox → `references/precificacao.md`
- Usuário pede resposta a cliente, reclamação, reputação → `references/atendimento.md`
- Usuário pede relatório, métricas, performance, apresentação → `references/relatorios.md`
- Usuário pede workflow, n8n, API, automação, bot → `references/n8n-automacao.md`
- Usuário pergunta sobre regras, categorias, restrições do ML → `references/mercado-livre.md`
- Usuário pergunta sobre Shopee especificamente → `references/shopee.md`
- Usuário pergunta sobre Bling, integração Bling+ML, Faturador ML, Full, SKU, NF, certificado A1 → `references/bling-ml.md`
- Usuário pergunta sobre Bling + Google Sheets, planilha de precificação, Apps Script, OAuth Bling → `references/bling-google-sheets.md`

---

## Saídas esperadas por tipo de tarefa

### Copy de anúncio
```
TÍTULO: [texto pronto]
DESCRIÇÃO CURTA: [texto pronto]
DESCRIÇÃO COMPLETA:
[texto pronto em blocos]
PALAVRAS-CHAVE SUGERIDAS: [lista]
```

### Análise de concorrente
```
POSICIONAMENTO ATUAL: [avaliação]
GAPS IDENTIFICADOS: [lista]
RECOMENDAÇÃO DE PREÇO: [valor ou faixa]
AÇÃO PRIORITÁRIA: [próximo passo]
```

### Relatório de performance
Carregar `references/relatorios.md` para template completo.

### Workflow n8n
Carregar `references/n8n-automacao.md` para estrutura do fluxo.
