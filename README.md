Role Name
=========
kmish.orlando_iza

Requirements Client
-------------------
Have docker-compose installed
used version in to proyect
docker-compose version 1.23.1, build b02f1306
## IMPORTANT ##
## Install default ##
change variable of file 
 - install_wordpress.yml (hosts: your_server_name)

## Install Custom one server or list server ##
change variable of files
 - install_wordpress.yml (hosts: all)
 - hostname_install      (your_server_name or list hostname)
## The command validates if your server has any containers running, it requests the credentials manually and does not use RSA key, additionally it uses the inventory of hostname_install file, do not forget to put the user you will use and the correct path of hostname_install file.
ansible all -a "sudo docker ps" -u USER_NAME -i /PATH_OF_ROLE/kmish.orlando_iza/hostname_install -kK

## The command validates syntax
ansible-playbook install_wordpress.yml --syntax-check -i /PATH_OF_ROLE/kmish.orlando_iza/hostname_install

## Run ejecution
ansible-playbook install_wordpress.yml -u USER_NAME -i /PATH_OF_ROLE/kmish.orlando_iza/hostname_install -kK

## The command validates containers running wordpress and mysql
ansible all -a "sudo docker ps" -u USER_NAME -i /PATH_OF_ROLE/kmish.orlando_iza/hostname_install -kK

## Validate wordpress installation on client
BROWSER

http://YOURS_IP_CLIENT:8080 


Role Variables
--------------
Variables, Config and credential of wordpress and mysql in the file: docker-compose.yml

Dependencies
------------
The user to be used in the clients must have installation, reading and writing permissions.


Example Playbook
----------------

    - hosts: your_server_name
      roles:
         - kmish.orlando_iza

License
-------

BSD

##Project Outputs

[root@ansible kmish.orlando_iza]# pwd
/root/.ansible/roles/kmish.orlando_iza
[root@ansible kmish.orlando_iza]# ansible all -a "sudo docker ps" -u orlando -i /root/.ansible/roles/kmish.orlando_iza/hostname_install -kK
SSH password:
BECOME password[defaults to SSH password]:
[WARNING]: Consider using 'become', 'become_method', and 'become_user' rather than running sudo
192.168.126.136 | CHANGED | rc=0 >>
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@ansible kmish.orlando_iza]# ansible-playbook install_wordpress.yml -vv -u orlando -i /root/.ansible/roles/kmish.orlando_iza/hostname_install -kK
ansible-playbook 2.9.11
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3.6/site-packages/ansible
  executable location = /usr/bin/ansible-playbook
  python version = 3.6.8 (default, Dec  5 2019, 15:45:45) [GCC 8.3.1 20191121 (Red Hat 8.3.1-5)]
Using /etc/ansible/ansible.cfg as config file
SSH password:
BECOME password[defaults to SSH password]:
statically imported: /root/.ansible/roles/kmish.orlando_iza/tasks/configure.yml
statically imported: /root/.ansible/roles/kmish.orlando_iza/tasks/install.yml

PLAYBOOK: install_wordpress.yml **********************************************************************************************************************************************************
1 plays in install_wordpress.yml

PLAY [Install Wordpress] *****************************************************************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************************************************
task path: /root/.ansible/roles/kmish.orlando_iza/install_wordpress.yml:2
ok: [192.168.126.136]
META: ran handlers

TASK [kmish.orlando_iza : Create directory for copy file docker-compose.yml] *************************************************************************************************************
task path: /root/.ansible/roles/kmish.orlando_iza/tasks/configure.yml:2
changed: [192.168.126.136] => {"changed": true, "gid": 999, "group": "systemd-coredump", "mode": "0775", "owner": "systemd-coredump", "path": "/home/docker/wordpress/mysql-data", "size": 4096, "state": "directory", "uid": 999}

TASK [kmish.orlando_iza : Copy wordpress and mysql configuration file] *******************************************************************************************************************
task path: /root/.ansible/roles/kmish.orlando_iza/tasks/configure.yml:10
ok: [192.168.126.136] => {"changed": false, "checksum": "d5600ff0827841eeeb5e5a234f367d567ae033cb", "dest": "/home/docker/wordpress/docker-compose.yml", "gid": 0, "group": "root", "mode": "0644", "owner": "root", "path": "/home/docker/wordpress/docker-compose.yml", "size": 534, "state": "file", "uid": 0}

TASK [kmish.orlando_iza : Install Wordpress and Mysql according to the file docker-compose.yml] ******************************************************************************************
task path: /root/.ansible/roles/kmish.orlando_iza/tasks/install.yml:2
changed: [192.168.126.136] => {"ansible_job_id": "721601000503.54105", "changed": true, "finished": 0, "results_file": "/root/.ansible_async/721601000503.54105", "started": 1}
META: ran handlers
META: ran handlers

PLAY RECAP *******************************************************************************************************************************************************************************
192.168.126.136            : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[root@ansible kmish.orlando_iza]# ansible all -a "sudo docker ps" -u orlando -i /root/.ansible/roles/kmish.orlando_iza/hostname_install -kK
SSH password:
BECOME password[defaults to SSH password]:
[WARNING]: Consider using 'become', 'become_method', and 'become_user' rather than running sudo
192.168.126.136 | CHANGED | rc=0 >>
CONTAINER ID        IMAGE                     COMMAND                  CREATED             STATUS              PORTS                  NAMES
bf0d5db95595        wordpress:php7.2-apache   "docker-entrypoint.s…"   About an hour ago   Up 10 seconds       0.0.0.0:8080->80/tcp   wordpress_wordpress_1
328b515b56b8        mysql:8.0.13              "docker-entrypoint.s…"   About an hour ago   Up 11 seconds       3306/tcp, 33060/tcp    wordpress_mysql_1
[root@ansible kmish.orlando_iza]#


