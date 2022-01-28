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

Запускаем второй контейнер debian

    root@igor-X202EP:/home/igor# docker run -it --rm -d --name debian -v $(pwd)/data:/data debian:stable
    Unable to find image 'debian:stable' locally
    stable: Pulling from library/debian
    282deafaaa63: Pull complete 
    Digest: sha256:4771808bf8178f6570b1c3bc6a36b72588bb86079529fdd464ab02377cfc9a00
    Status: Downloaded newer image for debian:stable
    269ace4a24ca5226da1d2b19d8ba17d64bca2e8b1cd37cd0d68d7e99e0b0fd77

Создали текстовый файл с помощью docker exec

    root@igor-X202EP:/home/igor# docker exec -it centos bash
    [root@7c074f6fae72 /]# echo "Hello Netology" > /data/centos.txt
    [root@7c074f6fae72 /]# exit
    exit

Создали текстовый файл с хоста

    root@igor-X202EP:/home/igor# echo "Hello Netology" > data/host.txt

Листинг и содержание файлов

    root@igor-X202EP:/home/igor# docker exec -it debian bash
    root@269ace4a24ca:/# ls -l /data/
    total 8
    -rw-r--r-- 1 root root 15 Jan 28 15:47 centos.txt
    -rw-r--r-- 1 root root 27 Jan 28 15:48 host.txt
