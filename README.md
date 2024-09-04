# Documentation

Source : https://elk-docker.readthedocs.io/

# Installation avec Docker

## Commandes nécessaires

- `sudo sysctl -w vm.max_map_count=262144` (nécessaire sur Linux depuis version 5 de Elasticsearch)
- `docker-compose up` (pour lancer l'image)

## Commandes facultatives

- `docker pull sebp/elk` (pour installer l'image)
- `docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 -it --name elk sebp/elk` (pour lancer l'image et **5601 pour Kibana, 9200 pour Elasticsearch et 5044 pour Logstash**)
- `docker start elk` (pour relancer après avoir stoppé)
- `docker run -p 5601:5601 -p 9200:9200 -p 5044:5044 -it -e LOGSTASH_START=0 -e KIBANA_START=0 --name elk sebp/el` (lancement de certains composants (dans ce cas Elasticsearch) avec != de 1)

# Création de logs pour tester

- `docker compose up` (pour lancer le container)
- `docker ps` (pour récupérer le nom du container)
- `sudo docker exec -it <container-name> /bin/bash` (pour ouvrir un terminal dans le container)
- `/opt/logstash/bin/logstash --path.data /tmp/logstash/data -e 'input { stdin { } } output { elasticsearch { hosts => ["localhost"] } }'` (pour créer un log)
- entrer ensuite du texte et quitter avec CTRL+C
- aller sur *http://127.0.0.1:9200/_search?pretty&size=1000* pour voir le résultat (Elasticsearch)
- aller sur *http://127.0.0.1:5601* pour voir le résultat (Kibana)
