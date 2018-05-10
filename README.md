Etckeeper template
=========

Installs etckeeper on client+server and install gitlist on server

Requirements
------------
Centos 7

Debian 8-9

Role Variables
--------------
./group_vars/all
```
uninstall_etckeeper: false
uninstall_gitlist: false	
```
Example Playbook
----------------
```
##########gitlist###########
- hosts: gitlist-servers
  become: yes
  roles:
  - role: gitlist_server


###########etckeeper#########
- hosts: etckeeper-servers

- hosts: etckeeper-clients
  become: yes
  pre_tasks:
    - import_tasks: tasks/generate_key.yml
      when: uninstall_etckeeper == false

- hosts: etckeeper-servers
  become: yes
  roles:
  - role: etckeeper_server

- hosts: etckeeper-clients
  become: yes
  roles:
  - role: etckeeper_client
```

Author Information
------------------
sanakess