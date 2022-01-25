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

Задание 4.
========================

Выбираем провайдера 

    root@igor-X202EP:/home/igor# export VAGRANT_DEFAULT_PROVIDER=virtualbox

Скачиваем нужный нам образ

    root@igor-X202EP:/home/igor# vagrant box add bento/ubuntu-20.04 --provider=virtualbox --force
    ==> box: Loading metadata for box 'bento/ubuntu-20.04'
    box: URL: https://vagrantcloud.com/bento/ubuntu-20.04
    ==> box: Adding box 'bento/ubuntu-20.04' (v202112.19.0) for provider: virtualbox
    box: Downloading: https://vagrantcloud.com/bento/boxes/ubuntu-20.04/versions/202112.19.0/providers/virtualbox.box
    box: Download redirected to host: vagrantcloud-files-production.s3-accelerate.amazonaws.com
    ==> box: Successfully added box 'bento/ubuntu-20.04' (v202112.19.0) for 'virtualbox'!

Выбираем образ

    root@igor-X202EP:/home/igor# vagrant box list
    bento/ubuntu-20.04 (virtualbox, 202112.19.0)

Выбираем директорию под вагрант, инициализируем

    vagrant init
   
Изменяем Vagrantfile

    # -*- mode: ruby -*-

    ISO = "bento/ubuntu-20.04"
    NET = "192.168.1."
    DOMAIN = ".netology"
    HOST_PREFIX = "server"
    INVENTORY_PATH = "../ansible/inventory"

    servers = [
      {
    :hostname => HOST_PREFIX + "1" + DOMAIN,
    :ip => NET + "140",
    :ssh_host => "20011",
    :ssh_vm => "22",
    :ram => 1024,
    :core => 1
      }
    ]

    Vagrant.configure(2) do |config|
      config.vm.synced_folder ".", "/vagrant", disabled: false
      servers.each do |machine|
      config.vm.define machine[:hostname] do |node|
      node.vm.box = ISO
      node.vm.hostname = machine[:hostname]
      node.vm.network "public_network", ip: machine[:ip], bridge: "br0"
      node.vm.network :forwarded_port, guest: machine[:ssh_vm], host: machine[:ssh_host]
      node.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
        vb.customize ["modifyvm", :id, "--cpus", machine[:core]]
        vb.name = machine[:hostname]
      end
      node.vm.provision "ansible" do |setup|
        setup.inventory_path = INVENTORY_PATH
        setup.playbook = "../ansible/provision.yml"
        setup.become = true
        setup.extra_vars = { ansible_user: 'vagrant' }
        end
     end
    end
    end
    
Изменяем ansible.cfg

    [defaults]
    inventory=./inventory
    deprecation_warnings=False
    command_warnings=False
    ansible_port=22
    interpreter_python=/usr/bin/python3
    
Изменяем /etc/ansible/inventory

    [nodes:children]
    manager

    [manager]
    server1.netology ansible_host=127.0.0.1 ansible_port=20011 ansible_user=vagrant
    
Изменяем /etc/ansible/provision.yml

    ---

      - hosts: nodes
        become: yes
        become_user: root
        remote_user: vagrant

        tasks:
          - name: Create directory for ssh-keys
            file: state=directory mode=0700 dest=/root/.ssh/

          - name: Adding ed25519-key in /root/.ssh/authorized_keys
            copy: src=~/.ssh/id_ed25519.pub dest=/root/.ssh/authorized_keys owner=root mode=0600
            ignore_errors: yes

          - name: Checking DNS
            command: host -t A google.com

          - name: Installing tools
            apt: >
              package={{ item }}
              state=present
              update_cache=yes
            with_items:
              - git
              - curl

          - name: Installing docker
            shell: curl -fsSL get.docker.com -o get-docker.sh && chmod +x get-docker.sh && ./get-docker.sh

          - name: Add the current user to docker group
            user: name=vagrant append=yes groups=docker
            
Запускаем Vagrant 

    vagrant up
    vagrant ssh
    
Устанавливаем  docker 

    curl -sSL https://get.docker.com/ | sh

Проверяем docker ps

    root@server1:/home# docker ps
    CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
