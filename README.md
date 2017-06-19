ElasticSearchWorkshop
=====================

Installatie stappenplan
==========================

 1.  Download de binaries op: https://www.elastic.co/products
	 1. Elasticsearch
	 2. Kibana
 2.  Configuren elastic-search en kibana
	 1. Vervang de config bestanden in de mappen kibana/config en elasticsearch/config met de config bestanden uit de git repository.

Mappings aanmaken
====================

Mapping voor Shakespeare dataset
```
curl -XPUT 'localhost:9200/shakespeare?pretty' -H 'Content-Type: application/json' -d'
{
 "mappings" : {
  "_default_" : {
   "properties" : {
    "speaker" : {"type": "keyword" },
    "play_name" : {"type": "keyword" },
    "line_id" : { "type" : "integer" },
    "speech_number" : { "type" : "integer" }
   }
  }
 }
}
'
```

Mapping voor logstash dataset
```
curl -XPUT 'localhost:9200/logstash-2015.05.18?pretty' -H 'Content-Type: application/json' -d'
{
  "mappings": {
    "log": {
      "properties": {
        "geo": {
          "properties": {
            "coordinates": {
              "type": "geo_point"
            }
          }
        }
      }
    }
  }
}
'
```
```
curl -XPUT 'localhost:9200/logstash-2015.05.19?pretty' -H 'Content-Type: application/json' -d'
{
  "mappings": {
    "log": {
      "properties": {
        "geo": {
          "properties": {
            "coordinates": {
              "type": "geo_point"
            }
          }
        }
      }
    }
  }
}
'
```
```
curl -XPUT 'localhost:9200/logstash-2015.05.20?pretty' -H 'Content-Type: application/json' -d'
{
  "mappings": {
    "log": {
      "properties": {
        "geo": {
          "properties": {
            "coordinates": {
              "type": "geo_point"
            }
          }
        }
      }
    }
  }
}
'
```

Indexen vullen
============
```
curl -H 'Content-Type: application/x-ndjson' -XPOST 'localhost:9200/bank/account/_bulk?pretty' --data-binary @accounts.json
```
```
curl -H 'Content-Type: application/x-ndjson' -XPOST 'localhost:9200/shakespeare/_bulk?pretty' --data-binary @shakespeare.json
```
```
curl -H 'Content-Type: application/x-ndjson' -XPOST 'localhost:9200/_bulk?pretty' --data-binary @logs.jsonl
```
Informatie over de net gevulde indexen
```
curl -XGET 'localhost:9200/_cat/indices?v&pretty'
```

Query documentatie
==================

https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html

Opdrachten
===========
In de folder Opdrachten staan enkele opdrachten om je op weg te helpen met het schrijven van queries. De tekstbestanden bevatten de opdrachten en de Json bestanden de oplossingen.

Kibana url
==========
http://localhost:5601

X-PACK (Optioneel)
======
```
Wanneer x-pack geïnstalleerd is werk ElasticHQ niet meer.
```

 Installeren X-Pack plugins voor security
	 1. bin/elastic-plugin install x-pack
		 1. *Vraagt tijdens de installatie om premissies
	 2. bin/kibana-plugin install x-pack

user: elastic
password: changeme
