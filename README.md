Дипломный практикум в YandexCloud
===
1. Зарегистрировать доменное имя (любое на ваш выбор в любой доменной зоне).
![изображение](https://user-images.githubusercontent.com/60341565/185978183-4ce1d001-725b-4880-9912-819673a8d34d.png)

2. Создание инфраструктуры

Создаем сервис-аккаунт:

    root@igor-X202EP:/home/igor/netology_devops# yc iam service-account create --name netology-diplom
    id: ajeg51rca6rirh4giupl
    folder_id: b1gspe3rb4i7q3fdemk1
    created_at: "2022-08-22T16:46:04.206024969Z"
    name: netology-diplom

Назначаем роль editor:

    root@igor-X202EP:/home/igor/netology_devops# yc resource-manager folder add-access-binding b1gspe3rb4i7q3fdemk1 --role editor --subject serviceAccount:ajeg51rca6rirh4giupl
    done (1s)
    
Создаем статический ключ доступа:

    root@igor-X202EP:/home/igor/netology_devops# yc iam access-key create --service-account-name netology-diplom
    access_key:
      id: ajeuds8ih3ucug4fqb8h
      service_account_id: ajeg51rca6rirh4giupl
      created_at: "2022-08-22T17:09:28.742607390Z"
      key_id: YCAJEz3RgxSkVAtjtv4N1qmVh
    secret: YCPakqMEZEwf8kibsQm4qPULds1EzIIFE2qS2Q65
2. Создали бакет в YC:

