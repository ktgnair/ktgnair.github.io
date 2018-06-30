**[Things in Mysql](http://ktgnair.github.io/Things In Mysql) / [Check Port No](http://ktgnair.github.io/ThingsInMySQL1) / [Create new user and give privileges](http://ktgnair.github.io/ThingsInMySQL3) / [Different operations in MySQL](http://ktgnair.github.io/ThingsInMySQL4) / [Reset root password](http://ktgnair.github.io/ThingsInMySQL5)**  


*__To find all the privileges given to an user in MySQL.__*  

To know the privileges of an user, login to your MySQL with the user login details whose privileges you want to know and type this.  
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

Another way to view the privileges given to an user is by typing this  
```  
<b>INPUT:</b>    
show grants for current_user;  
```  

This also gives the same output as the earlier command.  
