FROM java:7
MAINTAINER David Gibb <david.gibb@slalom.com>

ENV path https://download.elasticsearch.org/elasticsearch/elasticsearch
ENV package elasticsearch-1.5.1

RUN wget -q ${path}/${package}.tar.gz
RUN tar zxf ${package}.tar.gz
WORKDIR ${package}

EXPOSE 9200
CMD bin/elasticsearch

