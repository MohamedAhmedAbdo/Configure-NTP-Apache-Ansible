# Configure Linux Machines using Ansible

## Description ## 
- USing Ansible we could configure client machines, by running those configurations in the master node

- Here, we have 2 Roles [Apache role and NTP role], each role is on github Repo
- each Role-Repo is mentioned in file **roles/requirements.yml** 
   - **Apache Role:** [Github_Repo_link](https://github.com/DinaSol/Ansible-Apache-Role.git)
      - install httpd service, enable and start it
      - copy from master node **index.html** file to  client in Path **/var/www/html/index.html**
      - allow port 80 on firewall and reload firewalld
   - **NTP Role:** [Github_Repo_link](https://github.com/DinaSol/Ansible-NTP-Role.git)
     - ensure that chrony is exist 
     - copy from master node **chrony.conf** file to  client in Path **/etc/chrony.conf**
     - enable and start chronyd service
---
## Pre-requisites:
- 2 vms centos 8
- generate ssh keys

   ```bash
     ssh-keygen
   ```
- copy public-ssh-key to the other machines
   ```bash
     ssh-copy-id 192.168.1.138
   ```
- install Ansible on Master node
  ```python
    # Update OS
       sudo yum update

    # Install python3
	    sudo yum install python3
    # Install ansible 
    	sudo yum install epel-release
        sudo yum install ansible

## :warning:  NOTE:
- In **inventories/hosts** ensure that you set the IPs of your client machines

---
## Project Folder Structure 

```python
 project
    ├── chrony.conf 
    ├── index.html
    ├── inventories
    │   └── hosts
    ├── playbook.yml
    └── roles
        └── requirements.yml

```

## Installation

1. Use the ansible-galaxy  to install Roles Repos from github.

   ```bash
    ansible-galaxy install -r roles/requirements.yml

   ```

2. Use the ansible-playbook to run **playbook.yml** .

   ```bash
    ansible-playbook playbook.yml -i inventories/hosts

   ```

***Happy Ending*** :relaxed:
