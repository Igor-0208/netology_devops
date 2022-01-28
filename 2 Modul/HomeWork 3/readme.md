Задание 1.
=======================

https://hub.docker.com/repository/docker/igor020899/netology

Задание 2.
========================


Задание 3.
=======================

Запускаем первый контейнер centos

    root@igor-X202EP:/home/igor# docker run -it --rm -d --name centos -v $(pwd)/data:/data centos:latest
    Unable to find image 'centos:latest' locally
    latest: Pulling from library/centos
    a1d0c7532777: Pull complete 
    Digest: sha256:a27fd8080b517143cbbbab9dfb7c8571c40d67d534bbdee55bd6c473f432b177
    Status: Downloaded newer image for centos:latest
    7c074f6fae72ee6c2d539b73285ecfc9a05acce23de49cd25698de248bfee243
    root@igor-X202EP:/home/igor# 

