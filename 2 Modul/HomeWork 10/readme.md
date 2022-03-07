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


