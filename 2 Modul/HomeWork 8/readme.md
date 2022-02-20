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

Перейдите в управляющую консоль mysql внутри контейнера.

        root@181f1d009733:/#  mysql -u root -p
        Enter password: 
        Welcome to the MySQL monitor.  Commands end with ; or \g.
        Your MySQL connection id is 11
        Server version: 8.0.28 MySQL Community Server - GPL

Найдите команду для выдачи статуса БД и приведите в ответе из ее вывода версию сервера БД.

    mysql> \s
    --------------
    mysql  Ver 8.0.28 for Linux on x86_64 (MySQL Community Server - GPL)

    Connection id:		11
    Current database:	
    Current user:		root@localhost
    SSL:			Not in use
    Current pager:		stdout
    Using outfile:		''
    Using delimiter:	;
    Server version:		8.0.28 MySQL Community Server - GPL
