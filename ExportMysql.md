**[Home](https://ktgnair.github.io/) / [Assignment 1](https://ktgnair.github.io/Assignment 1) / [Assignment 2](https://ktgnair.github.io/Assignment 2) / [Rules For Code](https://ktgnair.github.io/Rules For Code) / [Git Tutorials](https://ktgnair.github.io/Basic Github) / [Database](https://ktgnair.github.io/Database) / [How to disable root for ssh](http://ktgnair.github.io/DisableRoot) / [Things in Mysql](http://ktgnair.github.io/Things In Mysql) / [Issues during Tomcat](http://ktgnair.github.io/Tomcat_Issues)**  


**How to transfer mysql database from localhost to remote server**  

To understand how to do this the first step is to create a simple database(in my case its ClientManagement) and some tables with data in it.  

> **FROM YOUR LOCALHOST**    

* Now you need to create a backup file of your database which you want to copy to your remote server.  

For doing the above thing you will be using a mysql command i.e mysqldump.  
It transfers or dumps mysql databases from one mysql server to another mysql server.  

This is the syntax 
```  
mysqldump -u root -p 'Name of your database you want to dump' > 'Backup file name'.out  
```  

Example:  

**mysqldump -u root -p ClientManagement > ClientManagement.out**  

After that you will be asked for password  

**Enter password:(database password of you localhost)**   

* Copy that backup file to your remote server  

We will use scp for coping files. **scp** stands for secure copy which means you will be transferring the files using ssh connection.  
Using ssh means that the connection will ne encrypted and it is a sucure way to transfer files.  

This is the syntax for transferring files using scp  
```
scp 'Backed up file name' 'Remote server name and address':'The location where you want to store in remote server'  
```  

Example:  

**scp ClientManagement.out jenkins@188.166.174.63:/home/jenkins**  

Enter your password of remote server.  
jenkins@188.166.174.63's password:  

After that this is what you will get on your terminal.    
ClientManagement.out                          100% 7504    35.7KB/s   00:00     


> **FROM REMOTE SERVER**  

* Now that we have copied the file from localhost to our remote server, lets login to our remote server and do the following.  
- [x] Check whether the file has been copied or not.  
- [x] Create a database in the remote server mysql.  
- [x] Copy the backup file from remote server to remote server mysql.  
- [x] Check whether the database has been copied in mysql.  

* Log in to your remote server.  

```  
ssh jenkins@188.166.174.63  
jenkins@188.166.174.63's password:  
```  

* List out the files to see whether the copied file exists in that location.  

```  
ls  
```  
You will see your file here if its copied.  
```  
ClientManagement.out  
```  

* Create a database in your remote server mysql.  

I am creating a database named ClientManagement.  

```  
mysqladmin --user=root --password create ClientManagement  
Enter password:(your mysql password)   
```  

* Copy the file in your remote mysql server.  

Copy ClientManagement.out file which you have on your remote server into mysql server.  

```  
mysql -u root -p ClientManagement < ClientManagement.out   
Enter password: (your mysql password)   
```  
Where the 'ClientManagement' is your database name.  

* Check whether the database has been copied in your mysql.   

```  
mysql -u root -p  
Enter password:(your mysql password)  

Welcome to the MySQL monitor.  Commands end with ; or \g.  
Your MySQL connection id is 21   
Server version: 5.7.21 MySQL Community Server (GPL)  

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.  

Oracle is a registered trademark of Oracle Corporation and/or its  
affiliates. Other names may be trademarks of their respective  
owners.  

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.  
```  

```  
mysql> show databases;  
+--------------------+  
| Database           |  
+--------------------+  
| information_schema |  
| ClientManagement   |  
| mysql              |  
| performance_schema |  
| sys                |  
+--------------------+  
```  

```  
mysql> use ClientManagement;  
Reading table information for completion of table and column names  
You can turn off this feature to get a quicker startup with -A  

Database changed  
```  

```  
mysql> show tables;  
+----------------------------+  
| Tables_in_ClientManagement |  
+----------------------------+  
| COMPANY                    |  
| COMPANY_CONTACTS           |   
| COMPNAY_CONTACTS_BKP       |  
| TICKETS                    |  
+----------------------------+  
```  
This proves that you have been able to successfully export the database from your localhost to remote server.  
