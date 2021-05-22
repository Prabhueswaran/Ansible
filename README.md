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

dev:vars parameters are applied to the servers under dev label. As we know that Ansible uses ssh for connecting to hosts. So we need to specify the username and password of those hosts. If all the servers have the same username and password, you can mention it in dev:vars label
