
- Ministers All Properties:

PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>
SELECT ?p ?propLabel ?eff ('' as ?notes)
WHERE {
{
    SELECT DISTINCT  ?p  (count(*) as ?eff)
    WHERE {
        ?item wdt:P31 wd:Q5; 
             wdt:P569 ?birthDate.
       ?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .
			?item ?p ?o.
        }
		GROUP BY ?p
    }

    ## we need this construct to get the label of the property
    ## properties are also entities in Wikidata,
    ## but only in the entities' namespace

    ?prop wikibase:directClaim ?p .
    ?prop rdfs:label ?propLabel.
    FILTER(LANG(?propLabel) = 'en')
    }  
ORDER BY DESC(?eff) 

- Ministers Occupation Labels:

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>
SELECT ?object ?objectLabel (COUNT(*) as ?eff)
WHERE
    {
    ### subquery adding the distinct clause
        {
        SELECT DISTINCT ?item
        WHERE {
        ?item wdt:P31 wd:Q5; 
              wdt:P569 ?birthDate.
        
            ?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .
            }
        } 
	
        ### The property P106 associates occupations to persons
        # we call here the target variable ?object 
        # in order to more easily reuse the query. 
        # ?occupation would be also a good name for the variable
        ?item wdt:P106 ?object.
        ?object rdfs:label ?objectLabel.
        FILTER(LANG(?objectLabel) = 'en')
}  
GROUP BY ?object ?objectLabel 
ORDER BY DESC(?eff)

- Ministers Place of Birth :

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>
SELECT ?object ?objectLabel (COUNT(*) as ?eff)
WHERE
    {
    ### subquery adding the distinct clause
        {
        SELECT DISTINCT ?item
        WHERE {
        ?item wdt:P31 wd:Q5; 
              wdt:P569 ?birthDate.
      
            ?item p:P39 ?statement .
    ?statement ps:P39 ?carica .
    ?carica wdt:P279* wd:Q3858501 . 
            }
        } 
	
        ### The property P106 associates occupations to persons
        # we call here the target variable ?object 
        # in order to more easily reuse the query. 
        # ?occupation would be also a good name for the variable
        ?item wdt:P19 ?object.
        ?object rdfs:label ?objectLabel.
        FILTER(LANG(?objectLabel) = 'en')
}  
GROUP BY ?object ?objectLabel 
ORDER BY DESC(?eff)

- Ministers Educated At :

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>
SELECT ?object ?objectLabel (COUNT(*) as ?eff)
WHERE
    {
    ### subquery adding the distinct clause
        {
        SELECT DISTINCT ?item
        WHERE {
        ?item wdt:P31 wd:Q5; 
              wdt:P569 ?birthDate.
      
           ?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 . 
            }
        } 
	
        ### The property P106 associates occupations to persons
        # we call here the target variable ?object 
        # in order to more easily reuse the query. 
        # ?occupation would be also a good name for the variable
        ?item wdt:P69 ?object.
        ?object rdfs:label ?objectLabel.
        FILTER(LANG(?objectLabel) = 'it')
}  
GROUP BY ?object ?objectLabel 
ORDER BY DESC(?eff)

- Ministers Position Held :

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>
SELECT ?object ?objectLabel (COUNT(*) as ?eff)
WHERE
    {
    ### subquery adding the distinct clause
        {
        SELECT DISTINCT ?item
        WHERE {
        ?item wdt:P31 wd:Q5; 
              wdt:P569 ?birthDate.
      
           ?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 . 
            }
        } 
	
        ### The property P106 associates occupations to persons
        # we call here the target variable ?object 
        # in order to more easily reuse the query. 
        # ?occupation would be also a good name for the variable
        ?item wdt:P39 ?object.
        ?object rdfs:label ?objectLabel.
        FILTER(LANG(?objectLabel) = 'it')
}  
GROUP BY ?object ?objectLabel 
ORDER BY DESC(?eff)