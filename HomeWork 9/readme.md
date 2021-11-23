Задание 1.
================

![image](https://user-images.githubusercontent.com/60341565/142986575-c6d8ad5d-97b1-40a7-887d-60c30ef6e073.png)

Создаем Systemd Unit:

![image](https://user-images.githubusercontent.com/60341565/142986662-ff946d81-a336-457d-ace3-ca50d7e67b7d.png)

Добавляем сервис в автозагрузку, запускаем его, проверяем статус командами:

 sudo systemctl daemon-reload
 
 sudo systemctl enable --now node_exporter
 
 sudo systemctl status node_exporter

Проверяем порт 9100 командой sudo ss -pnltu | grep 9100

![image](https://user-images.githubusercontent.com/60341565/142987123-c9721878-ae66-4f34-b27c-8857c4a448c6.png)

Задание 2.
===================
