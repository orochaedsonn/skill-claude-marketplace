# Bling + Mercado Livre — Configuração e Boas Práticas R9
> por Edson Rocha - R9mkt

## Princípio fundamental

O Bling é a **fonte da verdade**. Sempre edite produtos, preços e descrições no Bling — nunca diretamente no ML. O Bling sobrescreve o ML na próxima sincronização e você perde qualquer edição feita fora dele.

---

## Cadastro de produto no Bling antes de exportar para o ML

### Campos obrigatórios (sem eles o anúncio não vai ou vai incompleto)

| Campo | O que preencher | Observação |
|---|---|---|
| Nome | Título otimizado (fórmula da skill) | Use os 150 chars do ML |
| Código (SKU) | Código único interno | NUNCA mude após exportar — quebra o vínculo |
| Preço de venda | Preço final ao consumidor | Pode ter preço diferente por anúncio no carrinho verde |
| Unidade | UN ou PÇ | Obrigatório para emitir NF com certificado A1 |
| NCM | Código fiscal correto | Obrigatório para NF — consulte tabela NCM |
| Peso bruto | Em kg (ex: 0.350) | Afeta cálculo de frete — seja preciso |
| Dimensões | Comprimento × largura × altura em cm | Afeta frete — meça a embalagem final |

### Campos de descrição (aba produto)

- **Descrição curta**: não usar para ML — o ML usa a descrição do carrinho verde
- **Descrição complementar**: pode usar para observações internas
- **Observações**: visível apenas internamente no Bling

---

## Campos ocultos do ML — como ativar

Este é o ponto mais crítico para qualidade do anúncio. O ML exige atributos que ficam ocultos por padrão no Bling.

**Como ativar:**
```
Central de extensões → Minhas instalações → Mercado Livre
→ Campos personalizados de Produtos → ATIVAR
```

Depois de ativar, acesse o produto e preencha os campos customizados que aparecerem. Campos marcados com * são obrigatórios pelo ML.

### Campos customizados críticos por nicho (R9)

**Moda / Vestuário:**
- Gênero: Feminino / Masculino / Unissex
- Tamanho: usar nomenclatura padrão ML (P/M/G ou 34/36/38)
- Cor: nome padrão ML (Verde, não "verde musgo")
- Material/Composição: ex "80% Poliamida, 20% Elastano"
- Comprimento: curto/médio/longo

**Beleza / Cosméticos:**
- Tipo de pele (se aplicável)
- Volume/Conteúdo: ex "30ml"
- Gênero
- Linha/Série

**Fitness / Esportes:**
- Modalidade esportiva
- Material
- Peso máximo suportado (se aplicável)
- Tamanho/Tamanho único

### Como criar campos customizados no Bling
```
Todas as configurações → Sistema → Campos customizados → Criar novo campo
Cadastros → Categorias de produtos → selecione a categoria → vincule o campo
```
O Bling cria automaticamente os campos obrigatórios conforme a categoria vinculada ao ML. Preencha todos os marcados como obrigatório (*).

---

## Configurando o anúncio ML (carrinho verde)

Dentro do produto, clique no ícone/carrinho verde do ML:

```
Modalidade → sempre PREMIUM (visibilidade máxima)
Descrição → cole o copy otimizado (diferente do nome/título)
Preço → preço calculado com margem real
Frete grátis → ative se a margem permitir
```

**Para definir modalidade padrão para todos os anúncios:**
```
Central de extensões → Minhas instalações → Mercado Livre
→ Modalidade padrão dos anúncios → PREMIUM
```
Assim não precisa selecionar Premium toda vez que criar um anúncio.

---

## Regras de operação ML no Bling — configuração ideal

### Importação de Vendas

| Campo | Configuração recomendada | Motivo |
|---|---|---|
| Importar taxas do Marketplace | ✅ ATIVADO | Registra comissão ML no pedido — essencial para DRE e conciliação financeira real |
| Exibir apelido | Exibir | Identifica comprador pelo nick do ML antes de ter CPF |
| Importar nº do pedido nas observações | ✅ ATIVADO | Crítico — vincula pedido Bling ao pedido ML para rastreio e NF |
| Importar valor do frete | ✅ ATIVADO | Obrigatório para emitir NF com valor de frete correto (certificado A1) |
| Importar dados de faturamento | ✅ ATIVADO | Puxa CPF/CNPJ do comprador automaticamente para a NF |
| Importar XML de NFe (Faturador) | 🟡 DESATIVADO AGORA / ATIVAR quando configurar Full | Obrigatório para Full — quando ativar o Faturador ML, ativar este campo para o Bling importar o XML e lançar estoque + contas automaticamente |
| Cancelar NFe automaticamente | ❌ DESATIVADO | Cancelamento automático de NF é irreversível — sempre cancelar manualmente |
| Importar XML de NFe de Entrada | ❌ DESATIVADO | Só para compras/transferências — não aplica para vendas ML |
| Importar XML NFe Fulfillment | ❌ DESATIVADO | Ativar apenas quando usar Fulfillment ML |
| Importar pedidos Mercado Shops | ✅ ATIVADO | Cobre pedidos do Mercado Shops se usar |
| Data do pedido de venda | Data do pedido | Garante DRE e conciliação no dia correto |
| Importação de pedidos | Todos os pedidos | Importa pagos e em processamento — não perde nenhuma venda |
| Limite de dias para importação | Sem limite (início) / 30 dias (volume alto) | Com 500+ pedidos/mês, mude para 30 dias para evitar sobrecarga da API |

