# 📊 Dashboard Financeiro + Fluxo de Caixa

> Dashboard interativo de análise financeira desenvolvido no Power BI, com foco em KPIs de receita, custos, despesas, lucro e fluxo de caixa mensal.

![Status](https://img.shields.io/badge/Status-Concluído-brightgreen?style=flat-square)
![Tool](https://img.shields.io/badge/Power%20BI-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![Type](https://img.shields.io/badge/Tipo-Análise%20Financeira-blue?style=flat-square)

---

## 📋 Sobre o Projeto

Este projeto consiste em um dashboard financeiro completo desenvolvido em **Power BI**, com o objetivo de analisar o desempenho financeiro de uma empresa ao longo do ano. O relatório apresenta uma visão consolidada de receitas, custos, despesas e lucro, além de uma análise detalhada do fluxo de caixa mensal.

O modelo de dados segue a arquitetura **Star Schema**, com tabelas fato e dimensão devidamente relacionadas, e medidas calculadas em **DAX**.

---

## 📄 Páginas do Dashboard

### 🏠 Home
Página de entrada com navegação para as demais seções do relatório.

### 📈 Visão Geral
Painel com os principais KPIs financeiros e análises por dimensão:
- **Receita Total:** R$ 35.334.463
- **Custos:** R$ 43.837.917
- **Despesas:** R$ 11.517.571
- **Lucro:** -R$ 20.021.025

Visuais incluídos:
- Receita por Mês (gráfico de barras)
- Receita por Tipo de Conta — Operacional vs Não Operacional (gráfico de rosca)
- Pagamentos por Tipo — Fixo vs Variável (gráfico de rosca)
- Pagamentos por Mês e Tipo (gráfico de barras empilhadas)
- Receita por Cliente (ranking dos principais clientes)

### 🔍 Detalhamento — Fluxo de Caixa
Análise mensal detalhada do fluxo de caixa:
- Gráfico de cascata (waterfall) do fluxo de caixa mês a mês
- Tabela com evolução mensal de Receitas, Custos, Despesas, Lucro e % de Lucro

---

## 🗂️ Modelo de Dados (Star Schema)

| Tabela | Tipo | Descrição |
|--------|------|-----------|
| `fRecebimentos` | Fato | Registros de recebimentos por cliente |
| `fPagamentos` | Fato | Registros de pagamentos realizados |
| `dCalendario` | Dimensão | Tabela de datas (ano, mês, dia) |
| `dPlanoContas` | Dimensão | Plano de contas (conta, tipo, lançamento) |
| `_Medidas` | Medidas DAX | Cálculos: % Lucro, Custos, Despesas, Lucro, Margem Bruta, Receitas |

---

## 🛠️ Tecnologias Utilizadas

- **Power BI Desktop** — criação do relatório e visualizações
- **DAX (Data Analysis Expressions)** — cálculo das medidas financeiras
- **Power Query** — transformação e tratamento dos dados
- **Star Schema** — modelagem dos dados

---

## ✨ Funcionalidades

- ✅ KPIs financeiros em tempo real com filtro por ano
- ✅ Análise de receita por mês, tipo de conta e cliente
- ✅ Classificação de pagamentos entre fixos e variáveis
- ✅ Fluxo de caixa em gráfico de cascata (waterfall)
- ✅ Tabela analítica com variação percentual de lucro mês a mês
- ✅ Navegação entre páginas com botões interativos

---

## 📸 Screenshots

> Adicione aqui prints das páginas do dashboard.

---

## 👩‍💻 Autora

**Ingridy Isabelli**  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/isapinho)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/ingridypinho)
