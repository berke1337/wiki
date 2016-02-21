# MySQL Cheat Sheet

taken from https://en.wikibooks.org/wiki/MySQL/CheatSheet

### Connect/Disconnect
```
mysql -h <host> -u <user> -p
```

### Backup and Restore
Hint: Backup the different databases into different files to make selective restoring possible.
```
mysqldump --databases db1 db2 db3 --user=root --password > all_databases.sql
mysql -uroot -p < all_databases.sql
```

### Browsing
```PLpgSQL
SHOW DATABASES;
SHOW TABLES;
USE mbase; #switch to the database named mbase
```

### Query
```
SELECT * FROM table
SELECT field1, field2, ... FROM table1, table2, ... WHERE condition
```

### Create / delete / select / alter database
```
CREATE DATABASE mabase CHARACTER SET utf8
DROP DATABASE mabase
```

### Privileges
```
CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON base.* TO 'user'@'localhost' IDENTIFIED BY 'password';
GRANT SELECT, INSERT, DELETE ON base.* TO 'user'@'localhost' IDENTIFIED BY 'password'; #the .* is mandatory!
REVOKE ALL PRIVILEGES ON base.* FROM 'user'@'host'; -- one db permission only
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'user'@'host'; -- all permissions

SET PASSWORD = PASSWORD('new_pass')
SET PASSWORD FOR 'user'@'host' = PASSWORD('new_pass')
SET PASSWORD = OLD_PASSWORD('new_pass')

DROP USER 'user'@'host'
```


### Reset root password
```
$ service mysql stop
$ mysqld_safe --skip-grant-tables &
$ mysql # on another terminal
mysql> UPDATE mysql.user SET password=PASSWORD('nouveau') WHERE user='root';
## Kill mysqld_safe from the terminal, using Control + \
$ /etc/init.d/mysql start
```

### Repair tables after unclean shutdown
```
mysqlcheck --all-databases
mysqlcheck --all-databases --fast
```

### Data Manipulation
```
INSERT INTO table1 (field1, field2, ...) VALUES (value1, value2, ...)

LOAD DATA INFILE '/tmp/mydata.txt' INTO TABLE table1
FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"' ESCAPED BY '\\'

DELETE FROM table1 / TRUNCATE table1
DELETE FROM table1 WHERE condition
  ```
