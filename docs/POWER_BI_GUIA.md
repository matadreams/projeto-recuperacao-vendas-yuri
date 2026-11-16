# Guia rápido para montar o Power BI

## Importação

1. Abra o Power BI Desktop.
2. Selecione **Obter dados > Texto/CSV**.
3. Importe `data/processed/vendas_tratadas.csv`.
4. Confirme que `InvoiceDate` está como Data/Hora, `Quantity` como número inteiro, `UnitPrice` e `Revenue` como número decimal.
5. Crie uma tabela calendário ou use a coluna `YearMonth` para o eixo mensal.

## Medidas DAX

```DAX
Faturamento = SUM(vendas_tratadas[Revenue])

Pedidos = DISTINCTCOUNT(vendas_tratadas[InvoiceNo])

Itens vendidos = SUM(vendas_tratadas[Quantity])

Ticket médio = DIVIDE([Faturamento], [Pedidos])

Faturamento por pedido = DIVIDE([Faturamento], [Pedidos])
```

Formate `Faturamento` e `Ticket médio` como moeda GBP. Use separador de milhar nos cartões.

## Página 1 — Visão geral

- Título: **Vendas e desempenho no varejo online**.
- Subtítulo: `Fonte: UCI Online Retail | Período: 01/12/2010 a 09/12/2011 | Moeda: GBP`.
- Cartões: Faturamento, Pedidos, Itens vendidos e Ticket médio.
- Linha: Faturamento por `YearMonth`.
- Barras: Faturamento por `Country`, ordenado de forma decrescente.
- Segmentadores: `YearMonth`, `Country` e `Description`.
- Texto de rodapé: `Valores representam faturamento bruto calculado como Quantity × UnitPrice. Cancelamentos e valores não positivos foram excluídos dos KPIs.`

## Página 2 — Produtos e mercados

- Ranking de `Description` por Faturamento.
- Barras de Faturamento por País.
- Tabela com Produto, Faturamento, Itens e Pedidos.
- Filtros por país e período.

## Página 3 — Metodologia e limitações

Inclua caixas de texto com a fonte, licença CC BY 4.0, regras de limpeza, período, moeda, exclusão de `CustomerID`, limitações e a observação de que a análise é descritiva e não demonstra causalidade.

## Evidências

Depois de montar as páginas, exporte o relatório para PDF ou tire capturas legíveis. Salve as evidências em `powerbi/`. Salve também o arquivo `.pbix` nessa pasta. Se o Power BI Service for usado, confira as permissões antes de inserir o link no README e no AVA.
