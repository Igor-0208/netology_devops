Задание 1.
=====================

Основные преимущества IaaC:

  Ускорение производства и вывода продукта на рынок за счет автоматизации.
  
  Стабильность среды и устранение дрейфа конфигураций.
  
  Быстрая и эффективная разработка

Главное преимущество применения IaaC - Идемпоте́нтность. При любом повторном выполнении мы получим идентичный результат.

Задание 2.
====================

Ansible отличается простотой использования, имеет безагентную архитектуру (не требует установки агента/клиента на целевую систему) и YAML-подобный DSL, написана на Python и легко расширяется за счет модулей.

Push надёжней, т.к. централизованно управляет конфигурацией и исключает ситуации, когда кто-то что-то исправил напрямую на сервере и не отразил в репозитории - это может потеряться или создавать непредсказуемые ситуации.

Задание 3.
==================

    igor@igor-X202EP:~$ vagrant --version
    Vagrant 2.2.6
    igor@igor-X202EP:~$ ansible --version
    ansible 2.9.6
    config file = /etc/ansible/ansible.cfg
    configured module search path = ['/home/igor/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
    ansible python module location = /usr/lib/python3/dist-packages/ansible
    executable location = /usr/bin/ansible
    python version = 3.8.10 (default, Sep 28 2021, 16:10:42) [GCC 9.3.0]
![изображение](https://user-images.githubusercontent.com/60341565/150940412-53adacb5-f08f-49ca-8c0f-bdd0744da233.png)