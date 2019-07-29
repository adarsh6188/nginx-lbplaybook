Role Name
=========

This play book is to install and configure the nginx webservers  with loadbalancing 

Requirements
------------

This requires nginx package available in the VM. Also, please make sure that the servers have connectivity with each other.


Role Variables
--------------
The variables are provided in the /vars/main.yml. This includes the backend web server IPs. If you wish to add more web serves you can provide the server details here.


Example Playbook
----------------
This play book can be run using the following steps

Got to the directory:
cd nginx-lbplaybook-master/tasks/
run the command "ansible-playbook main.yml"

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
