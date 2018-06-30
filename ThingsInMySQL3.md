**[Things in Mysql](http://ktgnair.github.io/Things In Mysql) / [Check Port No](http://ktgnair.github.io/ThingsInMySQL1) / [Check user privileges](http://ktgnair.github.io/ThingsInMySQL2) / [Different operations in MySQL](http://ktgnair.github.io/ThingsInMySQL4) / [Reset root password](http://ktgnair.github.io/ThingsInMySQL5)**  

*__How to create a new user in MySQL and give privileges.__*   

I will guide you to the right path, just follow the steps below.  
**To create a new user.**  

First login to your MySQL root user.  

Now type the following into your MySQL terminal  
```  
SYNTAX:  
CREATE USER 'type_your_new_user_name'@'localhost' IDENTIFIED BY 'type_new_password_for_new_user';  

EXAMPLE:  
mysql> CREATE USER 'os'@'localhost' IDENTIFIED BY 'Osmysql@1';   
Query OK, 0 rows affected (0.02 sec)  
```  

Now there is a chance that you will get an error which i faced while creating the user.  

This is the error that i got but don't worry i will explain how to solve this error.  
```  
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements  
```  

**The Solution**  

It means you need to follow the criteria that has been set for passwords.  

But how are we now going to find what criteria has been set by MySQL?    

Simple-  Run this command   
```  
INPUT:  
mysql> show variables like 'validate_password%';  
```  
 
OUTPUT:(in my case) 
> ![Password Variable](/images/db/passwordVariables.png)    

The above output tells you that the minimum password length should be 8.  
It should contain one uppercase, number and a special character.  

After understanding this just type again the **CREATE USER** command with right password and you will be able to create new user.  

**To grant all privileges to an user.**  

Type this  
```  
INPUT:  
mysql> GRANT ALL PRIVILEGES ON *.* TO 'os'@'localhost';  

OUTPUT:  
Query OK, 0 rows affected (0.00 sec)  
```  
Here the 1st '*' specifies giving permissions to all the databases and the 2nd is giving permissions to all the tables.  
You can give permissions to specfic database or table by specifing the names accordingly instead of '*' marks.  
By running this command we are giving the new user all the root access i.e the new user can perform all the tasks that can be performed across any database and any tables.  
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

In most cases it is not right to give all privileges to an user, so to give specific privileges type this command  
```    
mysql> GRANT type_of_permission ON database_name.table_name TO 'name_of_the_new_user'@'localhost';  
```  
and follow the rest of the procedure as mentioned above.  
