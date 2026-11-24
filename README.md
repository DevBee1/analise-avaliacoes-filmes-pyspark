# Análise de avaliações de filmes com PySpark

Projeto acadêmico de Big Data (UNINTER) que usa o modelo **MapReduce** com PySpark para analisar o dataset `imdb-reviews-pt-br` (avaliações de filmes em português e inglês).

## Problema
Processar um volume grande de avaliações de filmes sem usar pandas, apenas com RDDs do PySpark, para responder a duas perguntas:

1. Qual é a soma dos `id` das avaliações classificadas como **negativas**?
2. Nos textos **negativos**, quantas palavras a mais existem em português do que em inglês?

## O que fiz
- Criei a SparkSession e li o CSV em um DataFrame do Spark.
- **Questão 1:** `map` transforma cada linha em `(sentiment, id)` e `reduceByKey` soma os IDs por sentimento.
- **Questão 2:** `map` transforma cada linha em `(sentiment, (palavras_en, palavras_pt))` e `reduceByKey` soma as contagens por sentimento. A diferença é calculada para as avaliações negativas.

## Resultados
| Pergunta | Resultado |
|---|---|
| Soma dos IDs negativos | 459.568.555 |
| Palavras EN (negativas) | 5.400.324 |
| Palavras PT (negativas) | 5.455.273 |
| Diferença PT - EN | 54.949 |

## Tecnologias
Python, PySpark, Google Colab

## Como rodar
1. Abra `analise_avaliacoes_pyspark.ipynb` no [Google Colab](https://colab.research.google.com/).
2. Execute as células em ordem (a primeira baixa o dataset).

## Aprendizados
- `map` transforma cada registro em um par chave-valor, e `reduceByKey` combina os valores da mesma chave, dois a dois.
- Esse modelo permite processar muitos dados de forma distribuída, em vez de percorrer tudo em um único laço.
