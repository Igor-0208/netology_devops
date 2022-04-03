Задание 1.
================

docker-compose.yml

    version: "3.8"

    services:

      postgres:
        image: postgres:12
        restart: always
        environment:
          POSTGRES_PASSWORD: netology
        volumes:
          - data:/var/lib/postgresql/data
          - backup:/var/tmp/backup
        ports:
          - 5432:5432

    volumes:
      data:
      backup:

Запускаем Docker-Compose

    docker-compose up -d

Запускаем команду в работающем контейнере

    root@igor-X202EP:/home/igor/Postgres# docker exec -it 5113c0a8395e sh
    # su - postgres
    postgres@5113c0a8395e:~$ psql
    psql (12.10 (Debian 12.10-1.pgdg110+1))
    Type "help" for help.

Задание 2.
====================

Итоговый список БД после выполнения пунктов выше.
================================================

    postgres=# \l                   
                                     List of databases
       Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileg
    es   
    -----------+----------+----------+------------+------------+------------------
    -----
     postgres  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
     template0 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres      
        +
               |          |          |            |            | postgres=CTc/post
    gres
     template1 | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres      
        +
               |          |          |            |            | postgres=CTc/post
    gres
     test_db   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
    (4 rows)

    postgres-# 

Описание таблиц (describe)
==========================

clients

    postgres-# \d clients
                                              Table "public.clients"
                  Column               |  Type   | Collation | Nullable |               Default               
    -----------------------------------+---------+-----------+----------+-------------------------------------
     id                                | integer |           | not null | nextval('clients_id_seq'::regclass)
     фамилия                    | text    |           |          | 
     страна_проживания | text    |           |          | 
     заказ                        | integer |           |          | 
    Indexes:
        "clients_pkey" PRIMARY KEY, btree (id)
        "страна_проживания_idx" btree ("страна_проживания")
    Foreign-key constraints:
        "fk_orders" FOREIGN KEY ("заказ") REFERENCES orders(id)

    postgres-# 

orders

    postgres-# \d orders
                                         Table "public.orders"
              Column          |  Type   | Collation | Nullable |              Default               
    --------------------------+---------+-----------+----------+------------------------------------
     id                       | integer |           | not null | nextval('orders_id_seq'::regclass)
     наименование | text    |           |          | 
     цена                 | integer |           |          | 
    Indexes:
        "orders_pkey" PRIMARY KEY, btree (id)
    Referenced by:
        TABLE "clients" CONSTRAINT "fk_orders" FOREIGN KEY ("заказ") REFERENCES orders(id)

    postgres-# 
    

SQL-запрос для выдачи списка пользователей с правами над таблицами test_db
=====================    

    SELECT * from information_schema.table_privileges WHERE grantee LIKE 'test%';
    
Список пользователей с правами над таблицами test_db
===

    postgres=# SELECT * from information_schema.table_privileges WHERE grantee LIKE 'test%';
     grantor  |     grantee      | table_catalog | table_schema | table_name | privilege_type | is_grantable | with_hierarchy 
    ----------+------------------+---------------+--------------+------------+----------------+--------------+----------------
     postgres | test_admin_user  | postgres      | public       | orders     | INSERT         | NO           | NO
     postgres | test_admin_user  | postgres      | public       | orders     | SELECT         | NO           | YES
     postgres | test_admin_user  | postgres      | public       | orders     | UPDATE         | NO           | NO
     postgres | test_admin_user  | postgres      | public       | orders     | DELETE         | NO           | NO
     postgres | test_admin_user  | postgres      | public       | orders     | TRUNCATE       | NO           | NO
     postgres | test_admin_user  | postgres      | public       | orders     | REFERENCES     | NO           | NO
     postgres | test_admin_user  | postgres      | public       | orders     | TRIGGER        | NO           | NO
     postgres | test_admin_user  | postgres      | public       | clients    | INSERT         | NO           | NO
     postgres | test_admin_user  | postgres      | public       | clients    | SELECT         | NO           | YES
     postgres | test_admin_user  | postgres      | public       | clients    | UPDATE         | NO           | NO
     postgres | test_admin_user  | postgres      | public       | clients    | DELETE         | NO           | NO
     postgres | test_admin_user  | postgres      | public       | clients    | TRUNCATE       | NO           | NO
     postgres | test_admin_user  | postgres      | public       | clients    | REFERENCES     | NO           | NO
     postgres | test_admin_user  | postgres      | public       | clients    | TRIGGER        | NO           | NO
     postgres | test_simple_user | postgres      | public       | orders     | INSERT         | NO           | NO
     postgres | test_simple_user | postgres      | public       | orders     | SELECT         | NO           | YES
     postgres | test_simple_user | postgres      | public       | orders     | UPDATE         | NO           | NO
     postgres | test_simple_user | postgres      | public       | orders     | DELETE         | NO           | NO
     postgres | test_simple_user | postgres      | public       | clients    | INSERT         | NO           | NO
     postgres | test_simple_user | postgres      | public       | clients    | SELECT         | NO           | YES
     postgres | test_simple_user | postgres      | public       | clients    | UPDATE         | NO           | NO
     postgres | test_simple_user | postgres      | public       | clients    | DELETE         | NO           | NO
    (22 rows)

    postgres=# 

