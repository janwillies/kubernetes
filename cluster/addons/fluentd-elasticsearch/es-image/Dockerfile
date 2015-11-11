# A Dockerfile for creating an Elasticsearch instance that is designed
# to work with Kubernetes logging. Inspired by the Dockerfile
# dockerfile/elasticsearch

FROM java:openjdk-7-jre
MAINTAINER Satnam Singh "satnam@google.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y curl && \
    apt-get clean

RUN cd / && \
    curl -O https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.0.0/elasticsearch-2.0.0.tar.gz && \
    tar xf elasticsearch-2.0.0.tar.gz && \
    rm elasticsearch-2.0.0.tar.gz

COPY elasticsearch.yml /elasticsearch-2.0.0/config/elasticsearch.yml
COPY run.sh /
COPY elasticsearch_logging_discovery /

RUN useradd es && \
    chown -R es:es /elasticsearch-2.0.0 && \
    chown -R es:es /elasticsearch_logging_discovery

USER es

VOLUME ["/data"]
EXPOSE 9200 9300

CMD ["/run.sh"]
