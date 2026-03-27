# Mercado Livre — Referência Completa R9

## Algoritmo do ML (como funciona o ranking)

O Mercado Livre usa um algoritmo próprio chamado internamente de **"relevância"**. Os principais fatores de ranking são:

### Fatores de maior peso
1. **Histórico de vendas** do anúncio (volume e recência)
2. **Taxa de conversão** (visitas → vendas)
3. **Reputação do vendedor** (termômetro e % reclamações)
4. **Qualidade do anúncio** (completude, fotos, descrição)
5. **Preço competitivo** vs. a média da categoria
6. **Frete grátis** (forte diferencial de ranking)
7. **Tempo de envio** (Full = maior peso; Flex e Coletas em seguida)

### Fatores secundários
- CTR (taxa de clique) nas buscas
- Avaliações positivas recentes
- Anúncios promovidos (Product Ads) — pagos mas influenciam visibilidade orgânica indiretamente

---

## Tipos de anúncio

| Tipo | Comissão | Visibilidade | Quando usar |
|---|---|---|---|
| Grátis | 0% | Mínima | Nunca para venda séria |
| Clássico | ~11-13% | Média | Produtos de baixa margem |
| Premium | ~14-16% | Máxima | Padrão recomendado |

> Sempre Premium para produtos com margem suficiente. A diferença de visibilidade compensa a comissão.

---

## Fulfillment (Mercado Envios Full)

**Vantagens:**
- Badge "Chegará amanhã" ou "Chegará hoje" → enorme conversão
- Maior posição no algoritmo
- Menos trabalho operacional (ML faz o picking/packing/entrega)

**Requisitos:**
- Produto aprovado pelo ML para Full
- Estoque enviado para centro de distribuição ML
- SKU e código de barras corretos

**Quando NÃO usar Full:**
- Produtos frágeis ou de alto valor sem embalagem adequada
- SKUs com baixa rotatividade (custo de armazenagem)
- Produtos com variações complexas

---

## Saúde do anúncio — checklist ML

- [ ] Título com 80+ caracteres usando keywords principais
- [ ] Mínimo 6 fotos (recomendado: 10+)
- [ ] Primeira foto: fundo branco, sem texto, sem marca d'água
- [ ] Descrição com 300+ palavras
- [ ] Ficha técnica preenchida 100% (atributos da categoria)
- [ ] Variações configuradas corretamente (cor, tamanho, etc.)
- [ ] Perguntas frequentes respondidas
- [ ] Preço competitivo (verificar buybox)
- [ ] Estoque mínimo de 3 unidades (evitar ruptura = queda no ranking)

---

## Reputação do vendedor — como funciona

### Termômetro (cores)
- 🟢 Verde: excelente (meta)
- 🟡 Amarelo: regular (atenção)
- 🔴 Vermelho: ruim (risco de suspensão)

### Métricas que afetam a reputação
| Métrica | Peso | Meta |
|---|---|---|
| Reclamações | Alto | < 1% |
| Cancelamentos pelo vendedor | Alto | < 2% |
| Envios com atraso | Médio | < 3% |
| Avaliações negativas | Médio | < 5% de negativas |

> Reputação é calculada sobre os últimos 60 dias. Ações urgentes impactam rápido.

---

## Campanhas Product Ads (ML ADS)

### Tipos disponíveis
- **Produto Patrocinado**: aparece como anúncio nas buscas — CPC (custo por clique)
- **Display**: banners em posições estratégicas — CPM ou CPC
- **Marcas patrocinadas**: para marcas com loja oficial

### Estratégia recomendada para início
1. Campanhas automáticas primeiro (ML decide onde anunciar)
2. Após 2 semanas: analisar quais keywords geraram venda
3. Criar campanha manual com as keywords de maior conversão
4. Negativar keywords irrelevantes que geraram cliques sem venda
5. Meta de ROAS: mínimo 4x (R$4 em vendas para cada R$1 investido)

### Estrutura de campanha recomendada
```
Campanha Principal [Auto]
  └── Grupo: Todos os produtos ativos

Campanha Performance [Manual]
  └── Grupo: Top produtos por margem
      └── Keywords: [extraídas da campanha auto]

Campanha Defesa [Manual]
  └── Grupo: Produtos ameaçados por concorrentes
      └── Keywords: brand + produto
```

---

## Categorias com maior potencial (nichos R9)

### Moda e Vestuário
- Alta concorrência, mas alto volume
- Diferencial: fotos lifestyle de qualidade + copy focado em fit e estilo
- Sazonalidade forte: verão, inverno, datas comemorativas

### Beleza e Cuidados Pessoais
- Crescendo aceleradamente no ML
- Regulatório: cosméticos precisam de registro Anvisa no cadastro
- Diferencial: descrição detalhada de ingredientes + resultados comprovados

### Esportes e Fitness
- Crescimento pós-pandemia mantido
- Alta busca por palavras técnicas (ex: "powerlifting", "funcional", "HIIT")
- Diferencial: especificações técnicas completas + público segmentado

---

## Políticas críticas para não ser suspenso

1. **Nunca vender réplicas ou produtos falsos** — banimento permanente
2. **Não infringir marcas registradas** nos títulos sem autorização
3. **Não incluir dados de contato** em nenhum campo do anúncio
4. **Não redirecionar para fora do ML** (links, QR codes, etc.)
5. **Estoque real**: anunciar produto sem estoque gera cancelamento e penalidade
6. **Fotos próprias**: usar fotos de terceiros sem autorização gera denúncia de IP
