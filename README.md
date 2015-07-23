# ELK trivial configuration

## Goal

The goal of this repository is to understand elasticsearch, kibana, and logstash work together. This the simplest demo configuration I could come up with that separated each component into a separate container.

This is _not_ intended to be used in any type of production environment. Use an official repo on docker hub for that.

This version uses nc as a source for logstash/elasticsearch. Use the logspout branch for a version which uses nginx as a source.

## Usage

Before running, be sure that docker has been correctly installed. Optionally install docker-compose

### Building and running (docker-compose)

    docker-compose build
    docker-compose up

### Building and running (manually)

First, build the docker containers

    docker build -t logstash logstash
    docker build -t elasticsearch elasticsearch 
    docker build -t kibana kibana

Next, run the containers. 
    
    docker run -d --name es elasticsearch
    docker run -P -d --link es:es -t logstash bin/logstash -e 'input { tcp { port 9000 } } output { elasticsearch { host => es } }'
    docker run -d -P --link es:es -v $PWD/config:/kibana-4.1.1-linux-x64/config kibana
    
### Adding content and viewing the results

First, review the ports and IPs. If you are running docker locally, use `localhost` for the `$DOCKER_IP`. If you are using boot2docker, use the results of `boot2docker ip`.

To see the ports used by each container, use `docker ps` or `docker-compose ps`.

Let's add content to the elasticsearch server. Connect to the logstash input port and add "logs" (one entry per line).

    nc $DOCKER_IP $LOGSTASH_PORT

View the directly from the Elasticsearch REST interface:

    curl 'http://$DOCKER_IP:$ES_PORT/_search?pretty'

Search for and view the results on Kibana by going to `http://$DOCKER_IP:$KIBANA_PORT` on your favorite browser

