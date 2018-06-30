**[Things in Mysql](http://ktgnair.github.io/Things In Mysql) / [Check user privileges](http://ktgnair.github.io/ThingsInMySQL2) / [Create new user and give privileges](http://ktgnair.github.io/ThingsInMySQL3) / [Different operations in MySQL](http://ktgnair.github.io/ThingsInMySQL4) / [Reset root password](http://ktgnair.github.io/ThingsInMySQL5)**  

*__To check which port is used by MySQL.__*   

Type the following in your terminal.  
```  
INPUT:      
sudo netstat -tlnp  
```  

```  
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
```  

Here first line's last column tells us that it's MySQL,  
Check the local address of the line it will and it will tell us that the port no 3306 is being used.  
