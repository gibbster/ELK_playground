FROM java:7
MAINTAINER David Gibb <david.gibb@slalom.com>

ENV path https://download.elastic.co/kibana/kibana
ENV package kibana-4.1.1-linux-x64

RUN wget -q ${path}/${package}.tar.gz
RUN tar zxf ${package}.tar.gz
WORKDIR ${package}

EXPOSE 5601
CMD bin/kibana

