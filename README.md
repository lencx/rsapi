# RSAPI

## MySQL

* [Download](https://dev.mysql.com/downloads/mysql)

```bash
# mac
# .zshrc or .bash_profile
PATH=$PATH:/usr/local/mysql/bin
```

```bash
# login
mysql -u root -p

# create the user
mysql> CREATE USER 'lencx'@'%' IDENTIFIED BY 'test123';
Query OK, 0 rows affected (0.05 sec)

# create the database
mysql> CREATE DATABASE rsapi;
Query OK, 1 row affected (0.01 sec)

# set up permissions
mysql> GRANT ALL PRIVILEGES ON rsapi.* TO lencx;
Query OK, 0 rows affected (0.00 sec)

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| rsapi              | # create
| sys                |
+--------------------+
5 rows in set (0.00 sec)

# or `quit`
mysql> exit
```
