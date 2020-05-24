# RSAPI

## Quick start

```bash
# step1: install the `diesel-cli`
# order to facilitate automated database setup and migration generation
cargo install diesel_cli --no-default-features --features mysql

# step2: create the rust project
cargo init --bin rsapi

# step3: generate `.env` file(connect to our database)
echo DATABASE_URL=mysql://root:test.123@localhost:3306/rsapi > .env

# step4: creates `migrations` directory + `src/schema.rs` file
diesel setup
# (1): create user table
# migrations/xxxx_users/{down,up}.sql
diesel migration generate users

# (2): edit up.sql and down.sql files
# ...

# (3)
diesel migration run
# diesel migration redo
```

### Error

```bash
# Library not loaded
diesel setup
# dyld: Library not loaded: @rpath/libmysqlclient.21.dylib
#   Referenced from: ~/.cargo/bin/diesel
#   Reason: image not found

sudo ln -s /usr/local/mysql/lib/libmysqlclient.21.dylib /usr/local/lib/libmysqlclient.21.dylib

# Creates `migrations` directory + `src/schema.rs` file
diesel setup
# Creating migrations directory at: ~/YOUR_PATH/rsapi/migrations
# The --database-url argument must be passed, or the DATABASE_URL environment variable must be set.
```

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
Enter password:
# Welcome to the MySQL monitor.  Commands end with ; or \g.

# create the user
mysql> CREATE USER 'lencx'@'%' IDENTIFIED BY 'test123';
Query OK, 0 rows affected (0.05 sec)

# create the database
mysql> CREATE DATABASE rsapi;
Query OK, 1 row affected (0.01 sec)

# set up permissions
mysql> GRANT ALL PRIVILEGES ON rsapi.* TO lencx;
Query OK, 0 rows affected (0.00 sec)

# mysql> SHOW DATABASES;
mysql> show databases;
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

# https://stackoverflow.com/questions/3736407/mysql-server-port-number
# port number of your local host on which MySQL.
mysql> SHOW VARIABLES WHERE Variable_name = 'port';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| port          | 3306  |
+---------------+-------+
1 row in set (0.02 sec)

# delete table
mysql> drop table posts;
Query OK, 0 rows affected (0.02 sec)

mysql> show tables;
+----------------------------+
| Tables_in_rsapi            |
+----------------------------+
| __diesel_schema_migrations |
| users                      |
+----------------------------+
2 rows in set (0.00 sec)

# or `quit`
mysql> exit
```
