- Basic Properties :

PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>


SELECT DISTINCT ?item  ?gender ?year ?itemLabel ?p ?propLabel 
        WHERE {

        ## note the service address          
        SERVICE <https://query.wikidata.org/sparql>
            {
            {?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .}  
              
        
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                wdt:P569 ?birthDate; # It must necessarily have a birth date property
                wdt:P21 ?gender. # It must necessarily have a gender property
        BIND(year(?birthDate) as ?year)
        
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
        }
        }
        LIMIT 1000

- Inspecting Triplets :

PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>


CONSTRUCT 
        {
           ?item wdt:P21 ?gender.
           ?item  wdt:P569 ?year.
           ?item rdfs:label ?itemLabel.
           # ?item  wdt:P31 wd:Q5.
           # Noter qu'on modifie pour disposer de la propriété standard
           # afin de déclarer l'appartenance d'une instance à une classe
           ?item  rdf:type wd:Q5. }
      
        WHERE {

        ## note the service address          
        SERVICE <https://query.wikidata.org/sparql>
            {
            {?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .}    
        
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                wdt:P569 ?birthDate; # It must necessarily have a birth date property
                wdt:P21 ?gender. # It must necessarily have a gender property
        BIND(year(?birthDate) as ?year)
       
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
        LIMIT 5

        - Dedicated Graph (?) :

        <https://tegrich.github.io/italy_ministers/graphs-defs.html#wikidata>
  