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


    docker-compose up -d

    root@igor-X202EP:/home/igor/Postgres# docker exec -it 5113c0a8395e sh
    # su - postgres
    postgres@5113c0a8395e:~$ psql
    psql (12.10 (Debian 12.10-1.pgdg110+1))
    Type "help" for help.
