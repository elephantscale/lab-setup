# Lab 1: Getting Started


In this lab, we will begin to teach you the practical skills to cover the very fundamentals of Ansible, starting with how to install Ansible. We'll then look at node requirements and how to validate your Ansible installation.

In this lab, we will cover the following topics:
 * Installing and configuring Ansible 
 * Understanding your Ansible installation


## Login

SSH to the machine that your instructor has provided you. You login name is `ubuntu` and password will be provided by your instructor.


# Getting the Labs

You can download the labs as follows:

```bash
wget https://elephantscale-public.s3.amazonaws.com/labs/ansible-course.zip
```

You can proceed this lab as follows:

```bash
cd ~/ansible-course/Lab_1
```


## Confirm passwordless ssh


(This step should not be necessary on the lab machines, but will be required if you have a vanilla ubuntu install)

You should be able to `ssh` to localhost, as follows:

```bash
ssh localhost  # you may have to type in yes when asking for a key
exit
```

If this does not work, you need to configure the key for passwordless ssh to localhost

```bash
ssh-keygen -t rsa # Press enter for each line 
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod og-wx ~/.ssh/authorized_keys 
```



## Installing Ansible

Confirm that you have ansible installed as follows

```bash
ansible --version
```

And you should get the following response:

```console

ansible 2.9.24
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/ubuntu/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.12 (default, Mar  1 2021, 11:38:31) [GCC 5.4.0 20160609]


```

If you do not have installed already,

```bash
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt-get install ansible
```


## Configuring Hosts

We are going to be creating some hosts in `/etc/hosts` file to test with ansible in our labs

First, edit (as sudo) the `/etc/hosts` file with a commmand line editor such as `vim` or `nano`.

```bash
sudo vi /etc/hosts/
```

Add the following lines to the file `/etc/hosts`

```text
127.0.0.1 web1.example.com
127.0.0.1 web2.example.com
127.0.0.1 ap1.example.com
127.0.0.1 ap2.example.com

```

Now, confirm this works by attempting to perform an ssh to each of the four machiens

```bash
ssh web1.example.com   # You may have to say "yes" when asked
exit
ssh web2.example.com   # You may have to say "yes" when asked
exit
ssh ap1.example.com   # You may have to say "yes" when asked
exit
ssh ap2.example.com   # You may have to say "yes" when asked
exit
ssh frt01.example.com   # You may have to say "yes" when asked
exit
ssh frt02.example.com   # You may have to say "yes" when asked
exit
```

## Configure ansible hosts files

We need to add our new hosts to our `/etc/ansible/hosts` file

```bash
sudo vim /etc/ansible/hosts
```

```text
[webservers]
web1.example.com
web2.example.com

[apservers]
ap1.example.com
ap2.example.com
```



## Perform a ping command

```bash
ansible webservers -m ping
```

Ignore any deprecation warnings about python 2 vs 3

You should get the following

```console
ap1.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
ap2.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}

```

## Verifying the Ansible installation
In this section, you will learn how you can verify your Ansible installation with simple ad hoc commands.

As we discussed in the previous section, we must also define an inventory for Ansible to run against. Another simple example is shown here:

These should be added to your `/etc/ansible/hosts`

```text
[frontends] 
frt01.example.com 
frt02.example.com
```
 Following are three simple examples that demonstrate ad hoc commands---they are also valuable for verifying both the installation of Ansible on your control machine and the configuration of your target hosts, and they will return an error if there is an issue with any part of the configuration:


### Ping Hosts
Ping hosts: You can perform an Ansible "ping" on your inventory hosts using the following command:
```bash
ansible frontends -i hosts -m ping
```

### Display Gathered Facts

```bash
ansible frontends -i hosts -m setup | less
```

### Filtered Gathered Facts

```bash
ansible frontends -i hosts -m setup -a "filter=ansible_distribution*"
```

Ad hoc commands are incredibly powerful, both for verifying your Ansible installation and for learning Ansible and how to work with modules as you don't need to write a whole playbook---you can just run a module with an ad hoc
command and learn how it responds. Here are some more ad hoc examples for you to consider:

# Copy a file
Copy a file from the Ansible control host to all hosts in the [frontends] group with the following command:
```bash
ansible frontends -m copy -a "src=/etc/hosts dest=/root/Desktop/hosts"
```

## Create A new directory
Create a new directory on all hosts in the [frontends] inventory group, and create it with specific ownership and permissions:

```bash
ansible frontends -m file -a "dest=/path/user1/new mode=777 owner=user1 group=user1 state=directory"
```

## Delete a Directory
Delete a specific directory from all hosts in the [frontends] group with the following command:

$ ansible frontends -m file -a "dest=/path/user1/new state=absent"

### Install apache2 package
Install the [apache2] package with [apt] if it is not already present---if it is present, do not update it. Again, this applies to all hosts in the [frontends] inventory group:

```bash
ansible frontends -m apt -a "name=apache2 state=present"
```

## Get Latest package
The following command is similar to the previous one, except that changing [state=present] to [state=latest] causes Ansible to install the (latest version of the) package if it is not present, and update it to the latest version if it is present:
```bash
ansible frontends -m apt -a "name=apache2 state=latest"
```

## Display Facts
Display all facts about all the hosts in your inventory (warning---this will produce a lot of JSON!):

```bash
ansible all -m setup
```



## Questions
1. On which operating systems can you install Ansible? (Multiple correct answers) 
   * A) Ubuntu
   * B) Fedora
   * C) Windows 2019 server 
   * D) HP-UX
   * E) Mainframe
2. Which protocol does Ansible use to connect the remote machine for running tasks? 
   * A) HTTP
   * B) HTTPS 
   * C) SSH 
   * D) TCP * 
   * E) UDP
3. To execute a specific module in the Ansible ad hoc command line, you need to use the `[-m]` option. 
   * A) True
   * B) False
