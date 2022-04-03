Задание 1.
===

Dockerfile:

    FROM centos:7

    EXPOSE 9200 9300


    RUN groupadd elasticsearch \
        && useradd -s /sbin/nologin -c "elasticsearch" -g elasticsearch elasticsearch \
        && yum -y install wget \
        && yum clean all \
        && mkdir -p /opt/ext_volume/logs \
        && mkdir -p /opt/ext_volume/data \
        && cd /opt \
        && wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.0.0-linux-x86_64.tar.gz \
        && tar -xzf elasticsearch-8.0.0-linux-x86_64.tar.gz \
        && rm -f /opt/*.tar.gz \
        && chown -R elasticsearch:elasticsearch /opt/*

    VOLUME /opt/ext_volume

    COPY --chown=elasticsearch:elasticsearch ./config /opt/elasticsearch-8.0.0/config

    USER elasticsearch:elasticsearch

    ENV ES_USER=elasticsearch ES_GROUP=elasticsearch
    WORKDIR /opt/elasticsearch-8.0.0/bin

    ENTRYPOINT ./elasticsearch

Авторизируемся:

    docker login

Собираем Docker-образ:

    docker build . -t centos7-elasticsearch8_0_0
    
Создаем тэг:

    docker tag centos7-elasticsearch8_0_0:latest igor020899/netology:centos7-elasticsearch

Загружаем на Docker Hub

    docker push igor020899/netology:centos7-elasticsearch

Запускаем Docker контейнер:

    docker run -d --mount source=es_volume,target=/opt/ext_volume --ulimit nofile=65535 -p=9200:9200 -p=9300:9300 centos7-elasticsearch8_0_0

Проверяем:

    root@igor-X202EP:/home/igor/centos7:elasticsearch# docker ps
    CONTAINER ID   IMAGE                        COMMAND                  CREATED         STATUS         PORTS                                                                                  NAMES
    eb36cd5a9900   centos7-elasticsearch8_0_0   "/bin/sh -c ./elasti…"   3 seconds ago   Up 2 seconds   0.0.0.0:9200->9200/tcp, :::9200->9200/tcp, 0.0.0.0:9300->9300/tcp, :::9300->9300/tcp   ecstatic_cray
      



