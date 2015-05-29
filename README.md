# ansible-mysql-replication
##Clone
Clone this repository.
$ git clone https://github.com/potgieterdl/ansible-mysql-replication.git
$ cd ansible-mysql-replication

##Setup
###Mysql Hosts
Ensure you have configured your hosts file with the following groups [vi /etc/ansible/hosts]
```yml
[mysql-master]
10.0.93.9

[mysql-slave]
10.0.93.10

[mysql:children]
mysql-master
mysql-slave
```
###Edit Group Vars
Edit group_vars/all
```
mysql_server_port: 6033
mysql_repl_db: taxi
mysql_repl_user: repl_user
replicate_databases:
  - taxi
replicate_ignore_tables:
  - taxi.hoge
```

vi group_vars/mysql-master
```
mysql_repl_role: mysql-master
```
vi group_vars/mysql-slave
```
mysql_repl_role: mysql-slave
```
ansible-vault create group_vars/mysql/passwd [specify password for file]
```
mysql_root_pass: Summer1234
```

##Execute
$ ansible-playbook site.yml --ask-vault-pass

** Specify the password used for the passpw file, so ansible can decrypt and use the var mysql_root_pass
