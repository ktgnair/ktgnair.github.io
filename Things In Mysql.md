**[Home](https://ktgnair.github.io/) / [Assignment 1](https://ktgnair.github.io/) / [Assignment 2](https://ktgnair.github.io/Assignment 2) / [Rules For Code](https://ktgnair.github.io/Rules For Code) / [Git Tutorials](https://ktgnair.github.io/Basic Github) / [Database](https://ktgnair.github.io/Database) / [Export Mysql](http://ktgnair.github.io/ExportMysql) / [How to disable root for ssh](http://ktgnair.github.io/DisableRoot)**  

**There are some things which are simple but yet unknown to us as they are not needed to us in our day to day basis.**  

**So today i am going write keeping the above in context which i felt was true in my case.**  

*__To check which port is used by MySQL.__*   

Type the following in your terminal.  
```  
<b>INPUT:</b>   
sudo netstat -tlnp  
```  

```  
<b>OUTPUT:</b>  
Active Internet connections (only servers)  
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name     
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      1019/mysqld           
tcp        0      0 0.0.0.0:5355            0.0.0.0:*               LISTEN      965/systemd-resolve  
tcp        0      0 0.0.0.0:5900            0.0.0.0:*               LISTEN      1821/vino-server    
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      753/cupsd           
tcp6       0      0 :::5355                 :::*                    LISTEN      965/systemd-resolve   
tcp6       0      0 :::5900                 :::*                    LISTEN      1821/vino-server    
tcp6       0      0 ::1:631                 :::*                    LISTEN      753/cupsd           
```  

Here first line's last column tells us that it's MySQL,  
Check the local address of the line it will and it will tell us that the port no 3306 is being used.    

*__To find all the privileges given to a user in MySQL.__*  

To know the privileges of a user login to your MySQL with the user whose privileges you want to know and type this.  
```  
<b>INPUT:</b>    
show grants;  
```  

```  
<b>OUTPUT:</b>  
Grants for root@localhost     
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION   
GRANT PROXY ON ''@'' TO 'root'@'localhost' WITH GRANT OPTION    
```  

The above output tells you that all the privileges has been given to the user "root".  

*__How to create a new user in MySQL and give privileges.__*  

I will guide you to the right path, just follow the steps below.  
**To create a new user.**  

First login to your MySQL, i am assuming that you have at present only one user in Mysql which is root having all privileges.  

Now type the following into your MySQL terminal  
```  
SYNTAX:  
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'newpasswordforthisuser';  

EXAMPLE:  
mysql> CREATE USER 'os'@'localhost' IDENTIFIED BY 'Osmysql@1';   
Query OK, 0 rows affected (0.02 sec)  
```  

Now if you are lucky you might get an error.  

What are you gone mad lucky for what an error?  --- Your thoughts   
But the answer should be Yes,because if you get an error then you will know something new and also indirectly got the privilege to solve that.    

This is the error that i got and also i will explain how to solve for this error.  
 ```  
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements  
```  

Going to the solution  

It means you need to follow the criteria that has been set for passwords.  

But how are we now going to find what criteria has been set by MySQL.  

Simple-  Run this command   
```  
INPUT:  
mysql> show variables like 'validate_password%';  
```  

```  
OUTPUT: 
![Password Variable](/images/db/passwordVariables.png)  
```  

The above output tells you that the minimum password length should be 8.  
It should contain one uppercase, number and a special character.  

After understanding this just type again the **CREATE USER** command with right password and you will be able to create new user.  

**To grant all privileges to a user.**  

Type this  
```  
INPUT:  
mysql> GRANT ALL PRIVILEGES ON *.* TO 'os'@'localhost';  

OUTPUT:  
Query OK, 0 rows affected (0.00 sec)  
```  

Now save the changes of the privileges.  
```  
INPUT:  
mysql> FLUSH PRIVILEGES;  

OUTPUT:  
Query OK, 0 rows affected (0.00 sec)  
```  

Now check whether changes have been made   

Just quit from the current MySQL.  
```  
mysql> QUIT  
Bye  
```  

Login using newly created user or using the user to whome you have set the privileges just now.  
```  
INPUT:  
mysql -u os -p  
Enter password:(NEW USER PASSWORD)  

OUTPUT:  
Welcome to the MySQL monitor.  Commands end with ; or \g.  
Your MySQL connection id is 7  
Server version: 5.7.21-0ubuntu0.17.10.1 (Ubuntu)  

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.  

Oracle is a registered trademark of Oracle Corporation and/or its  
affiliates. Other names may be trademarks of their respective  
owners.  
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.  
```  

Now check the privileges  
```  
INPUT:  
mysql> show grants;  

OUTPUT:  

Grants for os@localhost  
GRANT ALL PRIVILEGES ON *.* TO 'os'@'localhost' 
```  
This will show you that you have been successful in applying the previous steps.  

*__How to restart the MySQL__*  

```  
 INPUT:  
 service mysql restart  
 
 It will ask you for MySQL password just type it and you are good to go.  
 ```  
 
