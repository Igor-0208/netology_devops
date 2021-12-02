Задание 1.
=====================

  show ip route x.x.x.x

![image](https://user-images.githubusercontent.com/60341565/144407123-e8ec3165-9375-4447-85c6-31cf09a7db7e.png)

  show bgp x.x.x.x

![image](https://user-images.githubusercontent.com/60341565/144407729-d22c802f-4491-43df-8183-5edc797c5da8.png)

Задание 2.
=====================

Командой загружаем модуль «dummy», также добавляем опцию «numdummies=2» чтобы сразу создалось два интерфейса dummyX:

    sudo modprobe -v dummy numdummies=2
  
Проверяем, загрузился ли модуль:

	  lsmod | grep dummy

Смотрим создались ли интерфейсы:

    ifconfig -a | grep dummy
    
    ip link
    
    ip address
    
![image](https://user-images.githubusercontent.com/60341565/144418185-6ea3bf19-83ff-4543-962b-8a4624a81263.png)

Добавляем маршруты командой:

    sudo ip route add 192.168.1.1 via 10.0.2.1

![image](https://user-images.githubusercontent.com/60341565/144421605-746debf9-64ef-4367-8e95-d01dafee4d68.png)

Задание 3.
=================

Посмотреть открытые TCP порты в Linux можно разными командами:

    sudo netstat -plnt
    sudo lsof -nP -iTCP -sTCP:LISTEN
    sudo ss -plnt
    
![image](https://user-images.githubusercontent.com/60341565/144427100-3b2792f2-94ca-43b4-912e-0b45d923b740.png)

    Port 53 - systemd-resolve (локальный кэширующий dns резолвер)
    Port 111 - systemd, rpcbind (демон, сопоставляющий универсальные адреса и номера программ RPC. Это сервер, преобразующий номера программ RPC в универсальные адреса)
    Port 22 - sshd (служба, принимающая запросы на соединения от клиентов)

Задание 4.
===================

Посмотреть открытые UDP порты в Linux можно разными командами:

    sudo ss -plnu

![image](https://user-images.githubusercontent.com/60341565/144427220-963d5c16-7dec-4fa6-9d01-0cb459b6dc3e.png)

    Port 68 - systemd-network (системный демон, который управляет сетевыми настройками)
    Port 53 - systemd-resolve (локальный кэширующий dns резолвер)
    Port 111 - systemd, rpcbind (демон, сопоставляющий универсальные адреса и номера программ RPC. Это сервер, преобразующий номера программ RPC в универсальные адреса)
    
Задание 5.
=====================


Задание 6.
=====================

![image](https://user-images.githubusercontent.com/60341565/144434845-b3e942ca-ac2f-4adf-b80c-754b5aa23ebb.png)

![image](https://user-images.githubusercontent.com/60341565/144434717-f70a9a58-3dbd-40c1-af94-b821329fffe5.png)
