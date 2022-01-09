Задание 1.
==========================
![image](https://user-images.githubusercontent.com/60341565/148276381-d388e85d-a109-4b56-9090-1af660754295.png)


![image](https://user-images.githubusercontent.com/60341565/148275846-e1034f94-a931-4c18-843d-9431e40eece1.png)


Задание 2.
===========================

![image](https://user-images.githubusercontent.com/60341565/148275464-27f5a06c-6d51-4395-beba-75e9826b6176.png)

Задание 3.
===========================

![image](https://user-images.githubusercontent.com/60341565/148404087-5c21da00-0f25-4d69-90bd-019a1ed15cf1.png)

![image](https://user-images.githubusercontent.com/60341565/148404557-17ab0078-853a-44bd-a9aa-b624da411939.png)

![image](https://user-images.githubusercontent.com/60341565/148518768-d670ea9e-77c7-4fd3-b13e-e0e6d2858248.png)

Задание 4.
===========================

Настройка рабочего окружения

Воспользуемся командой 

    export VAULT_ADDR=http://127.0.0.1:8200
Она укажет текущему окружению подключаться к серверу по http. Затем открываем файл 
    
    nano /etc/vault.d/vault.hcl

И снимаем комментарии со следующих строк:
 
    listener "tcp" {
      address = "127.0.0.1:8200"
      tls_disable = 1
    }

Перезапускаем службу vault:

    systemctl restart vault

Обновляем системную переменную VAULT_ADDR:

    export VAULT_ADDR=http://127.0.0.1:8200
    
Выводим на экран статус:

    vault status
    
![image](https://user-images.githubusercontent.com/60341565/148524883-830b4f69-fa76-407e-adb4-e4215b6b4aba.png)

Инициализируем vault:

    vault operator init

![image](https://user-images.githubusercontent.com/60341565/148530317-9672a211-78e5-42ed-a089-a8619646b4f5.png)

![image](https://user-images.githubusercontent.com/60341565/148531125-fe945345-3fad-4085-a3e9-7a8ff8a31c82.png)

![image](https://user-images.githubusercontent.com/60341565/148539200-05e50048-08e6-4626-86c2-acfcc00ee452.png)

![image](https://user-images.githubusercontent.com/60341565/148539842-75619d48-6061-41b7-968e-4da51568a690.png)

![image](https://user-images.githubusercontent.com/60341565/148689968-e92d101c-7015-428d-86ed-77b829097786.png)

Задание 5.
=====================

Создаем директорию

    sudo mkdir /usr/local/share/ca-certificates
    
Копируем наш сертификат в директорию

    sudo cp vault.example.com.crt /usr/local/share/ca-certificates/
    
Обновляем список

    sudo update-ca-certificates
    
![image](https://user-images.githubusercontent.com/60341565/148693298-b20da070-d1ba-47ba-8ddb-709bacbbf5e4.png)

Добавляем свой корневой СА в доверенные

    sudo cp ./vault.example.com.crt /etc/ca-certificates/trust-source/anchors/

Обновляем общесистемный список доверенных CA

    sudo update-ca-trust

Задание 6.
==============================

Устанавливаем nginx 

    sudo apt-get install nginx

![image](https://user-images.githubusercontent.com/60341565/148697053-b6ba027f-1e75-47e2-b76c-cec7b9c584b2.png)

Запускаем 

    systemctl enable nginx
    systemctl start nginx
    
![image](https://user-images.githubusercontent.com/60341565/148697141-d6dfd53a-45ff-45fe-be65-0ac81ed2d25f.png)
