#### varfromfile.yml

### You can read variables from a file via playbook or from command line

```sh
$ ansible playbook varfromfile.yml -e "@ company.lst"
-e means extra vars
```
