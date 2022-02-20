Задание 1.
===

Используя docker поднимите инстанс MySQL (версию 8). Данные БД сохраните в volume.

    docker run --rm --name my \
        -e MYSQL_DATABASE=test_db \
        -e MYSQL_ROOT_PASSWORD=netology \
        -v $PWD/backup:/media/mysql/backup \
        -v my_data:/var/lib/mysql \
        -v $PWD/config/conf.d:/etc/mysql/conf.d \
        -p 13306:3306 \
        -d mysql:8
        

    root@igor-X202EP:/home/igor# docker exec -it 181f1d009733 bash
