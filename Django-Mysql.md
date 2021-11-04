# Setup MySQL servers and database for Sales Tracking


# Mysql Installation
https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-18-04
https://medium.com/@omaraamir19966/connect-django-with-mysql-database-f946d0f6f9e3


```
    sudo apt update
    sudo apt install mysql-server
    sudo mysql_secure_installation
	sudo apt install mysql-client

```

```
	sudo apt install gcc
	sudo apt install python3-dev
	sudo apt install libmysqlclient-dev
```

activate env before pip install mysqlclient

```
	pip install mysqlclient
```

## Sudo to Mysql as root

```
	sudo mysql
```


## Switch password authentication to native

>In order to use a password to connect to MySQL as root, you will need to switch its authentication method from auth_socket to mysql_native_password.

Check the current method used:

```
	mysql>

	SELECT user,authentication_string,plugin,host FROM mysql.user;

	+------------------+-------------------------------------------+-----------------------+-----------+
	| user             | authentication_string                     | plugin                | host      |
	+------------------+-------------------------------------------+-----------------------+-----------+
	| root             |                                           | auth_socket           | localhost |
	| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
	| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
	| debian-sys-maint | *BCCF31E8BD5218560B6D2FDF28EB089B2630A5BA | mysql_native_password | localhost |
	+------------------+-------------------------------------------+-----------------------+-----------+
	4 rows in set (0.00 sec)

```

Change to native method:

```
	ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'passwordqaa';

	SELECT user,authentication_string,plugin,host FROM mysql.user;


	+------------------+-------------------------------------------+-----------------------+-----------+
	| user             | authentication_string                     | plugin                | host      |
	+------------------+-------------------------------------------+-----------------------+-----------+
	| root             | *36589495D35C87F5A88913E093D0E3CD6801B00D | mysql_native_password | localhost |
	| mysql.session    | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
	| mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql_native_password | localhost |
	| debian-sys-maint | *BCCF31E8BD5218560B6D2FDF28EB089B2630A5BA | mysql_native_password | localhost |
	+------------------+-------------------------------------------+-----------------------+-----------+
	4 rows in set (0.01 sec)

```

## Create dedicate account for the database admin instead of root account

```
	CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
	GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION;
```


## Check Mysql status

```
	systemctl status mysql.service
```


## Start or Stop MySql

```
	sudo systemctl start mysql
	sudo systemctl stop mysql
```


## Create Database
Sign in with admin4crm

```
	mysql -u admin4crm -p

	CREATE DATABASE database_name CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
	CREATE DATABASE strkdb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

```


## Backup and Restore

mysqldump -u username -p database_name > database_name.sql
mysql -u username -p database_name < database_name.sql



## Configure MySQL to use UTF-8
https://www.a2hosting.com/kb/developer-corner/mysql/convert-mysql-database-utf-8#a-nameprocCurrentCharSetaDetermine-the-current-character-encoding-set

### Change database to use utf-8

ALTER DATABASE database_name CHARACTER SET utf8 COLLATE utf8_general_ci;

### Change all tables to use utf-8

First create mysql login fle.
.my.cnf

Put in content:
[client]
user=USERNAME
password="PASSWORD"

Run the Mysql command below:

mysql --database=database_name -B -N -e "SHOW TABLES;" | awk '{print "SET foreign_key_checks = 0; ALTER TABLE", $1, "CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci; SET foreign_key_checks = 1; "}' | mysql --database=database_name



## MySQL Client for Django
MySqlclient is required before python manage.py migrate can be run.
There are pre requisites before mysqlclient can be installed.

1. gcc
2. python3-dev
3. libmysqlclient-dev

```
	sudo apt install gcc
	sudo apt install python3-dev
	sudo apt install libmysqlclient-dev
```

activate env before pip install mysqlclient

```
	pip install mysqlclient
```
