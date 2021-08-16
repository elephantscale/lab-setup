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

```

Installing Ansible on Linux and FreeBSD
The following are some examples showing how you might install Ansible on Ubuntu:
Installing Ansible on Ubuntu: To install the latest version of the Ansible control machine on Ubuntu, the [apt] packaging tool makes it easy using the following commands:
Ansible has been installed already using apt-get. Below instructions are for information only.
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible $ sudo apt-get install ansible
Installing Ansible via the Python package manager (pip): To install Ansible via [pip], use the following command:
pip3 install ansible
Now that you have installed Ansible using your preferred method, you can run the [ansible] command as before, and if all has gone according to plan, you will see output similar to the following:
$ ansible --version ansible 2.9.6
config file = None
configured module search path = ['/Users/james/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
ansible python module location = /usr/local/Cellar/ansible/2.9.4_1/libexec/lib/python3.8/site-packages/ansible
executable location = /usr/local/bin/ansible
python version = 3.8.1 (default, Dec 27 2019, 18:05:45) [Clang 11.0.0 (clang- 1100.0.33.16)]
If you want to update your Ansible version, [pip] makes it easy via the following command:
pip3 install ansible --upgrade
