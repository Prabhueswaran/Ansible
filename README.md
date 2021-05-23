# Ansible
## Installing Ansible on Ubuntu

 `sudo apt install python3`

 `sudo apt install python3-pip`

 `pip3 install boto boto3 ansible`

 `sudo apt-get install ansible`

To verify the ansible version 

 `ansible --version`

![image](https://user-images.githubusercontent.com/42967535/118642599-30e53700-b7f9-11eb-9bad-48763ca34b98.png)

# Configuring hosts

Here I represent all the servers that have to be managed using Ansible as hosts. Ansible keeps track of the hosts using the inventory file ( A file with list of servers). It has the IP address/domain name of the hosts with username, password or key information to connect to the node.

All the default configurations are present in /etc/ansible/ansible.cfg file. Here you can change all the default paths if you want your own custom paths and configurations.

Now let’s disable host key checking by replacing the host_key_checking parameter to true so that Ansible won’t prompt for host key checking. 

`sed -i '/#host_key_checking = False/c\host_key_checking = True' /etc/ansible/ansible.cfg`

By default the inventory file named hosts is present in /etc/ansible/ directory. If you open the /etc/ansible/hosts you will find the sample host entries. Lets keeps this file as a backup and create our own hosts file.

Let’s create the backup of original hosts inventory file.

`sudo mv /etc/ansible/hosts /etc/ansible/hosts.original`

Create a new hosts file.

`sudo touch /etc/ansible/hosts`

```
[dev]
192.168.2.30
192.168.2.40

[dev:vars]
ansible_user=ubuntu
ansible_ssh_pass=password
ansible_ssh_private_key_file=~/ansible/sshkey.pem

[local]
127.0.0.1
```
or

```
[dev]
3.91.60.111 ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/ansible/ansible.pem
```



dev:vars parameters are applied to the servers under dev label. As we know that Ansible uses ssh for connecting to hosts. So we need to specify the username and password of those hosts. If all the servers have the same username and password, you can mention it in dev:vars label


Once added verify the connectivity using below command:

`ansible dev -m ping -i hosts`

If you have Multiple group in the host file and need to check all host group connectivity:

`ansible all -m ping -i hosts`

The out put look likes:

```
3.91.60.111 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}

```

# Playbooks

## Ansible playbook for install nginx on remote host 

```
- hosts: dev
  become: yes
  tasks:
  - name: "apt-get update"
    apt:
      update_cache: yes
      cache_valid_time: 3600

  - name: "install nginx"
    apt:
      name: ['nginx']
      state: latest
```

## To run the playbook with host file:

`ansible-playbook -i hosts nginx_install.yml`

## To copy content into remote host:
### playbook 
```
- hosts: dev
  become: yes
  tasks:
  - name: copy web content
    template:
      src: index.html
      dest: /var/www/html/
      owner: root
      group: root
      mode: '0644'
    notify: restart nginx

  handlers:
    - name: restart nginx
      service:
        name: nginx
        state: restarted
```
`ansible-playbook -i hosts copy.yml`

## To sync multiple files from source to destination:
### playbook 
```
- hosts: dev
  tasks:
  - name: "sync website"
    synchronize:
      src: site/
      dest: /var/www/html
      archive: no
      checksum: yes
      recursive: yes
      delete: yes
    become: yes
```

`ansible-playbook -i hosts sync.yml`
