Задание 5.

Характеристики виртуальной машины запущенной через Vagrant
![image](https://user-images.githubusercontent.com/60341565/141510832-e525d96e-eabb-4e59-ae35-b7ff1747a4be.png)

Характеристики виртуальной машины по умолчанию
![image](https://user-images.githubusercontent.com/60341565/141511269-50a0c136-6a1b-411e-bd0b-484803d5b4ca.png)

Задание 6.

Чтобы добавить оперативной памяти или ресурсов процессора виртуальной машине прописываем в файле Vagrantfile:

config.vm.provider "virtualbox" do |v|
  v.memory = 1024
  v.cpus = 2
end

Задание 7.

![image](https://user-images.githubusercontent.com/60341565/141514211-be594e29-c674-4e81-ae76-29a11ccc752c.png)

Задание 8.

  Длина журнала history можно задать переменной HISTSIZE, строка 1178, а HISTFILESIZE - максимальное количество команд хранящихся в файле истории, строка 1155.
  ignoreboth это сокращение для 2х директив ignorespace and ignoredups, 
    ignorespace - не сохранять команды начинающиеся с пробела, 
    ignoredups - не сохранять команду, если такая уже имеется в истории

Задание 9.

{} - зарезервированные слова, список, в т.ч. список команд команд в отличии от "(...)" исполнятся в текущем инстансе, 
используется в различных условных циклах, условных операторах, или ограничивает тело функции, 
В командах выполняет подстановку элементов из списка , если упрощенно то  цикличное выполнение команд с подстановкой 
строка 343

Задание 10.

touch {000001..100000} - создаст в текущей директории соответствующее число файлов
300000 - создать не удасться, это слишком дилинный список аргументов
выдает ошибку -bash: /usr/bin/touch: Argument list too long

Задание 11.

проверяет условие у -d /tmp и возвращает ее статус (0 или 1), выдает 1 (True) если каталог существует, 0 (False) если нет.

Задание 12.

   vagrant@vagrant:~$ mkdir /tmp/new_path_dir/
   
   vagrant@vagrant:~$ cp /bin/bash /tmp/new_path_dir/
   
   vagrant@vagrant:~$ type -a bash
   
   bash is /usr/bin/bash
   
   bash is /bin/bash
   
   vagrant@vagrant:~$ PATH=/tmp/new_path_dir/:$PATH
   
   vagrant@vagrant:~$ type -a bash
   
   bash is /tmp/new_path_dir/bash
   
   bash is /usr/bin/bash
   
   bash is /bin/bash

Задание 13.

  at - команда запускается в указанное время (в параметре)
  batch - команда для выполнения разовой задачи, когда средняя загрузка опускается ниже 0,8
