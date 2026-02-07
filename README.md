# DelayImpact Analytics

**Diagnóstico de atraso logístico e impacto na satisfação do cliente**

![Author](https://img.shields.io/badge/author-Jhonathan%20Domingues-lightgrey)
![Status](https://img.shields.io/badge/status-POC%20conclu%C3%ADda-success)
![License](https://img.shields.io/badge/license-MIT-blue)

![Python](https://img.shields.io/badge/python-3.12-blue?logo=python&logoColor=white)
![Data Engine](https://img.shields.io/badge/data%20engine-DuckDB-black?logo=duckdb&logoColor=white)
![Query](https://img.shields.io/badge/query-SQL-blue?logo=postgresql&logoColor=white)
![EDA](https://img.shields.io/badge/eda-diagnostic-informational)

![DelayImpact - Analytics](imagens/thumbnail.png)

---

## Visão Geral

Esta Proof of Concept (POC) tem como objetivo investigar, de forma analítica e orientada a negócio, **como atrasos logísticos impactam a satisfação do cliente em operações de e-commerce**.

A POC parte de dados operacionais, logísticos, financeiros e de experiência do cliente para construir uma base analítica confiável e realizar uma **análise diagnóstica**, focada em identificar padrões, pontos de inflexão e segmentos mais sensíveis ao atraso.

O foco não é previsão ou modelagem preditiva, mas **entendimento do problema e apoio à decisão**, respondendo à pergunta:

> *“Em que situações o atraso logístico passa a afetar significativamente a satisfação do cliente e onde agir primeiro?”*

---

## Problema de Negócio

A experiência de entrega é um dos principais determinantes da satisfação do cliente em e-commerce.  
Atrasos, mesmo de pequena duração, podem gerar frustração, avaliações negativas e impacto na percepção da marca.

No entanto, nem todo atraso tem o mesmo efeito.

Esta POC busca entender:

* como a satisfação varia conforme a intensidade do atraso
* se existem pontos críticos a partir dos quais a experiência se deteriora
* se o impacto do atraso é homogêneo ou varia por categoria e região
* onde esforços de melhoria logística tendem a gerar maior retorno

---

## Abordagem Analítica

A POC segue uma abordagem em camadas, simulando um pipeline analítico realista e reprodutível:

1. **Curadoria de Dados (Silver)**  
   Padronização, validação e criação de views intermediárias a partir do dataset original, garantindo consistência e confiabilidade.

2. **Camada Gold Analítica**  
   Consolidação de dados logísticos, financeiros e de satisfação em nível de pedido, com métricas e *features* analíticas voltadas para diagnóstico.

3. **Análise Exploratória Guiada (EDA)**  
   Análise estruturada e orientada por hipóteses, com foco em relações entre atraso, satisfação e comportamento do cliente.

4. **Síntese Analítica**  
   Organização dos principais achados em insights claros, voltados ao suporte à tomada de decisão.

---

## Relatório Executivo

Os principais achados desta POC foram consolidados em um **relatório executivo**, com foco em leitura gerencial e suporte à decisão.

[📄 **Acesse o relatório completo**](reports/executive_report.md)

O relatório apresenta:
- os impactos do atraso na satisfação do cliente
- o risco associado ao aumento de detratores
- diferenças regionais de sensibilidade ao atraso
- recomendações analíticas para priorização logística

---

## Dataset

* **Fonte:** Olist E-commerce Dataset (Kaggle)
* **Contexto:** Marketplace brasileiro de e-commerce
* **Período:** 2016–2018

O dataset é utilizado exclusivamente como **meio demonstrativo**, sendo adaptado para uma arquitetura analítica em camadas utilizando DuckDB.

---

### Ingestão de Dados

A ingestão e conversão dos dados brutos (CSV) para DuckDB foi realizada por meio de um script dedicado, mantido no repositório como **referência técnica e evidência de reprodutibilidade**.

O banco DuckDB versionado é considerado a **fonte oficial de dados** para esta POC.

---

## Estrutura do Projeto

```text
delayimpact-analytics/
│
├── data/
│   ├── raw/
│   │   └── olist.zip
│   └── processed/
│       └── olist.duckdb
├── imagens/
│   ├── detractors_by_state.png
│   ├── detractors_vs_delay_bucket.png
│   ├── score_vs_delay_bucket.png
│   └── thumbnail.png
├── notebooks/
│   ├── 01_curadoria_sql.ipynb
│   ├── 02_gold_delay_satisfaction.ipynb
│   └── 03_eda_delay_satisfaction.ipynb
├── reports/
│   └── executive_summary.md
├── scripts/
│   └── ingest_olist_to_duckdb.py
├── src/
│   └── paths.py
├── requirements.txt
└── README.md
```
---

## Como executar

### Ambiente virtual

```
bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```
---

## Camada Gold — `gold_delay_satisfaction`

A camada Gold consolida informações em **nível de pedido**, servindo como base única para a análise exploratória.

### Conteúdo principal

* métricas logísticas (tempo de entrega, atraso, status)
* métricas financeiras (GMV, frete, pagamentos)
* dados do cliente (UF, cidade)
* categoria principal do pedido
* avaliações do cliente (nota, presença de comentário)

### *Features* analíticas derivadas

* buckets de atraso
* flags de atraso
* grupos de satisfação (NPS simplificado)
* indicadores auxiliares para análise estatística

### Características

* foco analítico
* estrutura pensada para consumo em pandas
* sem lógica interpretativa embutida
* base única para EDA e diagnóstico

---

## Tecnologias Utilizadas

* Python
* SQL
* DuckDB
* Análise Exploratória de Dados (EDA)
* Análise Estatística
* Visualização de Dados

---

## Decisões de Design

* grão único: 1 linha por pedido
* curadoria centralizada em SQL
* separação explícita entre organização dos dados e análise
* foco em diagnóstico, não em dashboards
* comunicação orientada a decisão, não a exploração livre

---

## Status

POC concluída - Dados curados, camada Gold analítica construída, análise exploratória guiada finalizada e relatório executivo disponível.

---

## Licença

Este projeto está licenciado sob os termos da **MIT License**.  
Consulte o arquivo `LICENSE` para mais detalhes.

---
## Disclaimer

Este projeto é uma **Proof of Concept (POC)** desenvolvida com o objetivo de **demonstrar capacidade técnica e visão analítica aplicada a problemas reais de negócio**, utilizando ferramentas, métodos e práticas comuns em ambientes profissionais de dados.

As análises, visualizações, conclusões e recomendações apresentadas têm caráter **demonstrativo** e **não devem ser interpretadas como direcionamento operacional real**, nem como base direta para tomada de decisão em ambiente produtivo.

Esta POC**não foi desenvolvida para uso em produção.**

---

## Onde me encontrar

[![Website](https://img.shields.io/badge/🌐%20Website-Portfólio-black)](https://jhonathan.me)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Perfil-blue?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/jhonathandomingues)
[![Email](https://img.shields.io/badge/Email-Contato-success?logo=minutemailer&logoColor=white)](mailto:hello@jhonathan.me)