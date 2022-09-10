Дипломный практикум в YandexCloud
===
1. Зарегистрировать доменное имя (любое на ваш выбор в любой доменной зоне).
![изображение](https://user-images.githubusercontent.com/60341565/185978183-4ce1d001-725b-4880-9912-819673a8d34d.png)

2. Создание инфраструктуры

Создаем сервис-аккаунт:

    root@igor-X202EP:/home/igor/netology_devops# yc iam service-account create --name netology-diplom
    id: ***
    folder_id: ***
    created_at: "2022-08-22T16:46:04.206024969Z"
    name: netology-diplom

Назначаем роль editor:

    root@igor-X202EP:/home/igor/netology_devops# yc resource-manager folder add-access-binding *** --role editor --subject serviceAccount:***
    done (1s)
    
Создаем статический ключ доступа:

    root@igor-X202EP:/home/igor/netology_devops# yc iam access-key create --service-account-name netology-diplom
    access_key:
      id: ***
      service_account_id: ***
      created_at: "2022-08-22T17:09:28.742607390Z"
      key_id: ***
    secret: ***
 Создали бакет в YC:

![изображение](https://user-images.githubusercontent.com/60341565/185986619-e864211f-bb43-422b-9c17-2d1a1d869a94.png)

Конфигурация содержится в файле provider.tf:

        backend "s3" {
          endpoint = "storage.yandexcloud.net"
          bucket   = "netology-diplom-devops"
          region   = "ru-central1"
          key      = "stage/terraform-stage.tfstate"

          skip_region_validation      = true
          skip_credentials_validation = true
        }
        
 Настройка workspaces

Создаем workspaces `prod` и `stage`:
![изображение](https://user-images.githubusercontent.com/60341565/185987254-33395269-a42f-461c-b9ee-bbb93b5f3db0.png)

    root@igor-X202EP:/home/igor/netology_devops/diplom/terraform# terraform workspace list
      default
      prod
    * stage

Экспортируем ключи сервисного аккаунта

        export AWS_ACCESS_KEY_ID=Ключ доступа
        export AWS_SECRET_ACCESS_KEY=Секретный ключ

Создание VPC с подсетями в разных зонах доступности.
![изображение](https://user-images.githubusercontent.com/60341565/186162915-0b9c77a3-79d2-4068-bc40-6065db2c6896.png)
