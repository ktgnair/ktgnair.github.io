**[Home](https://ktgnair.github.io/) / [Assignment 1](https://ktgnair.github.io/) / [Assignment 2](https://ktgnair.github.io/Assignment 2) / [Rules For Code](https://ktgnair.github.io/Rules For Code) / [Git Tutorials](https://ktgnair.github.io/Basic Github) / [Database](https://ktgnair.github.io/Database) / [Export Mysql](http://ktgnair.github.io/ExportMysql) / [How to disable root for ssh](http://ktgnair.github.io/DisableRoot)**  

**There are some things which are simple but yet unknown to us as they are not needed to us in our day to day basis.**  

**So today i am going write keeping the above in context which i felt was true in my case.**  

*__To check which port is used by Mysql.__*   

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

Here first line's last column tells us that it's Mysql,  
Check the local address of the line it will and it will tell us that the port no 3306 is being used.    

*__To find all the privileges given to a user in Mysql.__*  

To know the privileges of a user login to your Mysql with the user whose privileges you want to know and type this.  
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

*__How to create a new user in Mysql and give privileges.__*  

I will guide you to the right path, just follow the steps below.  

First login to your Mysql, i am assuming that you have at present only one user in Mysql which is root having all privileges.  

Now type the following into your Mysql terminal  
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

But how are we now going to find what criteria has been set by Mysql.  

Simple-  Run this command   
```  
mysql> show variables like 'validate_password%';  
```  
