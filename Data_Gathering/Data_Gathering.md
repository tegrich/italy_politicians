Data's Gathering:

- List of Prime Ministers:

PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
SELECT ?item ?itemLabel
WHERE {
?item wdt:P31 wd:Q5;
      wdt:P39 wd:Q796897.
?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'en')

 }

- Party's Origin of Prime Ministers in cronological order:

SELECT DISTINCT ?premier ?premierLabel ?partitoLabel ?inizio ?fine
WHERE {
  ?premier p:P39 ?statement .
  ?statement ps:P39 wd:Q796897 .
  OPTIONAL { ?statement pq:P580 ?inizio . }
  OPTIONAL { ?statement pq:P582 ?fine . }
  OPTIONAL { ?premier wdt:P102 ?partito . }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "it". }
}
ORDER BY ?inizio
  
- Total of ministers and their birth gender, organized in cronological order by governement:

SELECT DISTINCT ?item ?itemLabel ?genderLabel ?caricaLabel ?inizio
WHERE {
  ?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .
  ?statement pq:P580 ?inizio .
  ?item wdt:P21 ?gender .
  SERVICE wikibase:label { 
    bd:serviceParam wikibase:language "it,en". 
    ?item rdfs:label ?itemLabel .
    ?gender rdfs:label ?genderLabel .
    ?carica rdfs:label ?caricaLabel .
  }
}
ORDER BY ?inizio

- Total of ministers and their party's origin in cronological order:

SELECT DISTINCT ?item ?itemLabel ?partitoLabel ?caricaLabel ?inizio 
WHERE {
  ?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .
  ?statement pq:P580 ?inizio .
  OPTIONAL { ?item wdt:P102 ?partito . }
  
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],it,en". }
}
ORDER BY ?inizio

- Total of ministers and their birth's region in cronological order:

SELECT DISTINCT ?item ?itemLabel ?caricaLabel ?inizio ?regioneLabel
WHERE {
  ?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 . 
  ?statement pq:P580 ?inizio .
  ?item wdt:P19 ?luogoNascita .
  ?luogoNascita wdt:P131* ?regione .
  ?regione wdt:P31 wd:Q16110 .

  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],it,en". }
}
ORDER BY ?inizio