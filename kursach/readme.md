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
