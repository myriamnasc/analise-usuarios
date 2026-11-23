
# Análise Comportamental de Usuários com SQL e Python

## Sobre o projeto

Este projeto tem como objetivo construir uma tabela de atributos comportamentais (*Feature Store*) dos usuários de um sistema de fidelidade associado à comunidade Téo Me Why, da Twitch.

A partir dos registros de transações, foram desenvolvidas consultas SQL para identificar padrões de utilização, frequência de interações, preferências por produtos e comportamento de acúmulo e resgate de pontos.

Os dados são consolidados em uma tabela que reúne características individuais dos usuários, considerando diferentes janelas temporais. Essa estrutura foi preparada para utilização em etapas posteriores de análise de dados e Machine Learning.

## Objetivos

Construir uma base consolidada com informações que permitam compreender o comportamento dos usuários, considerando:

- Quantidade de transações históricas e nos últimos 7, 14, 28 e 56 dias;
- Dias desde a última interação e tempo de permanência na base;
- Produtos mais utilizados em diferentes períodos;
- Saldo atual de pontos;
- Pontos acumulados positivos e negativos;
- Dias da semana e períodos do dia com maior atividade;
- Indicador de engajamento dos últimos 28 dias em relação ao histórico.

## Fonte de dados

Os dados utilizados foram disponibilizados no Kaggle:

[TeoMeWhy - Loyalty System](https://www.kaggle.com/datasets/teocalvo/teomewhy-loyalty-system)

A base contém registros relacionados ao sistema de fidelidade da comunidade, incluindo informações de clientes, transações e produtos.

## Tecnologias utilizadas

- **SQL (SQLite):** consultas, agregações e transformação dos dados.
- **Python:** execução e integração das consultas com o banco de dados.
- **Pandas:** leitura e manipulação dos resultados em DataFrames.
- **SQLAlchemy:** conexão entre Python e SQLite.

## Desenvolvimento

### 1. Preparação dos dados com SQL

A consulta foi estruturada utilizando Common Table Expressions (CTEs), por meio da cláusula `WITH`, para organizar o processamento em etapas.

Foram utilizadas diferentes tabelas e operações para consolidar as informações dos usuários.

Principais recursos SQL aplicados:

- CTEs (`WITH`);
- `JOIN` e `LEFT JOIN`;
- Funções de agregação (`COUNT`, `SUM` e `MIN`);
- Agrupamentos (`GROUP BY`);
- Expressões condicionais (`CASE WHEN`);
- Funções de janela (`ROW_NUMBER`);
- Tratamento de valores nulos (`COALESCE`);
- Funções de manipulação de datas (`JULIANDAY`, `DATETIME` e `STRFTIME`).

### 2. Construção dos atributos comportamentais

As métricas foram calculadas considerando diferentes janelas temporais: histórico completo, últimos 7, 14, 28 e 56 dias.

A consulta também identifica os produtos mais utilizados, os dias da semana e os períodos do dia com maior frequência de transações.

Ao final, as informações são consolidadas em uma única tabela, com uma linha por usuário para cada data de referência.

### 3. Integração entre SQL e Python

Foi desenvolvido um script Python para automatizar a execução da consulta SQL.

O processo utiliza SQLAlchemy para estabelecer a conexão com o banco SQLite e Pandas para carregar os resultados em DataFrames.

Foram definidas sete datas de referência, entre janeiro e julho de 2025. Para cada data, a consulta é executada e o resultado é inserido na tabela `feature_store_cliente`.

A inserção utiliza o modo `append`, permitindo armazenar os resultados de diferentes datas de referência na mesma tabela.

### 4. Indicador de engajamento

Foi criado um indicador para comparar a frequência de transações dos últimos 28 dias com a quantidade total de transações históricas.

Essa métrica permite observar a participação das atividades recentes em relação ao histórico de cada usuário.

## Estrutura do projeto

```text
analise-usuarios/
│
├── database.db
├── etl.py
├── etl.sql
├── README.md

```


## Próximas etapas

A tabela de atributos comportamentais construída neste projeto poderá servir como base para análises exploratórias e aplicações de Machine Learning, permitindo investigar padrões de comportamento e engajamento dos usuários.


