# How to run this

- Run the command

```sh 
[ansible@162-11-35-65 ~] $ ansible-playbook httpplaybook.yml
```
### This will run against all the hosts mentioned in the file
```sh 
$ ansible-playbook httpplaybook.yml limit 162-11-35-65 

- To play against a particular host
``` 

### Uninstall Httpd 

```sh
ansible ec2 -b -m yum -a "name=httpd state=absent"
```
