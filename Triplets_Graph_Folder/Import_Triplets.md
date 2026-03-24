- Ministers Number :    

PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>

SELECT (count(*) as ?effectif)
WHERE {

        ## note the service address  
        SERVICE <https://query.wikidata.org/sparql>
            {
           {?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .}  
  
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                wdt:P569 ?birthDate; # It must necessarily have a birth date property
  
       BIND(year(?birthDate) as ?year)


        
  
        OPTIONAL {
            # The item can have or not a gender property
            ?item wdt:P21 ?gender.
        }
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }

- Ministers Occupation: 

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
           ?item wdt:P106 ?occupation.
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
                wdt:P106 ?occupation; # It must necessarily have a birth date property
                
        BIND(year(?birthDate) as ?year)
       
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
        LIMIT 10000

- Occupation Graph:
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>


INSERT {

        ### Note that the data is imported into a named graph and not the DEFAULT one
        GRAPH <https://tegrich.github.io/italy_ministers/graphs-defs.html#wikidata>
             {?item  wdt:106 ?occupation. 
           ?item rdfs:label ?itemLabel.           # ?item  wdt:P31 wd:Q5.
           # modifier pour disposer de la propriété standard
           ?item  rdf:type wd:Q5.
           }
}
  
        WHERE {
  
  			SELECT DISTINCT ?item ?year ?gender ?itemLabel ?p ?occupation
  
  			WHERE {

        ## note the service address  
        SERVICE <https://query.wikidata.org/sparql>
           {
            {?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .}  
  
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                  wdt:P106 ?occupation. # It must necessarily have a birth date property



        BIND(year(?birthDate) as ?year)
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
    ORDER BY ?item 
    OFFSET 0
    LIMIT 10000 

- Ministers Position Held:

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
           ?item wdt:P39 ?position.
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
                wdt:P39 ?position; # It must necessarily have a birth date property
                
        BIND(year(?birthDate) as ?year)
       
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
        LIMIT 10000

- Position Held Graph:

PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>


INSERT {

        ### Note that the data is imported into a named graph and not the DEFAULT one
        GRAPH <https://tegrich.github.io/italy_ministers/graphs-defs.html#wikidata>
             {?item  wdt:P39 ?position. 
           ?item rdfs:label ?itemLabel.           # ?item  wdt:P31 wd:Q5.
           # modifier pour disposer de la propriété standard
           ?item  rdf:type wd:Q5.
           }
}
  
        WHERE {
  
  			SELECT DISTINCT ?item ?year ?gender ?itemLabel ?p ?position
  
  			WHERE {

        ## note the service address  
        SERVICE <https://query.wikidata.org/sparql>
           {
            {?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .}  
  
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                  wdt:P39 ?position. # It must necessarily have a birth date property



        BIND(year(?birthDate) as ?year)
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
    ORDER BY ?item 
    OFFSET 0
    LIMIT 10000
}

- Ministers Party :

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
           ?item wdt:P102 ?memberof.
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
                wdt:P102 ?memberof; # It must necessarily have a birth date property
                
        BIND(year(?birthDate) as ?year)
       
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
        LIMIT 10000
- Party Graph :
PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>


INSERT {

        ### Note that the data is imported into a named graph and not the DEFAULT one
        GRAPH <https://tegrich.github.io/italy_ministers/graphs-defs.html#wikidata>
             {?item  wdt:P102 ?memberof. 
           ?item rdfs:label ?itemLabel.           # ?item  wdt:P31 wd:Q5.
           # modifier pour disposer de la propriété standard
           ?item  rdf:type wd:Q5.
           }
}
  
        WHERE {
  
  			SELECT DISTINCT ?item ?year ?gender ?itemLabel ?p ?memberof
  
  			WHERE {

        ## note the service address  
        SERVICE <https://query.wikidata.org/sparql>
           {
            {?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .}  
  
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                  wdt:P102 ?memberof. # It must necessarily have a birth date property



        BIND(year(?birthDate) as ?year)
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
    ORDER BY ?item 
    OFFSET 0
    LIMIT 10000
}

- Ministers Place of Birth :

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
           ?item wdt:P19 ?placeof.
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
                wdt:P19 ?placeof; # It must necessarily have a birth date property
                
        BIND(year(?birthDate) as ?year)
       
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
        LIMIT 10000

- Place of Birth Graph :

PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>


INSERT {

        ### Note that the data is imported into a named graph and not the DEFAULT one
        GRAPH <https://tegrich.github.io/italy_ministers/graphs-defs.html#wikidata>
             {?item  wdt:P19 ?placeof. 
           ?item rdfs:label ?itemLabel.           # ?item  wdt:P31 wd:Q5.
           # modifier pour disposer de la propriété standard
           ?item  rdf:type wd:Q5.
           }
}
  
        WHERE {
  
  			SELECT DISTINCT ?item ?year ?gender ?itemLabel ?p ?placeof
  
  			WHERE {

        ## note the service address  
        SERVICE <https://query.wikidata.org/sparql>
           {
            {?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .}  
  
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                  wdt:P19 ?placeof. # It must necessarily have a birth date property



        BIND(year(?birthDate) as ?year)
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
    ORDER BY ?item 
    OFFSET 0
    LIMIT 10000
}

- Ministers Educated At :

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
           ?item wdt:P69 ?educatedat.
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
                wdt:P69 ?educatedat; # It must necessarily have a birth date property
                
        BIND(year(?birthDate) as ?year)
       
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
        LIMIT 10000

- Educated At Graph :

PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX p: <http://www.wikidata.org/prop/>
PREFIX ps: <http://www.wikidata.org/prop/statement/>


INSERT {

        ### Note that the data is imported into a named graph and not the DEFAULT one
        GRAPH <https://tegrich.github.io/italy_ministers/graphs-defs.html#wikidata>
             {?item  wdt:P69 ?educatedat. 
           ?item rdfs:label ?itemLabel.           # ?item  wdt:P31 wd:Q5.
           # modifier pour disposer de la propriété standard
           ?item  rdf:type wd:Q5.
           }
}
  
        WHERE {
  
  			SELECT DISTINCT ?item ?year ?gender ?itemLabel ?p ?educatedat
  
  			WHERE {

        ## note the service address  
        SERVICE <https://query.wikidata.org/sparql>
           {
            {?item p:P39 ?statement .
  ?statement ps:P39 ?carica .
  ?carica wdt:P279* wd:Q3858501 .}  
  
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                  wdt:P69 ?educatedat. # It must necessarily have a birth date property



        BIND(year(?birthDate) as ?year)
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'it')
    }
   
        }
        }
    ORDER BY ?item 
    OFFSET 0
    LIMIT 10000
}


- Count TripleStore :

PREFIX wd: <http://www.wikidata.org/entity/>

SELECT (COUNT(*) as ?number)
WHERE {
  GRAPH <https://tegrich.github.io/italy_ministers/graphs-defs.html#wikidata> {
  ## deux expressions équivalentes
  # ?item  rdf:type wd:Q5
  ?item  a wd:Q5
        }
}
  

- Inspect Graph :

PREFIX wd: <http://www.wikidata.org/entity/>

SELECT *
WHERE {
  GRAPH <https://tegrich.github.io/italy_ministers/graphs-defs.html#wikidata>
  {
  ?item  a wd:Q5;
        ?p ?o.
        }
}
ORDER BY ?item ?p
LIMIT 1000

  
- Clear Graph :

CLEAR GRAPH <https://tegrich.github.io/italy_ministers/graphs-defs.html#wikidata>