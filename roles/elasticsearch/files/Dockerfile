FROM hypriot/rpi-java

# Install elasticsearch
ENV ES_CONFIG_PATH /data/config/elasticsearch.yml
ENV ES_VERSION 1.7.1
RUN \
  cd /tmp && \
  wget --no-check-certificate https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-$ES_VERSION.tar.gz && \
  tar xvzf elasticsearch-$ES_VERSION.tar.gz && \
  rm -f elasticsearch-$ES_VERSION.tar.gz && \
  mv /tmp/elasticsearch-$ES_VERSION /opt/elasticsearch-$ES_VERSION && \
  ln -s /opt/elasticsearch-$ES_VERSION /opt/elasticsearch

# Install plugins
RUN \
  cd /opt/elasticsearch/bin && \
  ./plugin --install royrusso/elasticsearch-HQ && \
  ./plugin --install mobz/elasticsearch-head && \
  ./plugin --install karmi/elasticsearch-paramedic && \
  ./plugin --install lukas-vlcek/bigdesk && \
  ./plugin --install jettro/elasticsearch-gui && \
  ./plugin --install lmenezes/elasticsearch-kopf

# Basic configuration
ENV ES_CLUSTER_NAME elasticsearch
ENV ES_NODE_MASTER true
ENV ES_NODE_DATA true

VOLUME ["/data/data"]

WORKDIR /data/data

ADD docker-entrypoint.sh /bin/docker-entrypoint.sh

RUN chmod +x /bin/docker-entrypoint.sh

CMD /bin/docker-entrypoint.sh
