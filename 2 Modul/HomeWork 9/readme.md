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

