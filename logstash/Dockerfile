FROM java:7
MAINTAINER David Gibb <david.gibb@slalom.com>

ENV path https://download.elasticsearch.org/logstash/logstash
ENV package logstash-1.5.2

RUN wget ${path}/${package}.tar.gz
RUN tar zxvf ${package}.tar.gz
WORKDIR ${package}

EXPOSE 9000

CMD bin/logstash -e 'input { tcp { port => 9000 } } output { stdout {} }'

