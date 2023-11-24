# Linking Parts
Project for Semantic Web course at FCFM.

## Colab
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/iPolarisu/linking-data/blob/main/steam_games_keyword_linker.ipynb)

## SPARQL Queries
You can query the generated TTL file at the [course's virtuoso service](https://cc7220.dcc.uchile.cl:8900/sparql).

```sparql
# Q1
PREFIX rdf:     <http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
PREFIX rdfs:    <http://www.w3.org/2000/01/rdf-schema#> 
PREFIX : <http://ex.org/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?game1Label ?game2Label (COUNT(?keyphrase) as ?keyphraseCount)
FROM <https://grupo1.cl>
WHERE {
   ?game1 :hasKP ?keyphrase .
   ?game2 :hasKP ?keyphrase .
   FILTER(?game1 != ?game2)
   ?game1 rdfs:label ?game1Label .
   ?game2 rdfs:label ?game2Label .
   FILTER(?game1Label < ?game2Label)
}
GROUP BY ?game1Label ?game2Label
ORDER BY DESC (?keyphraseCount)
```

```sparql
#Q2
PREFIX rdf:     <http://www.w3.org/1999/02/22-rdf-syntax-ns#> 
PREFIX rdfs:    <http://www.w3.org/2000/01/rdf-schema#> 
PREFIX : <http://ex.org/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?dev1 ?dev2 (COUNT(?keyphrase) as ?keyphraseCount)
FROM <https://grupo1.cl>
WHERE {
   ?game1 :hasKP ?keyphrase; :dev ?dev1 .
   ?game2 :hasKP ?keyphrase; :dev ?dev2 .
   FILTER(?dev1 != ?dev2)
}
GROUP BY ?dev1 ?dev2
ORDER BY DESC (?keyphraseCount)
```

## Attribution
The Steam Store Games (Clean dataset) was created by Nik Davis, you can check [kaggle](https://www.kaggle.com/datasets/nikdavis/steam-store-games/) for more information. It uses the following [license]( https://creativecommons.org/licenses/by/4.0/).
