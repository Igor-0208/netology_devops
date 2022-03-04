Задание 1.
====

docker-compose.yml

      version: "3.8"

    services:

      db:
        image: postgres:13
        restart: always
        environment:
          POSTGRES_PASSWORD: netology
        volumes:
          - db-volume:/var/lib/postgresql/data
        ports:
          - 5432:5432

    volumes:
      db-volume:

Запускаем Docker-Compose и заходим в контейнер.

    root@igor-X202EP:/home/igor/Postgres# docker-compose up -d
    Starting postgres_db_1 ... done
    root@igor-X202EP:/home/igor/Postgres# docker ps
    CONTAINER ID   IMAGE         COMMAND                  CREATED       STATUS          PORTS                                       NAMES
    e88dd4f28a25   postgres:13   "docker-entrypoint.s…"   6 hours ago   Up 10 seconds   0.0.0.0:5432->5432/tcp, :::5432->5432/tcp   postgres_db_1
    root@igor-X202EP:/home/igor/Postgres# docker exec -it e88dd4f28a25 sh
    # 

Подключаемся к PostgreSQL

    # su - postgres
    postgres@e88dd4f28a25:~$ psql
    psql (13.6 (Debian 13.6-1.pgdg110+1))
    Type "help" for help.

    postgres=# 

Найдите и приведите управляющие команды для:

-вывода списка БД

      \l[+]   [PATTERN]      list databases
-подключения к БД

        \c[onnect] {[DBNAME|- USER|- HOST|- PORT|-] | conninfo}
                               connect to new database (currently "postgres")
-вывода списка таблиц

      \dt[S+] [PATTERN]      list tables
-вывода описания содержимого таблиц

      \d[S+]  NAME           describe table, view, sequence, or index
-выхода из psql

      \q                     quit psql

Задание 2.
=====

Используя psql создайте БД test_database.

      postgres=# CREATE DATABASE test_database;
      CREATE DATABASE
      
Изучите бэкап БД.

Восстановите бэкап БД в test_database.

      postgres@e88dd4f28a25:/$ psql test_database < /var/tmp/test_dump.sql 
      SET
      SET
      SET
      SET
      SET
       set_config 
      ------------

      (1 row)

      SET
      SET
      SET
      SET
      SET
      SET
      CREATE TABLE
      ALTER TABLE
      CREATE SEQUENCE
      ALTER TABLE
      ALTER SEQUENCE
      ALTER TABLE
      COPY 8
       setval 
      --------
            8
      (1 row)

      ALTER TABLE

Перейдите в управляющую консоль psql внутри контейнера.

      postgres@e88dd4f28a25:/$ psql
      psql (13.6 (Debian 13.6-1.pgdg110+1))
      Type "help" for help.

      postgres=# \l
                                         List of databases
           Name      |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
      ---------------+----------+----------+------------+------------+-----------------------
       postgres      | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
       template0     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
                     |          |          |            |            | postgres=CTc/postgres
       template1     | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
                     |          |          |            |            | postgres=CTc/postgres
       test_database | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
      (4 rows)

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

      postgres=# \c test_database 
      You are now connected to database "test_database" as user "postgres".
      test_database=# \dt
               List of relations
       Schema |  Name  | Type  |  Owner   
      --------+--------+-------+----------
       public | orders | table | postgres
      (1 row)

      test_database=# ANALYZE VERBOSE orders;
      INFO:  analyzing "public.orders"
      INFO:  "orders": scanned 1 of 1 pages, containing 8 live rows and 0 dead rows; 8 rows in sample, 8 estimated total rows
      ANALYZE

Используя таблицу pg_stats, найдите столбец таблицы orders с наибольшим средним значением размера элементов в байтах.

Приведите в ответе команду, которую вы использовали для вычисления и полученный результат.

      test_database=# SELECT attname, avg_width FROM pg_stats WHERE tablename = 'orders' order by avg_width desc limit 1;
       attname | avg_width 
      ---------+-----------
       title   |        16
      (1 row)

Задание 3.
===

