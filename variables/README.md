#### varfromfile.yml

### You can read variables from a file via playbook or from command line

```sh
$ ansible playbook varfromfile.yml -e "@ company.lst"
-e means extra vars
```

## OUTPUT


```sh

[ansible@ip-172.28.35.54 variable]$ vi company.lst
[ansible@ip-172.28.35.54 variable]$ ls
company.lst  varfromfile.yml  variable.yml
[ansible@ip-172.28.35.54 variable]$ ansible-playbook varfromfile.yml -e "@company.lst"

PLAY [ec2] *************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************
[WARNING]: Platform linux on host 172.28.32.65 is using the discovered Python interpreter at /usr/bin/python, but future installation of another Python interpreter could change this. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information.
ok: [172.28.35.54]

TASK [create company list] *********************************************************************************************************************************************************************
changed: [172.28.35.54]

TASK [add names] *******************************************************************************************************************************************************************************
changed: [172.28.35.54] => (item=Infosys)
changed: [172.28.35.54] => (item=TCS)
changed: [172.28.35.54] => (item=CTS)
changed: [172.28.35.54] => (item=Accenture)
changed: [172.28.35.54] => (item=Reliance)
changed: [172.28.35.54] => (item=LAndT)
changed: [172.28.35.54] => (item=PAndG)
changed: [172.28.35.54] => (item=Hero Honda)

PLAY RECAP *************************************************************************************************************************************************************************************
172.28.35.54              : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@ip-172.28.35.54 variable]$
```
