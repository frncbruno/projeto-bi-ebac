# 🎬 PIXIES Ltda — Dashboard de Análise de Bilheteria (Projeto fictício para certificado de curso de Power BI na plataforma de ensino EBAC)

Dashboard desenvolvido no **Power BI** para identificar os principais fatores que influenciam o sucesso de bilheteria no setor cinematográfico.

---

## 📌 Objetivo

Responder perguntas estratégicas para a diretoria:

- Quais gêneros têm maior retorno?
- Quais países apresentam melhor desempenho?
- Quais produtoras têm maior sucesso?
- Existem filmes de baixo orçamento com alta bilheteria?

---

## 🗂️ Estrutura dos Dados

O modelo é composto por três tabelas relacionadas:

**Filmes** — tabela fato central
| Coluna | Descrição |
|---|---|
| titulo | Nome do filme |
| genero | Gênero cinematográfico |
| ano_lancamento | Ano de lançamento |
| rating_imdb | Nota no IMDb |
| orcamento_dolares | Orçamento em dólares |
| bilheteria | Receita de bilheteria |
| ID_Produtora | Chave estrangeira |
| ID_País | Chave estrangeira |

**Produtoras** — dimensão
| Coluna | Descrição |
|---|---|
| ID_Produtora | Chave primária |
| nome | Nome da produtora |
| pais_origem | País de origem |
| ano_fundacao | Ano de fundação |

**Países** — dimensão
| Coluna | Descrição |
|---|---|
| ID_País | Chave primária |
| nome_pais | Nome do país |
| continente | Continente |
| idioma | Idioma oficial |
| moeda | Moeda local |
| capital | Capital |

---

## 🔗 Relacionamentos

```
Filmes (N) ──── (1) Produtoras
Filmes (N) ──── (1) Países
```

Cardinalidade Muitos para Um (*:1), filtro unidirecional.

---

## 📐 Medidas DAX

```dax
Bilheteria Total = SUM(Filmes[bilheteria])

Orçamento Total = SUM(Filmes[orcamento_dolares])

Lucro Total = [Bilheteria Total] - [Orçamento Total]

ROI = DIVIDE([Bilheteria Total] - [Orçamento Total], [Orçamento Total], 0)

Bilheteria Média = AVERAGE(Filmes[bilheteria])

Qtd Filmes = COUNTROWS(Filmes)

Quantidade de Países = DISTINCTCOUNT(Países[nome_pais])
```

> Todas as métricas foram implementadas como **medidas DAX**, evitando colunas calculadas para melhor performance do modelo.

---

## 📊 Visualizações

| Visual | Descrição |
|---|---|
| Cartões KPI | Bilheteria Total, Bilheteria Média, ROI, Qtd Filmes, Qtd Países |
| Barras horizontais | Bilheteria Total por Gênero |
| Colunas | Bilheteria Total por Produtora (Top 10) |
| Barras horizontais | Bilheteria Total por País |
| Gráfico de Dispersão | Orçamento x Bilheteria por Filme (com tamanho = Lucro Total) |
| Barras | Rating IMDb por Gênero |
| Tabela detalhada | Página 2 com todos os filmes e métricas |

---

## 🔎 Segmentadores (Slicers)

- **País** — dropdown
- **Gênero** — dropdown
- **Data de Lançamento** — controle deslizante (range)

Todos os slicers afetam todas as visualizações simultaneamente via relacionamentos do modelo.

---

## 💡 Processo e Principais Insights

📊 O que foi feito:
→ Modelagem de dados com 3 tabelas relacionadas (Filmes, Produtoras e Países)
→ Data cleaning
→ Medidas em DAX: Bilheteria Total, ROI, Lucro Total e Bilheteria Média
→ Gráfico de dispersão para identificar filmes de baixo orçamento com alta bilheteria
→ KPIs, segmentadores interativos e 2 páginas de visualização
→ Zero colunas calculadas — tudo resolvido com medidas para melhor performance

- **Action** é o gênero com maior bilheteria total, seguido de Animation e Adventure
- **Estados Unidos** domina em volume absoluto de bilheteria
- **Marvel Studios** lidera entre as produtoras com ampla margem
- Filmes como **City of God** (orçamento de $3,3M) demonstram alto retorno proporcional, aparecendo no quadrante de baixo orçamento / alta bilheteria no scatter chart

---

## 📊 Dashboard

<img width="1150" height="641" alt="dash1" src="https://github.com/user-attachments/assets/391439d0-a1c8-4d36-b065-9a6f39d58f0c" />

<img width="1152" height="646" alt="dash2" src="https://github.com/user-attachments/assets/18c8bc15-cd30-4cd2-983a-d79eee7a78e6" />

---

## 🛠️ Tecnologias

- Power BI Desktop
- DAX (Data Analysis Expressions)
- Power Query (M)
- Figma

---

## 👨‍💻 Autor

**Bruno Tubino Franco**  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-blue?style=flat&logo=linkedin)](https://linkedin.com/in/brunotubino)