### Exportação de Vendas

| Campo | Configuração recomendada | Motivo |
|---|---|---|
| Enviar dados fiscais ao emitir NF | ✅ ATIVADO | Envia chave de acesso da NF para o ML automaticamente — obrigatório para liberar repasse |
| Enviar mensagem com dados fiscais | ❌ DESATIVADO | Gera spam na conversa do ML com o comprador — prejudica experiência |
| Enviar mensagem de recebimento | Depende da logística | Ativar apenas para Logística Própria ou Entrega a combinar |
| Mensagem de recebimento | Ver template abaixo | Configurar se ativar o campo acima |
| Sincronizar rastreamento ME1 | ✅ ATIVADO | Atualiza status do pedido no ML conforme rastreamento — crítico para reputação |
| Sincronização automática de status | ✅ ATIVADO | Automatiza atualização de status — essencial para reputação. Atenção: status como "entregue" são irreversíveis (correto e normal) |

**Template de mensagem de recebimento do pedido:**
```
Olá! Recebemos seu pedido e já estamos separando com carinho.
Em breve você receberá o código de rastreio.
Qualquer dúvida, estamos à disposição! 😊
```

---

## Precificação — cálculo obrigatório antes de exportar

Monte esse cálculo para cada produto antes de definir o preço no Bling:

```
Custo do produto:               R$ ____
+ Custo de embalagem:           R$ ____
+ Frete médio (custo real):     R$ ____
────────────────────────────────────────
= Custo total:                  R$ ____

Sobre o preço de venda incidem:
  Comissão ML Premium:          16%
  Simples Nacional:             ~6% (verificar sua faixa)
  Gateway/repasse ML:           já incluso na comissão

Fórmula do preço mínimo viável:
Preço = Custo total ÷ (1 - 0,16 - 0,06)
      = Custo total ÷ 0,78

Com margem de 30%:
Preço = Custo total ÷ 0,78 ÷ 0,70
```

**Dica prática:** Mantenha uma planilha Google Sheets com essa fórmula. O Bling recebe o preço final calculado — nunca precifique de cabeça.

---

## Variações de produto no Bling

Para produtos com cor, tamanho ou outras variações:

```
Cadastros → Produtos → + Incluir cadastro
Formato: Simples ou com variação → adicionar atributos
Atributo 1: Cor → opções: Preto, Branco, Rosa (Enter entre cada)
Atributo 2: Tamanho → opções: P, M, G, GG (Enter entre cada)
→ Clicar em "Adicionar variação"
```

Cada combinação vira uma linha na tabela de variações — cada uma tem SKU, preço e estoque próprios.

⚠️ Cada variação tem um ID único no ML (VARIATION_ID). Para vincular variações já existentes no ML ao Bling, exporte a planilha de anúncios do ML e copie o ID de cada variação para o carrinho verde correspondente.

---

## Checklist completo antes de exportar para o ML

### Produto
- [ ] Nome com 80-150 chars e keywords principais no início
- [ ] SKU único definido (não mudar após exportar)
- [ ] NCM correto preenchido
- [ ] Peso bruto correto (kg)
- [ ] Dimensões corretas da embalagem (cm)
- [ ] Campos customizados/ocultos todos preenchidos
- [ ] Variações configuradas (cor, tamanho)
- [ ] Mínimo 6 imagens (primeira: fundo branco, sem texto)

### Anúncio (carrinho verde ML)
- [ ] Modalidade: Premium
- [ ] Descrição otimizada colada (diferente do título)
- [ ] Preço calculado com margem real
- [ ] Frete grátis configurado se margem permitir

### Configurações gerais (fazer uma vez)
- [ ] Campos ocultos ML ativados nas configurações
- [ ] Modalidade padrão definida como Premium
- [ ] Todas as regras de importação/exportação configuradas conforme tabela acima
- [ ] Certificado A1 ativo e válido para emissão de NF

---

## Faturador ML + Full — modelo híbrido obrigatório

### Regra não negociável

Para vender no Full é OBRIGATÓRIO usar o Faturador do ML. As NF-e são emitidas automaticamente no centro de distribuição — não tem como usar o Bling para emitir no Full.

Mas isso não substitui o Bling — os dois operam em camadas complementares.

### Dois fluxos de faturamento

**Envio próprio (ME1, ME2):**
```
Venda no ML
    ↓
Bling importa o pedido
    ↓
Você emite NF-e pelo Bling (certificado A1) — automático
    ↓
Bling envia chave de acesso ao ML
    ↓
ML libera repasse
```

