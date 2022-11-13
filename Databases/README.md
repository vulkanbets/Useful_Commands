

# If Using systemd init Linux system
## Ensure MariaDB Server is Running Using Systemctl:
~~~console
sudo systemctl start mariadb.service
~~~

## Check if MariaDB Service Is Running
~~~console
systemctl | grep "maria"
~~~

## Check The Status Of The MariaDB Service
~~~console
systemctl status mariadb.service
~~~
---
---
---
## 1. Database creation
```sql
mysql> CREATE DATABASE `mydb`;
```
## 2. User creation
```sql
mysql> CREATE USER 'myuser'@localhost IDENTIFIED BY 'mypassword';
```
## 3. Grant permissions to access and use the MySQL server
Only allow access from localhost (this is **the most secure and common configuration** you will use for a web application):
```sql
mysql> GRANT USAGE ON *.* TO 'myuser'@localhost IDENTIFIED BY 'mypassword';
```
To allow access to MySQL server from any other computer on the network:
```sql
mysql> GRANT USAGE ON *.* TO 'myuser'@'%' IDENTIFIED BY 'mypassword';
```
In MySQL 8 or higher we will not add the IDENTIFIED BY ‘mipassword’ part.
## 4. Grant all privileges to a user on a specific database
MySQL 5.7 and earlier versions:
```sql
mysql> GRANT ALL privileges ON `mydb`.* TO 'myuser'@localhost IDENTIFIED BY 'mypassword';
```
MySQL 8 and higher versions:
```sql
mysql> GRANT ALL ON `mydb`.* TO 'myuser'@localhost;
```
As in the previous command, if you want the user to work with the database from any location you will have to replace localhost with ‘%’.
## 5. Apply changes made
To be effective the new assigned permissions you must finish with the following command:
```sql
mysql> FLUSH PRIVILEGES;
```
## 6. Verify your new user has the right permissions
```sql
mysql> SHOW GRANTS FOR 'myuser'@localhost;     
+--------------------------------------------------------------+ 
| Grants for myuser@localhost                                  | 
+--------------------------------------------------------------+ 
| GRANT USAGE ON *.* TO 'myuser'@'localhost'                   | 
| GRANT ALL PRIVILEGES ON `mydb`.* TO 'myuser'@'localhost'     | 
+--------------------------------------------------------------+ 
2 rows in set (0,00 sec)
```
If you made a mistake at some point you can undo all the steps above by executing the following commands, taking the precaution of replacing localhost with ‘%’ if you also changed it in the previous commands:
```sql
DROP USER myuser@localhost;
DROP DATABASE mydb;
```
---
---
---

<br>

# Backup/Restoring SQL Databases
#### To restore a backup created with mysqldump, use the mysql client to import the dump, for example:
~~~bash
mysql db_name < backup-file.sql
~~~
