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

    postgres=# test_db=# \l                   
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

    postgres-# test_db=# \d clients
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

    postgres-# test_db=# \d orders
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

