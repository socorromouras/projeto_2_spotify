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

  a. Músicas com BPM (Batidas Por Minuto) mais altos fazem mais sucesso em termos de número de streams no Spotify;  
  b. As músicas mais populares no ranking do Spotify também possuem um comportamento semelhante em outras plataformas, como a Deezer;  
  c. A presença de uma música em um maior número de playlists está correlacionada com um maior número de streams;  
  d. Artistas com um maior número de músicas no Spotify têm mais streams;  
  e. As características da música influenciam o sucesso em termos de número de streams no Spotify.

#### 2. Importação e TRATAMENTO do *dataset* disponibilizado:

- `track_in_competition`:traz posicionamento do Spotify diantes de outros streams;  
- `track_in_spotify`: tabela composta pela identificação dentre outras características o autor da música, período de lançamento, streams e etc.;  
- `track_technical_info`: traz informações relativas as características de cada música, com energia, batidas, performance ao vivo, palavras faladas, positividade;entre outros;

#### 3. Contexto:

- As tabelas correspondem ao ano de 2023 com músicas lançadas nas mais diversas épocas, mas que são consumidas e repercutem até os dias atuais;
- Na fase do pré-processamento, que inclui organização e limpeza dos dados, foram aplicado o tratamento de dados nulos, duplicados, fora do escopo, discrepantes, assim como criadas 
  novas variáveis que complementassem as análises;
- No processo descrito anteriormente, o **BigQuery** e **Power BI**, foram essenciais para os primeiros passos no exame das tabelas;
- Também foram necessário um primeiro reconhecimento através do **HISTOGRAMA:**

![HISTOGRAMA.png](attachment:0791cb5f-2c7b-4c6c-86fd-543fd6497125:HISTOGRAMA.png)

**1ª Observação**: maior parte dos conteúdos analisados têm desempenho mediano, entre 50 mil e 150 mil streams. Há poucos casos de grande sucesso, mas eles existem. A distribuição é levemente assimétrica, típica de dados em que popularidade não é igualmente distribuída (normal para música, vídeos etc);

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

1. **Hipótese 1:**
    1. (Spearman): -0.010248769009473531
    2. p-valor: 0.7520179059448279
2. **Hipótese 2:**
    1. (Spearman): 0.5889212257714336
    2. p-valor: 4.868132172329094e-90
3. **Hipótese 3:**
    1. (Spearman): 0.018724496096824243
    2. p-valor: 0.5637163900482092
4. **Hipótese 4:** 
    1. (Spearman): -0.006847079025223792
    2. p-valor: 0.8328098894273368
    3. ⚠️ **>>> Refuta a correlação do Big Query**
5. **Hipótese 5:**
    Hipótese 5:Resultados variados, mas fraca explicação da variância |

---

### 📉 Regressão Linear (Marco Adicional):
No MARCO ADICIONAL, com a Regressão Linear e em um caso específico (hipótese 5) com Regressão múltipla, temos as seguintes conclusões:

1. **Hipótese 1 -** Não podemos concluir que músicas com BPM mais alto realmente fazem mais sucesso no Spotify com base nesses dados. Pode ser que outros fatores estejam influenciando mais o número de streams, ou talvez o BPM não seja uma variável tão importante;
2. **Hipótese 2 -** De forma geral, quando uma música é popular no Spotify, ela tende a ser popular também no Deezer, mas não é uma relação perfeita. A força da correlação é moderada, o que significa que não é 100% certo que as músicas populares no Spotify estarão necessariamente populares no Deezer;
3. **Hipótese 3 -** A hipótese parece ser bem sustentada pelos dados, já que o coeficiente de correlação é bastante alto. Isso indica que, de fato, a inclusão de uma música em playlists populares tende a ter um impacto significativo no número de vezes que ela é ouvida no Spotify;
4. **Hipótese 4  -** A regressão linear pode ter um coeficiente de 0.7809, indicando que, com a quantidade de músicas, há uma forte tendência de aumento no número de streams. Porém, a correlação de **Pearson de -0.0068** indica que **não há uma relação forte ou significativa** entre as duas variáveis (pelo menos do ponto de vista da correlação simples);
5. **Hipótese 5 -** A análise mostra que a popularidade de uma música é mais influenciada por sua presença em playlists e por estratégias de publicação (como volume de lançamentos) do que por características técnicas isoladas;

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