**Full (estoque no CD do ML):**
```
Venda no ML Full
    ↓
Faturador ML emite NF-e automaticamente no CD
    ↓
Bling importa XML da NF via "Importar XML de NFe (Faturador)"
    ↓
Bling lança estoque e contas automaticamente
```

### Comparativo: Faturador ML vs Bling

| Critério | Faturador ML | Bling (certificado A1) |
|---|---|---|
| Custo | Gratuito | Incluso no Bling |
| Full | ✅ Obrigatório e automático | ❌ Não funciona no Full |
| Envio próprio ME1/ME2 | Funciona mas manual | ✅ Automático e integrado |
| Controle financeiro / DRE | ❌ Fraco | ✅ Completo |
| Multi-canal (Shopee, loja própria) | ❌ Só ML | ✅ Todos os canais |
| Emissão em massa | Sim, no painel ML | ✅ Automático |
| Integração contábil | ❌ Não | ✅ Exporta para contador |

**Conclusão: usar os dois. Nunca 100% Faturador ML — sem DRE, sem conciliação, sem multi-canal.**

### Restrição de estado

A integração Faturador ML + Bling está disponível APENAS para São Paulo.
Clientes da R9 em outros estados: não podem usar essa integração — emitem NF pelo Bling normalmente para todos os pedidos (inclusive Full exige atenção especial nesses casos).

### Como ativar o Faturador ML no Bling (quando for para o Full)

**Pré-requisitos:**
- [ ] CNPJ habilitado na SEFAZ do seu estado
- [ ] Inscrição Estadual (IE) cadastrada no ML com dados idênticos à SEFAZ
- [ ] Certificado A1 associado ao Faturador ML (mesmo certificado ou um novo)
- [ ] Conta PJ no ML (MEI do RS não usa o faturador)
- [ ] Empresa em SP (para integração Bling + Faturador)

**Passo a passo no Bling:**
```
1. Central de extensões → buscar "Faturador do Mercado Livre" → instalar
2. Nome do canal: "Faturador ML" (para diferenciar da integração principal)
3. Autenticar com a conta ML (mesmo login)
4. Configurar naturezas de operação:
   - Venda ML Full → CFOP 6.108 ou conforme orientação do contador
   - Retorno simbólico → CFOP correspondente
5. Vincular produtos: SKU Bling = SKU ML (obrigatório para o vínculo funcionar)
6. Exportar dados fiscais dos produtos para o Faturador
7. Ativar "Importar XML de NFe (Faturador)" nas regras de operação ML
8. Ativar "Lançar contas ao importar XML"
9. Ativar "Lançar estoque ao importar XML"
```

**⚠️ Ordem importa:** vincular produtos antes de ativar a importação — se ativar antes, as notas chegam sem vínculo e não lançam estoque/contas.

### Checklist de ativação do Full + Faturador

**Antes de enviar estoque para o CD do ML:**
- [ ] Faturador ML instalado e autenticado no Bling
- [ ] Naturezas de operação configuradas (validar com contador)
- [ ] Produtos vinculados entre Bling e ML Fulfillment (SKU idêntico)
- [ ] Dados fiscais dos produtos exportados para o Faturador
- [ ] "Importar XML de NFe (Faturador)" ATIVADO nas regras de operação
- [ ] "Lançar contas ao importar XML" ATIVADO
- [ ] "Lançar estoque ao importar XML" ATIVADO
- [ ] "Importar XML NFe Fulfillment" ATIVADO nas regras de operação ML
- [ ] Teste com 1 produto antes de enviar todo o estoque

### Custos do Full ML (referência 2025)

Armazenagem por unidade/dia:
- Pequeno (até 12×15×25cm, até 18kg): R$ 0,007/dia
- Médio (até 28×36×51cm, até 18kg): R$ 0,013/dia
- Grande (até 60×60×70cm, até 18kg): R$ 0,047/dia
- Extragrande: R$ 0,107/dia

⚠️ Produtos parados por muito tempo geram taxa extra — giro de estoque é obrigatório no Full.

---

## Erros comuns de grandes vendedores no Bling + ML

1. **Mudar o SKU após exportar** → quebra o vínculo e cria anúncio duplicado
2. **Editar descrição/preço direto no ML** → Bling sobrescreve na próxima sync e você perde a edição
3. **Não preencher campos ocultos** → anúncio perde posição no algoritmo ML
4. **Peso/dimensão errados** → frete calculado errado → prejuízo ou reclamação
5. **Não ativar sincronização automática de status** → reputação cai por não atualizar status de entrega
6. **Cancelar NF automaticamente ativado** → risco de cancelar NFs válidas automaticamente
7. **Limite de importação sem limite com alto volume** → API sobrecarregada, atrasos no Bling
8. **Ativar "Importar XML Faturador" antes de vincular produtos** → notas chegam sem vínculo, não lançam estoque nem contas
9. **Enviar estoque para o Full sem configurar o Faturador** → NF não é emitida, CD não libera o produto para venda
10. **SKU diferente entre Bling e ML no Full** → vínculo quebrado, estoque e contas não sincronizam
