# R9 Marketplace Skill — v2.0

Desenvolvida por **Edson Rocha - R9mkt**

Skill para Claude Code especializada em gestão de marketplaces e e-commerce.

Cobre Mercado Livre, Shopee, Amazon e plataformas próprias (Nuvemshop/Shopify) — desde copy de anúncios até automações com n8n.

---

## O que essa skill faz

Ao instalar, o Claude passa a ter conhecimento especializado em:

- Criar e otimizar títulos e descrições de anúncios para ML e Shopee
- Estratégias de precificação e análise de concorrentes
- Responder clientes, gerenciar reclamações e proteger reputação
- Gerar relatórios de performance para apresentar a clientes
- Criar workflows de automação com n8n + APIs dos marketplaces
- Aplicar as regras e políticas do Mercado Livre e Shopee corretamente
- Configurar e integrar o Bling ERP com o Mercado Livre (NF, Full, Faturador)
- Integrar o Bling com Google Sheets via API v3 + Apps Script para precificação

---

## Instalação

### Requisitos
- [Claude Code](https://claude.ai/code) instalado

### Passo a passo

1. Clone este repositório:
   ```bash
   git clone https://github.com/orochaedsonn/skill-claude-marketplace.git
   ```

2. Mova para a pasta de skills do Claude Code:

   **Windows:**
   ```
   %APPDATA%\Local\Claude\skills\user\r9-marketplace\
   ```

   **Mac/Linux:**
   ```
   ~/.claude/skills/user/r9-marketplace/
   ```

3. Reinicie o Claude Code — a skill será detectada automaticamente.

---

## Estrutura do repositório

```
r9-marketplace/
├── SKILL.md                        # Definição principal da skill (lida pelo Claude)
└── references/
    ├── anuncios-copy.md            # Regras e templates para títulos e descrições
    ├── precificacao.md             # Estratégias de preço e análise competitiva
    ├── atendimento.md              # Respostas a clientes, reclamações, mediação
    ├── relatorios.md               # Templates de relatórios para clientes
    ├── n8n-automacao.md            # Workflows e integrações via n8n
    ├── mercado-livre.md            # Algoritmo, políticas e boas práticas do ML
    ├── shopee.md                   # Algoritmo, boosting e políticas da Shopee
    ├── bling-ml.md                 # Configuração Bling+ML, Faturador, Full, checklist
    └── bling-google-sheets.md      # Integração Bling API v3 com planilha de precificação
```

---

## Como usar

Depois de instalar, basta conversar com o Claude normalmente. A skill é ativada automaticamente quando você mencionar:

- Mercado Livre, Shopee, marketplace, anúncio, listing
- Título de produto, descrição de produto
- Precificação, concorrente, buybox
- Relatório de vendas, performance de loja
- Campanha ADS, Product Ads
- n8n, automação, API do Mercado Livre ou Shopee
- Bling, integração Bling+ML, Faturador ML, Full, NF, certificado A1
- Bling + Google Sheets, planilha de precificação, Apps Script, OAuth Bling
- "me ajuda com minha loja", "precificar", "anúncio"

### Exemplos de uso

```
"Cria um título otimizado para tênis masculino no Mercado Livre"

"Como devo responder uma reclamação de produto com defeito no ML?"

"Analisa a estratégia de preço para minha loja de cosméticos na Shopee"

"Monta um relatório de performance mensal para apresentar ao cliente"

"Cria um workflow em n8n para atualizar estoque via API do ML"

"Como configuro o Bling para emitir NF automaticamente no ML?"

"Como integro o Bling com o Google Sheets para precificação via Apps Script?"
```

---

## Contexto de uso

Essa skill foi criada por **Edson Rocha - R9mkt** para o fluxo de trabalho da agência, mas funciona para qualquer agência ou vendedor que gerencie:

- Contas próprias em marketplaces
- Contas de clientes (modo agência)
- Lojas em Nuvemshop ou Shopify integradas com ML/Shopee

**Stack de automação suportada:** n8n auto-hospedado via Coolify em VPS.

---

## Como contribuir

Contribuições são bem-vindas! Especialmente:

- Novas referências de plataformas (Amazon, Magalu, Americanas)
- Templates adicionais de relatórios
- Workflows prontos de n8n
- Correções nas políticas dos marketplaces (as regras mudam com frequência)

### Para contribuir

1. Fork este repositório
2. Crie uma branch: `git checkout -b minha-contribuicao`
3. Edite ou adicione arquivos em `references/`
4. Abra um Pull Request descrevendo o que mudou e por quê

### Padrão dos arquivos de referência

Cada arquivo em `references/` deve seguir o padrão:
- Título claro com `#` e subtítulos com `##`
- Tabelas para comparações e checklists
- Exemplos práticos e prontos para usar
- Seção de "quando usar" para orientar o Claude

---

## Licença

MIT — use, adapte e distribua livremente.

---

Desenvolvido por **[Edson Rocha - R9mkt](https://github.com/orochaedsonn)**
