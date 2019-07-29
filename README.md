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
run the command

```bash   
ansible-playbook main.yml
```
The playbook will first install nginx package in all VMs.
The function "delegate_to" is used to select the lb from the invetory to configure the nginx configuration to add the specified template.

```bash 
delegate_to: lb
```
## nginx lb configuration

```bash 
upstream web_backend { 
 # Uncomment for the Least Connected load balancing method: # least_conn;  
 # The default load balancing method is round robin. Since, we didn't specified any methods the configuration will chose roundrobin
 server '{{server_1}}'; 
 server '{{server_2}}'; 
}
```

Once the configuartion is completed the playbook will restart.

The following function is used to check whether there is any  configuration changes is done

```bash 
 register: content_status
```
If there are any chnages triggerd in the configuration the nginx will restart using the following condition

```bash 

 when: 
       - content_status.changed == true 
       - ansible_nodename == "lb01"
```

