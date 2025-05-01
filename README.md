# projeto_2_spotify
Nesse projeto utilizei as ferramentas Big Query, Power BI e Google Colab para viabilizar a validação (refurtar/confirmar) de hipóteses levantas pelo cliente. Esse projeto corresponde a minha participação no Bootcamp da Laboratória Brasil. 

# PROJETO 2 - Spotify

## ✔ Ficha Técnica: Projeto de Análise de Dados

---

## 📰 Título do Projeto: **Spotify - Hipóteses**

---

### 🎯 Objetivo:
Realizar o pré-processamento, análise e validação (confirmar ou refutar) das hipóteses levantadas pela gravadora através da análise de dados. Com esse estudo, será possível indicar ações estratégicas adequadas diante das questões levantadas e aplicar os direcionamentos mais assertivos para o alcance de resultados mais satisfatórios junto ao público.

---

### 👩🏽‍🦱 Equipe:
O projeto foi feito em dupla, mas as etapas aqui relacionadas foram realizadas **individualmente**.

---

### ⚙ Ferramentas e Tecnologias:

- BigQuery  
- Power BI  
- Google Colab  
- Python  
- SQL  

---

### 💻 Processamento e Análises:

#### 1. HIPÓTESES levantadas:

1. Músicas com BPM (Batidas Por Minuto) mais altos fazem mais sucesso em número de streams no Spotify;
2. As músicas mais populares no Spotify também têm desempenho semelhante em outras plataformas (como Deezer);
3. A presença de uma música em mais playlists está correlacionada com mais streams;
4. Artistas com mais músicas no Spotify têm mais streams;
5. As características da música influenciam o sucesso em streams no Spotify.

#### 2. Importação e TRATAMENTO do *dataset*:

- `track_in_competition`: posicionamento do Spotify diante de outras plataformas;  
- `track_in_spotify`: identificação, autor, lançamento, streams etc.;  
- `track_technical_info`: características da música (energia, batidas, positividade etc.);

#### 3. Contexto:

- Dados do ano de 2023, com músicas de diversos períodos;  
- Pré-processamento incluiu limpeza de nulos, duplicados, fora do escopo, discrepantes, criação de variáveis complementares;  
- **BigQuery** e **Power BI** foram usados para análise inicial;  
- Análise exploratória com **histograma**:

![HISTOGRAMA.png](attachment:0791cb5f-2c7b-4c6c-86fd-543fd6497125:HISTOGRAMA.png)

**1ª Observação**: a maioria dos conteúdos tem desempenho entre 50 mil e 150 mil streams. Há poucos casos de muito sucesso. A distribuição é levemente assimétrica.

---

### 📊 Correlação no BigQuery:

| Hipótese | Variáveis | Correlação |
|----------|-----------|------------|
| 1 | bpm / streams_limpo | -0.0024 |
| 2 | in_spotify_charts / in_deezer_charts | 0.6002 |
| 3 | streams_limpo / in_spotify_playlists | 0.7898 |
| 4 | qtd_musicas / total_streams | 0.7809 ⚠️ Refutado pelo Python |
| 5 | múltiplas variáveis / streams_limpo |  
- bpm: -0.0024  
- danceability: -0.1054  
- valence: -0.0408  
- energy: -0.0260  
- acousticness: -0.0044  
- instrumentalness: -0.0449  
- liveness: -0.0483  
- speechiness: -0.1123  

---

### 🧪 Testes de Significância (Python):

| Hipótese | Spearman | p-valor | Resultado |
|----------|----------|---------|-----------|
| 1 | -0.0102 | 0.7520 | Refutada |
| 2 | 0.5889 | 4.86e-90 | Confirmada |
| 3 | 0.0187 | 0.5637 | Refutada |
| 4 | -0.0068 | 0.8328 | Refutada |
| 5 | Resultados variados, mas fraca explicação da variância |

---

### 📉 Regressão Linear (Marco Adicional):

**Hipótese 1**: BPM não é um bom preditor isolado de sucesso.  
**Hipótese 2**: Sucesso no Spotify tende a refletir no Deezer (correlação moderada).  
**Hipótese 3**: Inclusão em playlists impacta fortemente o número de streams.  
**Hipótese 4**: Apesar de parecer haver correlação, a significância estatística refuta isso.  
**Hipótese 5**: Características técnicas explicam pouco da variação de streams (apenas 2,9%).

---

### 📋 Quadro Resumo:

| Hipótese | BigQuery | Power BI | Teste Significância (Python) | Regressão Linear |
|----------|----------|----------|------------------------------|------------------|
| 1 | Não confirmada | Não confirmada | Não confirmada | Não confirmada |
| 2 | Confirmada | Confirmada | Confirmada | Confirmada |
| 3 | Confirmada | Confirmada | Não confirmada | Confirmada |
| 4 | Confirmada ⚠️ Refutada | Não confirmada | Não confirmada | Não confirmada |
| 5 | Não confirmada | * | * | Não confirmada |

---

### 📑 Resultados e Conclusões:

1. Apenas as **hipóteses 2 e 3** foram confirmadas.
2. **Hipótese 2**: sucesso em uma plataforma tende a refletir em outra — levanta questões sobre fidelidade à plataforma.
3. **Hipótese 3**: presença em playlists amplia a visibilidade — comparável à lógica de redes sociais.
4. A principal estratégia é a **promoção estratégica do artista** para criar comunidade e engajamento.
5. A música está acessível a todos. O diferencial está em **construir redes autênticas**.

#### Exemplos de estratégias autênticas:

- Constância com propósito (valores, estilo de vida);  
- “Acessibilidade” do artista (interações diretas via redes sociais).

#### Hipóteses Refutadas:

- **Hipótese 1**: BPM não é determinante no sucesso de uma faixa.
- **Hipótese 4**: Ter mais músicas não garante mais streams — sucesso pode vir de poucos hits.
- **Hipótese 5**: Características técnicas têm pouca influência isolada. Fatores externos (popularidade, divulgação, playlists) são mais relevantes.

---

### 🔐 Limitações / Próximos Passos:

1. Exclusão de dados pode enviesar resultados;
2. Correlação não implica causalidade — outras variáveis podem estar por trás dos padrões;
3. Testes adicionais exigem mais trabalho e dados;
4. É necessário considerar **terceiras ou quartas variáveis** além das diretamente analisadas.

---

### 🔗 Links de Interesse:

- **Power BI**: [Ver Link](https://drive.google.com/file/d/1pQrrQoZ0svMfihc0xdB5V0RK4Db6k_St/view?usp=sharing)  
- **BigQuery (Correlações)**: [Ver Link](https://console.cloud.google.com/bigquery?sq=401192978632:697703941d0345c29ccf107a45d39d13)  
- **Google Colab (Teste de Significância)**: [Ver Link](https://colab.research.google.com/drive/1XLzgvzh0SO7Mvn0XJlapnwa7UW3j7ya0?usp=sharing)  
- **Google Colab (Marco Adicional)**: [Ver Link](https://colab.research.google.com/drive/1G0ZyA8T4G7JbCJwy7Xuiuv5Gu8SyuPV_?usp=sharing)  
- **Documentação**: [Ver Link](https://docs.google.com/document/d/1zXoxDQBZqJE0NengCMKP9SHTcl3ToW3UjcRQ78qkkT4/edit?usp=sharing)

