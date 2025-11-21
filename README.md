# dio-neo4j
CineGraph Analytics: Modelagem de Dados Orientada a Grafos

# 🎬 CineGraph: Modelagem de dados de Entretenimento

![Badge Status](https://img.shields.io/badge/Status-Completed-success)
![Badge Tech](https://img.shields.io/badge/Tech-Neo4j%20%7C%20Cypher%20%7C%20NoSQL-blue)
![Badge License](https://img.shields.io/badge/License-MIT-green)

> Uma abordagem baseada em grafos para modelagem de dados de streaming, focada em performance de relacionamento e sistemas de recomendação.

---

## 📑 Sobre o Projeto

O **CineGraph** é um projeto de estudo desenvolvido para explorar a potência dos **Bancos de Dados Orientados a Grafos**. O objetivo central é modelar as interações complexas entre usuários e catálogos de mídia (Filmes e Séries), superando as limitações de JOINs custosos encontrados em modelos relacionais tradicionais.

Esta arquitetura permite responder perguntas complexas com facilidade, como:
* *"Quais usuários assistiram aos mesmos filmes que eu e o que mais eles gostam?"*
* *"Qual a influência de um estúdio específico em um gênero ao longo das décadas?"*

---

## 🧩 O Modelo de Dados (Schema)

A modelagem foi desenhada para centralizar as obras (Movies/Series) como nós conectores ("hubs"), orbitados por suas propriedades e interações.

### 📷 Visualização do Grafo

![Modelagem do Grafo](modelagem_grafo.jpg)
*(O diagrama acima ilustra os nós e relacionamentos implementados neste projeto)*

### 📌 Entidades (Nós)
O grafo é composto pelos seguintes nós principais:

| Nó | Descrição |
| :--- | :--- |
| **`User`** | Representa o consumidor do conteúdo na plataforma. |
| **`Movie` / `Series`** | As obras principais consumidas. |
| **`Actor`** | Artistas que participaram do elenco. |
| **`Director`** | Responsáveis pela direção da obra. |
| **`Studio`** | Estúdio produtor ou detentor dos direitos. |
| **`Genre`** | Categoria temática (Ação, Drama, Sci-Fi, etc.). |
| **`Ano de Lançamento`** | Nó temporal para análises cronológicas. |

### 🔗 Relacionamentos (Edges)
As arestas definem a semântica das conexões:

- **`(:User)-[:WATCHED]->(:Movie|:Series)`**: Histórico de visualização.
- **`(:Actor)-[:ACTED_IN]->(:Movie|:Series)`**: Participação no elenco.
- **`(:Director)-[:DIRECTED]->(:Movie|:Series)`**: Autoria/Direção da obra.
- **`(:Movie|:Series)-[:BELONGS_TO]->(:Studio)`**: Propriedade intelectual.
- **`(:Movie|:Series)-[:IN_GENRE]->(:Genre)`**: Classificação.
- **`(:Movie|:Series)-[:RELEASED_IN]->(:Year)`**: Conexão temporal.

---

## 🚀 Tecnologias Utilizadas

* **Neo4j Database**: Motor de banco de dados gráfico.
* **Cypher Query Language (CQL)**: Para criação e consulta dos dados.
* **Ferramenta de Modelagem**: Arrows.app.

---

## 🧠 Código gerado para criação dos grafos e relacionamentos (Cypher)

CREATE (genre)<-[:IN_GENRE]-(series)<-[:WATCHED]-()-[:WATCHED]->(movie)-[:IN_GENRE]->(genre),
(`director `)-[:ACTED_IN]->(series)<-[:ACTED_IN]-()-[:ACTED_IN]->(movie)<-[:ACTED_IN]-(`director `),
(`ano de lançamento `)<-[:_RELATED]-(estudio)<-[:BELONGS_TO]-(series)<-[:DATE]-(`ano de lançamento `)-[:DATE]->(movie)-[:BELONGS_TO]->(estudio)

