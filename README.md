# 📊 Dashboard Financeiro — Fluxo de Caixa e KPIs

Dashboard interativo de análise financeira em Power BI, com modelagem dimensional em Star Schema, ETL em Power Query e medidas em DAX para receita, custos, despesas, lucro e fluxo de caixa mensal.

> **Sobre os dados.** A base é fictícia e cobre recebimentos e pagamentos de 2017 a 2024. Os valores não representam nenhuma operação real: há anos com resultado negativo, o que serve justamente para exercitar o comportamento das medidas de margem e variação quando o denominador é negativo ou próximo de zero.

---

## 🎯 A pergunta que o projeto responde

Relatório financeiro costuma parar em "quanto entrou e quanto saiu". Isso não sustenta decisão.

As perguntas que este dashboard responde são outras:

- O resultado do mês veio de receita maior ou de custo menor?
- Quanto do pagamento é fixo e quanto é variável — ou seja, quanto dá pra cortar se precisar?
- Qual cliente concentra receita a ponto de virar risco?
- Lucro e caixa contam a mesma história neste mês?

A última é a que mais importa e a que mais gente ignora: **lucro é competência, caixa é liquidez.** Uma empresa lucrativa quebra por caixa.

Os indicadores foram escolhidos a partir de quatro anos de rotina fiscal e financeira, produzindo o relatório mensal que a diretoria de fato usava — não a partir de um template.

---

## 🖥️ Preview

<!-- TODO: exportar os prints das duas páginas, criar a pasta docs/images/, commitar os arquivos e remover este comentário.

### Visão Geral
![Visão Geral do dashboard financeiro](docs/images/visao-geral.png)

### Detalhamento — Fluxo de Caixa
![Gráfico de cascata do fluxo de caixa mensal](docs/images/fluxo-de-caixa.png)

-->

---

## 🗂️ Modelo de dados (Star Schema)

| Tabela | Tipo | Conteúdo |
|---|---|---|
| `fRecebimentos` | Fato | Recebimentos por cliente e data |
| `fPagamentos` | Fato | Pagamentos realizados, por conta e data |
| `dCalendario` | Dimensão | Tabela de datas contínua, marcada como tabela de datas |
| `dPlanoContas` | Dimensão | Plano de contas: conta, tipo e natureza do lançamento |
| `_Medidas` | Medidas | Receitas, Custos, Despesas, Lucro, % Lucro, Margem Bruta |

```
        dCalendario                 dPlanoContas
             │                            │
             ├──────────┬─────────────────┤
             ▼          ▼                 ▼
      fRecebimentos          fPagamentos
```

### Decisões de modelagem

**Por que Star Schema e não uma tabela única.** Duas razões concretas. A primeira é tamanho: texto repetido (nome de cliente, descrição de conta) comprime muito melhor isolado numa dimensão do que replicado em cada linha da fato. A segunda, e mais importante: com duas tabelas fato e uma tabela única eu não teria um eixo de tempo comum — não daria para comparar recebimento e pagamento no mesmo mês sem ambiguidade de relacionamento.

**Por que uma tabela calendário dedicada.** As funções de time intelligence do DAX (`SAMEPERIODLASTYEAR`, `DATEADD`, `TOTALYTD`) exigem uma tabela de datas contínua e marcada como tal. Usar a coluna de data da própria fato quebra em dois casos: um mês sem lançamento simplesmente desaparece do eixo, e duas fatos não teriam um calendário comum para se relacionar.

**Relacionamentos unidirecionais.** Dimensão filtra fato, em uma direção só. Filtro bidirecional abre mais de um caminho entre as tabelas e é a origem clássica do total que muda quando você mexe num filtro sem motivo aparente.

---

## 📄 Páginas

### Home
Navegação para as demais seções.

### Visão Geral
KPIs consolidados com filtro por ano, e a leitura por dimensão:

- Receita por mês
- Receita por tipo de conta — operacional vs. não operacional
- Pagamentos por tipo — fixo vs. variável
- Pagamentos por mês e tipo (barras empilhadas)
- Receita por cliente, para leitura de concentração

### Detalhamento — Fluxo de Caixa
- Gráfico de cascata mês a mês, mostrando de onde vem cada variação
- Tabela com evolução mensal de receitas, custos, despesas, lucro e % de lucro

---

## 🧮 Medidas em DAX

```dax
Receitas = SUM( fRecebimentos[Valor] )

Custos =
CALCULATE(
    SUM( fPagamentos[Valor] ),
    dPlanoContas[Tipo] = "Custo"
)

Despesas =
CALCULATE(
    SUM( fPagamentos[Valor] ),
    dPlanoContas[Tipo] = "Despesa"
)

Lucro = [Receitas] - [Custos] - [Despesas]

% Lucro = DIVIDE( [Lucro], [Receitas] )
```

`DIVIDE` em vez do operador `/`: devolve em branco na divisão por zero, em vez de erro. Num relatório financeiro com meses sem receita, isso é a diferença entre um visual limpo e um visual cheio de `#ERRO`.

---

## 🛠️ Stack

| Camada | Ferramenta |
|---|---|
| ETL | Power Query — limpeza, padronização e tipagem antes da carga |
| Modelagem | Star Schema, relacionamentos unidirecionais |
| Cálculo | DAX |
| Visualização | Power BI Desktop |

---

## 🚀 Como abrir

1. Baixe o [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (gratuito, Windows).
2. Clone o repositório:
   ```bash
   git clone https://github.com/Isapinhoo/powerbi-fluxo-de-caixa.git
   ```
3. Abra o `.pbix` dentro da pasta `Power BI - Financeiro + Fluxo de Caixa/`.

As bases de origem ficam em `01 - DataBase/` (recebimentos por ano e mês, pagamentos por ano, e o cadastro de plano de contas) e os planos de fundo das páginas em `00 - Assets/Background/`. Se o Power Query reclamar do caminho das fontes, aponte a pasta `01 - DataBase` no seu clone local.

---

## 🔭 Próximos passos

- [ ] Comparativo com o mesmo período do ano anterior (`SAMEPERIODLASTYEAR`)
- [ ] Indicador de concentração de receita por cliente (participação do top 5)
- [ ] Separação entre regime de competência e regime de caixa
- [ ] Projeção simples de caixa para os próximos 3 meses
- [ ] Publicação no Power BI Service com atualização agendada

---

## 👩‍💻 Autora

**Ingridy Isabelli Sant'Ana de Pinho**
Sistemas de Informação — Universidade Anhembi Morumbi
SQL · Python · Power BI · Salesforce Marketing Cloud

[LinkedIn](https://linkedin.com/in/isapinho) · [GitHub](https://github.com/Isapinhoo)
