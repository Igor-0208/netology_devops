Задание 1.
===

- Какой тип инфраструктуры будем использовать для этого проекта: изменяемый или не изменяемый?

Неизменяемый. В ТЗ написано что команда использовала Docker, Packer, Terraform.

- Будет ли центральный сервер для управления инфраструктурой?

Инструменты, которые можно использовать для оркестрации, не требуют сервера (Packer, Terraform, Ansible), но конфигурации будут храниться в git.

- Будут ли агенты на серверах?

Нет. Можно использовать ssh.

- Будут ли использованы средства для управления конфигурацией или инициализации ресурсов?

Да, Terraform.

- Какие инструменты из уже используемых вы хотели бы использовать для нового проекта?

Packer, Terraform, Docker, Kubernetes, Ansible.

- Хотите ли рассмотреть возможность внедрения новых инструментов для этого проекта?

В дальнейшем можно заменить `TeamCity` на `GitLab CI/CD`. `Kubernetes` можно заменить `Docker`. У `GitLab CI/CD` и `Kubernetes` больше сообщество и много конфигураций.

Задание 2.
===

    root@igor-X202EP:/home/igor# terraform -v
    Terraform v1.1.6
    on linux_amd64

    Your version of Terraform is out of date! The latest version
    is 1.1.7. You can update by downloading from https://www.terraform.io/downloads.html
    root@igor-X202EP:/home/igor# 
    
Задание 3.
===

        root@igor-X202EP:/# terraform12 -v
        Terraform v0.12.14

        Your version of Terraform is out of date! The latest version
        is 1.1.7. You can update by downloading from https://www.terraform.io/downloads.html
        root@igor-X202EP:/# terraform13 -v
        Terraform v0.13.7

        Your version of Terraform is out of date! The latest version
        is 1.1.7. You can update by downloading from https://www.terraform.io/downloads.html
        root@igor-X202EP:/# 
