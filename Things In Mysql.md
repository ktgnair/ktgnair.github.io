There are some things which are simple but yet unknown to us as they are not needed to us in our day to day basis.  

So today i am going write keeping the above in context which i felt was true in my case.  

1.  To check which port is used by Mysql.   

Type the following in your terminal.  
INPUT: sudo netstat -tlnp  

OUTPUT:  
Active Internet connections (only servers)  
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name     
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      1019/mysqld           
tcp        0      0 0.0.0.0:5355            0.0.0.0:*               LISTEN      965/systemd-resolve  
tcp        0      0 0.0.0.0:5900            0.0.0.0:*               LISTEN      1821/vino-server    
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      753/cupsd           
tcp6       0      0 :::5355                 :::*                    LISTEN      965/systemd-resolve   
tcp6       0      0 :::5900                 :::*                    LISTEN      1821/vino-server    
tcp6       0      0 ::1:631                 :::*                    LISTEN      753/cupsd           

Here first line's last column tells us that it's Mysql,  
Check the local address of the line it will and it will tell us that the port no 3306 is being used.    

2.  To find all the privileges given to a user in Mysql.  

To know the privileges of a user login to your Mysql with the user whose privileges you want to know and type this.  
INPUT: show grants;  

OUTPUT:
+---------------------------------------------------------------------+  
| Grants for root@localhost                                           |  
+---------------------------------------------------------------------+  
| GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION |  
| GRANT PROXY ON ''@'' TO 'root'@'localhost' WITH GRANT OPTION        |  
+---------------------------------------------------------------------+  

The above output tells you that all the privileges has been given to the user "root".  

3.  How to create a new user in Mysql and give privileges.  

CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'newpasswordforthisuser';

EXAMPLE:
mysql> CREATE USER 'os'@'localhost' IDENTIFIED BY 'Osmysql@1';
Query OK, 0 rows affected (0.02 sec)

BUT IF YOU GET AN ERROR LIKE THIS 
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements

IT MEANS YOU NEED TO FOLLOW THE CRITERIA THAT HAS BEEN SET FOR PASSWORDS.

TO CHECK THE CRITERIA THAT HAS BEEN SET RUN THIS COMMAND IN YOU MYSQL