Задание 3.
===

Таблица orders

    postgres=#  select * from orders;
     id | наименование | цена 
    ----+--------------------------+----------
      1 | Шоколад           |       10
      2 | Принтер           |     3000
      3 | Книга               |      500
      4 | Монитор           |     7000
      5 | Гитара             |     4000
    (5 rows)

    postgres=# 

Таблица clients

    postgres=#  select * from clients;
     id |             фамилия             | страна_проживания | заказ 
    ----+----------------------------------------+------------------------------
    -----+------------
      1 | Иванов Иван Иванович | USA                               |           
      2 | Петров Петр Петрович | Canada                            |           
      3 | Иоганн Себастьян Бах | Japan                             |           
      4 | Ронни Джеймс Дио         | Russia                            |           
      5 | Ritchie Blackmore                      | Russia                       
         |           
    (5 rows)

    postgres=# 
    
Вычислите количество записей для каждой таблицы, приведите в ответе: запросы, результаты их выполнения.
===

    postgres=# select count(*) from orders;
     count 
    -------
         5
    (1 row)

    postgres=# select count(*) from clients;
     count 
    -------
         5
    (1 row)

    postgres=# 

Задание 4.
===

Приведите SQL-запросы для выполнения данных операций.

    update clients set заказ = (select id from orders where наименование = 'Книга') where фамилия = 'Иванов Иван Иванович';
    update clients set заказ = (select id from orders where наименование = 'Монитор') where фамилия = 'Петров Петр Петрович';
    update clients set заказ = (select id from orders where наименование = 'Гитара') where фамилия = 'Иоганн Себастьян Бах';

Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод данного запроса.

    postgres=# select c.* from clients c join orders o on c.заказ = o.id;
     id |             фамилия             | страна_проживания | заказ 
    ----+----------------------------------------+-----------------------------------+------------
      1 | Иванов Иван Иванович | USA                               |          3
      2 | Петров Петр Петрович | Canada                            |          4
      3 | Иоганн Себастьян Бах | Japan                             |          5
    (3 rows)

    postgres=# 

Задание 5.
===

    postgres=# EXPLAIN SELECT * FROM clients WHERE заказ IS NOT NULL;
                            QUERY PLAN                         
    -----------------------------------------------------------
     Seq Scan on clients  (cost=0.00..18.10 rows=806 width=72)
       Filter: ("заказ" IS NOT NULL)
    (2 rows)

    postgres=# 
    

cost=первая_запись..вся_выборка - сколько времени уйдёт на поиск первой записи и сбор всей выборки

rows - сколько примерно будет строк

width - какой будет средняя длина строки в байтах

Задание 6.
===

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. Задачу 1).

    pg_dump -U postgres -h db -p 5432 --format=custom --clean --create --if-exists -f /var/tmp/backup/test_db.custom test_db

Остановите контейнер с PostgreSQL (но не удаляйте volumes).

    root@igor-X202EP:/home/igor/Postgres# docker-compose stop
    Stopping postgres_postgres_1 ... done
    root@igor-X202EP:/home/igor/Postgres# docker ps -a
    CONTAINER ID   IMAGE          COMMAND                  CREATED        STATUS                      PORTS     NAMES
    5113c0a8395e   postgres:12    "docker-entrypoint.s…"   4 hours ago    Exited (0) 12 seconds ago             postgres_postgres_1

Поднимите новый пустой контейнер с PostgreSQL.

    root@igor-X202EP:/home/igor/Postgres# docker run --rm -d -e POSTGRES_USER=test-admin-user -e POSTGRES_PASSWORD=netology -e POSTGRES_DB=test_db -v psql_backup:/var/tmp/backup --name postgres_2 postgres:12
    48269c9d955ce5b633bd784145f8d86790144b035ab66c4bf9422a96e5b7cb12
    root@igor-X202EP:/home/igor/Postgres# docker ps -a
    CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                     PORTS      NAMES
    48269c9d955c   postgres:12    "docker-entrypoint.s…"   24 seconds ago   Up 22 seconds              5432/tcp   postgres_2
    5113c0a8395e   postgres:12    "docker-entrypoint.s…"   5 hours ago      Exited (0) 5 minutes ago              postgres_postgres_1

Восстановите БД test_db в новом контейнере.

    docker exec -it postgres_2  bash
    export PGPASSWORD=netology && postgres_postgres_1 -h localhost -U test-admin-user -f $(ls -1trh /var/tmp/backup/*.sql) test_db

