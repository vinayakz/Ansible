# Installing Ansible

## Setup Ansible in AWS EC2 Instance
- Installation Overview
  - Enable “Extras” and “Optional” yum repos
  - Install Python 3+
  - Install Ansible
  - http://docs.ansible.com/ansible/intro_installation.html
  - Ansible manages machine over SSH protocol
  - Ansible will not add a DB, and there is no daemons to start or restart
  - Installation can be done on only one machine (Control Node) and that is enough to manage group of machines
  - Remote handling of machines does not require any installation on remote machines 
  
## Installation Steps On Control Server  
 1. Login to CentOs and switch to root user
 2.	Enable 	epel repository – 
  ```sh
  sudo yum install epel-release
  ```
 3.	```sh sudo yum install git python python-devel python-pip openssl ```
 4.	Install Ansible – ```sh sudo yum install ansible ```
 5.	Check with – ansible  --version 

### There is no need to restart in case of ansible

## Running Ansible 3 ways
1. Ad Hoc commands ansible <inventory targets> -m
2. Playbooks ansible playbook
3. Automation Framework Ansible Tower

## Examples 

```sh
ansible <inventory> <options> (use all for all)
```

```sh 
$ ansible localhost -a /bin/date  (execute the date command on remote machine and get me the output )
OUTOUT: 

>> localhost | CHANGED | rc=0 >>
>> Thu Jul 28 13:23:38 UTC 2022
```
 
 
## Checking git is install or not  

```sh
$ ansible (inventory name ex- localhost or centos)  -m yum -a "name=git state=present"
OUTPUT:

localhost | SUCCESS => {
    "ansible_facts": {
        "pkg_mgr": "yum"
    },
    "changed": false,
    "msg": "",
    "rc": 0,
    "results": [
        "git-2.37.1-1.amzn2.0.1.x86_64 providing git is already installed"
    ]
}
```
## If you want to uninstall  git 

```sh 
$ ansible (inventory name ex- localhost or centos) -b -m yum -a "name=git state=absent"
```

## Installing Apache on a remote machines part of Jenkins group in hosts file


```sh
  $ ansible Jenkins -m yum -a “name= httpd state=present” b (‘ a’ represents arguments to a
    module and ‘ b’ indicating ansible that it should execute this command as root user)
  
  Uninstalls apache
  $ ansible Jenkins -m yum -a "name= httpd state=absent" b (uninstalls apache)
    
```
## Creating a user on remote machine 
  
 ```sh
  $ ansible lab2 -b -m user -a “name=testansi” (check the home dir of target and you will
    see this users home there)
  
 - To remove the user
  $ ansible lab2 -b -m user -a “name=testansi state=absent”
 ``` 
# Ansible Gathering Information-Facts
- Facts provide specific information about a given target host
- The setup module can retrieve facts per target basis
- Facts are collected by default on playbook execution but can be set
  to no using “ gather_facts ” in
- Custom facts may be setup using facts.d directory:
  - Create / etc / facts.d directory
  - Files inside this directory should end with .fact and available to system as
    local facts
  - Files can be INI, JSON, or executables that return JSON
  - Facts are returned with ansible_local variable
  - Facts may be used in conditionals or printed using variable syntax
- From Commandline (output is JSON format)

```sh
 $ ansible ec2 -m setup -a 'filter=*ipv4*'
``` 
- In Playbook under host you can mention
  - host
  - Gather_facts : yes or no based on your need
  
## Test connection of two server in ansible 
```sh
$ ansible ec2 -m ping

172.35.87.95 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```