1. Foram feitos testes com as técnicas indicadas no escopo do projeto, e assim, cruzando os resultados, pode-se afirmar que apenas as **hipóteses 2 e 3** estão **confirmadas**;
2. Na **hipótese 2**, a música que faz sucesso no Spotify poderá também fazer sucesso no Deezer, por exemplo, porém essa confirmação traz a tona um novo questionamento: se as músicas tendem a ter o mesmo desempenho, *porque o consumidor final opta por um streaming e não por outro?*
3. Há na **hipótese 3**, a inclusão em mais playlists trazem mais possibilidades de reprodução, ou seja, quanto mais exposição, mais visibilidade. Em uma breve **analogia**, uma estratégia que se assemelha as táticas já absorvidas pelo público em geral, quando se trata de redes sociais, em que a **presença constante**, “o se fazer lembrado”, gera algum tipo de retorno;
4. Cruzando as duas informações, depreende-se que a preocupação primordial é na **promoção estratégica do artista**, para que isso reverbere na procura por suas músicas. O porque desse caminho? É necessário a formação de uma comunidade em torno do artista para que se gere a real conexão e assim o desejado aumento de consumo de suas músicas, porque afinal…
5. …música já existe em uma enorme quantidade e de fácil acesso. E então, *o que me diferencia nessa corrida?* A construção de **redes mais autênticas**!  
6.  Exemplos de posicionamentos que podem **construir/reforçar** essa ideia de autenticidade:
    a. A constância com **propósito**, ou seja, a exposição de forma calculada, com reforço de  valores, lifestyle  etc;
    b. Uma pretensa “acessibilidade”, como já fazem algumas celebridades, ao se colocar em **contato** mais direto com o público, como em DM’s ou X (antigo Twitter);
7. Quanto as hipóteses **refutadas**, segue:
    1. **Número 1**: o Bpm, ou batidas por minuto, pode ser um dado interessante em tempos de audios e vídeos acelerados, mas ainda não explica diretamente o que vai fazer uma música “hitar” ou mesmo o retorno de artistas antigos, ainda que com sons adaptados, e que voltam a fazer sucesso e se conectam com os públicos contemporâneos;
    2. **Número 4:** algo perceptível a “olho nu” e confirmado pelos dados: existem streams superiores a 2 bilhões e até 3 bilhões, mas não necessariamente com um número alto de músicas. Isso corrobora com a possibilidade de que a popularidade pode estar mais ligada à performance de uma ou poucas faixas de destaque, não à quantidade;
    3. **Número 5:** a análise de regressão linear múltipla indicou que as características técnicas das músicas explicam apenas 2,9% da variação no número de streams no Spotify, sugerindo uma influência limitada. 
        1. Algumas variáveis, como danceabilidade e speechiness, mostraram impacto estatisticamente significativo, porém com efeito negativo, o que pode indicar uma preferência do público por músicas **menos faladas** e **menos dançantes** em certos contextos. 
        2. No entanto, a baixa capacidade explicativa do modelo aponta que fatores externos às características sonoras — como a popularidade do artista, **estratégias de divulgação** e **presença em playlists** — provavelmente exercem um papel mais determinante no sucesso das faixas.

### **🔐Limitações/Próximos Passos**: limitações ou desafios encontrados durante o projeto. 

1. A tratativa do banco de dados é delicada, uma vez que a **exclusão** de dados podem gerar informações enviesadas;
2. A Correlação não implica necessariamente causalidade, pois o fato de se moverem juntas, não significa necessariamente que uma influencia na outra. As variáveis podem ter **um ponto em comum** que afeta o seu comportamento. E a depender do tamanho da amostra, também pode apresentar uma relação fraca ou forte somente por um acaso;
3. Assim, a comprovação por **outras técnicas** se faz necessário, gerando um maior trabalho e um volume grande de informações para serem tabuladas e compreendidas;
4. Por isso, é muito importante realizar análises que ultrapassem a simples explicação das variáveis estabelecidas, trazendo nas argumentações, os questionamentos sobre **terceiras ou quartas** variáveis que podem ser encaixadas nas deduções.

---
  
### 🔗 Links de Interesse:
- Ambiente - Power BI - [**LINK**](https://drive.google.com/file/d/1pQrrQoZ0svMfihc0xdB5V0RK4Db6k_St/view?usp=sharing)
- Ambiente - Big Query - (Correlações) -  [LINK](https://console.cloud.google.com/bigquery?sq=401192978632:697703941d0345c29ccf107a45d39d13)
- Ambiente - Colab (T. Significância) - [**LINK**](https://colab.research.google.com/drive/1XLzgvzh0SO7Mvn0XJlapnwa7UW3j7ya0?usp=sharing)
- Ambiente - Colab (Marco Adicional) - [**LINK**](https://colab.research.google.com/drive/1G0ZyA8T4G7JbCJwy7Xuiuv5Gu8SyuPV_?usp=sharing)
- Documentação - [**LINK**](https://docs.google.com/document/d/1zXoxDQBZqJE0NengCMKP9SHTcl3ToW3UjcRQ78qkkT4/edit?usp=sharing)

