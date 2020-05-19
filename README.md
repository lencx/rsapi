# RSAPI

## Quick start

```bash
# step1: install the `diesel-cli`
# order to facilitate automated database setup and migration generation
cargo install diesel_cli --no-default-features --features mysql

# step2:ss
# create the user, create the database, and set up permissions
# (1)
CREATE USER 'lencx'@'%' IDENTIFIED BY 'test123';
# (2)
CREATE DATABASE rsapi;
# (3)
GRANT ALL PRIVILEGES ON rsapi.* TO lencx;

# step3: connect to our database
export DATABASE_URL="mysql://root:test.123@localhost/rsapi"

# step4: creates `migrations` directory + `src/schema.rs` file
diesel setup
# (1)
diesel migration generate initialize
# (2)
diesel migration run
# diesel migration redo
```

### Error

```bash
# Library not loaded
diesel setup
# dyld: Library not loaded: @rpath/libmysqlclient.21.dylib
#   Referenced from: /Users/zakj/.cargo/bin/diesel
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
