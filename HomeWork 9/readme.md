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

Командой curl http://localhost:9100/metrics выводим metrics 

CPU:

node_cpu_guest_seconds_total

node_cpu_seconds_total

Диск:

node_disk_io_time_seconds_total

node_disk_read_bytes_total

node_disk_read_time_seconds_total 

node_disk_write_time_seconds_total

node_disk_write_bytes_total

node_disk_info

node_disk_io_now

Память:

node_memory_MemTotal_bytes

node_memory_Cached_bytes

node_memory_SwapFree_bytes

node_memory_SwapTotal_bytes

node_memory_MemAvailable_bytes 

node_memory_MemFree_bytes

Сеть:

node_network_speed_bytes

node_network_receive_errs_total

node_network_receive_bytes_total

node_network_transmit_bytes_total

node_network_transmit_errs_total

Задание 3.
===================

![image](https://user-images.githubusercontent.com/60341565/143031125-2fa8e88e-4ee2-4bbd-90fa-84dfb7c706ee.png)

![image](https://user-images.githubusercontent.com/60341565/143031201-46431238-17b8-43e5-90a5-5108208da362.png)

Задание 4.
===================

![image](https://user-images.githubusercontent.com/60341565/143036293-4b474b71-8ee5-4da8-88ac-77143c93fa40.png)

Задание 5.
===================

