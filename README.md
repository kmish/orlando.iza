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

Role Variables
--------------
## Variables, Config and credential of wordpress and mysql in the file: docker-compose.yml
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

