Задание 1.
===

Используя docker поднимите инстанс MySQL (версию 8). Данные БД сохраните в volume.

    docker run --rm --name my \
        -e MYSQL_DATABASE=test_db \
        -e MYSQL_ROOT_PASSWORD=netology \
        -v $PWD/backup:/var/tmp/backup \
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

Приведите в ответе количество записей с price > 300.

        mysql> select count(*) from orders where price > 300;
        +----------+
        | count(*) |
        +----------+
        |        1 |
        +----------+
        1 row in set (0.00 sec)

Задание 2.
===

Создайте пользователя test в БД c паролем test-pass

        CREATE USER 'test'@'localhost' 
            IDENTIFIED WITH mysql_native_password BY 'test-pass'
            WITH MAX_CONNECTIONS_PER_HOUR 100
            PASSWORD EXPIRE INTERVAL 180 DAY
            FAILED_LOGIN_ATTEMPTS 3 PASSWORD_LOCK_TIME 2
            ATTRIBUTE '{"first_name":"James", "last_name":"Pretty"}';

Предоставьте привелегии пользователю test на операции SELECT базы test_db

        grant select on test_db.* to test;

Используя таблицу INFORMATION_SCHEMA.USER_ATTRIBUTES получите данные по пользователю test

        mysql> select * from INFORMATION_SCHEMA.USER_ATTRIBUTES where user = 'test';
        +------+-----------+------------------------------------------------+
        | USER | HOST      | ATTRIBUTE                                      |
        +------+-----------+------------------------------------------------+
        | test | localhost | {"last_name": "Pretty", "first_name": "James"} |
        +------+-----------+------------------------------------------------+
        1 row in set (0.00 sec)
        
Задание 3.
===

Исследуйте, какой engine используется в таблице БД test_db

        mysql> SELECT table_schema,table_name,engine FROM information_schema.tables WHERE table_schema = DATABASE();
        +--------------+------------+--------+
        | TABLE_SCHEMA | TABLE_NAME | ENGINE |
        +--------------+------------+--------+
        | test_db      | orders     | InnoDB |
        +--------------+------------+--------+
        1 row in set (0.00 sec)

Измените engine и приведите время выполнения и запрос на изменения из профайлера в ответе

        set profiling = 1;
        alter table orders engine = 'MyISAM';
        alter table orders engine = 'InnoDB';
        show profiles;

Профайлер:

        mysql> show profiles;
        +----------+------------+--------------------------------------+
        | Query_ID | Duration   | Query                                |
        +----------+------------+--------------------------------------+
        |        1 | 0.02436675 | alter table orders engine = 'MyISAM' |
        |        2 | 0.02349825 | alter table orders engine = 'InnoDB' |
        |        3 | 0.01897750 | alter table orders engine = 'MyISAM' |
        |        4 | 0.02332425 | alter table orders engine = 'InnoDB' |
        |        5 | 0.01927200 | alter table orders engine = 'MyISAM' |
        |        6 | 0.02297425 | alter table orders engine = 'InnoDB' |
        |        7 | 0.01822650 | alter table orders engine = 'MyISAM' |
        |        8 | 0.02154475 | alter table orders engine = 'InnoDB' |
        +----------+------------+--------------------------------------+

Задание 4.
========

Буффер кеширования 30% рассчитан - 2гб ОЗУ

        [mysqld]
        pid-file        = /var/run/mysqld/mysqld.pid
        socket          = /var/run/mysqld/mysqld.sock
        datadir         = /var/lib/mysql
        secure-file-priv= NULL

        # Custom config should go here
        !includedir /etc/mysql/conf.d/

        # Netology
        innodb_flush_log_at_trx_commit = 2
        innodb_file_per_table = ON
        innodb_log_buffer_size = 1048576
        innodb_buffer_pool_size = 1688207360
        innodb_log_file_size = 104857600
