# ELK trivial configuration

## Goal

The goal of this repository is to understand elasticsearch, kibana, and logstash work together. This the simplest demo configuration I could come up with that separated each component into a separate container.

This is _not_ intended to be used in any type of production environment. Use an official repo on docker hub for that.

This version uses logspout as a source for logstash/elasticsearch.

## Usage

Before running, be sure that docker has been correctly installed. Optionally install docker-compose

### Building and running (docker-compose)

    docker-compose build
    docker-compose up

### Building and running (manually)

TODO

### Adding content and viewing the results

First, review the ports and IPs. If you are running docker locally, use `localhost` for the `$DOCKER_IP`. If you are using boot2docker, use the results of `boot2docker ip`.

To see the ports used by each container, use `docker ps` or `docker-compose ps`.

Let's add content to the elasticsearch server. 

    ab -n 1000 -c 50 'http://$DOCKER_IP:$NGINX_PORT'

View the directly from the Elasticsearch REST interface:

    curl 'http://$DOCKER_IP:$ES_PORT/_search?pretty'

Search for and view the results on Kibana by going to `http://$DOCKER_IP:$KIBANA_PORT` on your favorite browser

