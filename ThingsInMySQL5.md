**[Things in Mysql](http://ktgnair.github.io/Things In Mysql) / [Check Port No](http://ktgnair.github.io/ThingsInMySQL1) / [Check user privileges](http://ktgnair.github.io/ThingsInMySQL2) / [Create new user and give privileges](http://ktgnair.github.io/ThingsInMySQL3) / [Different operations in MySQL](http://ktgnair.github.io/ThingsInMySQL4)**  

**Reset root password.**  

This ia one particular issue which i faced while i was trying to take backup of some database but soon realized that i don't have some permissions for that user.  
So the alternative was to be the root user and perform the operations of backup, but then faced another problem i.e I did not remember the right password for root to login.  
I was getting this error when i typed what i fairly remembered as my password to login into root user.  
```  
ERROR 1045: Access denied for user: 'root@localhost' (Using password: YES)  
```  
That's when i started looking for answers to reset the root password and found a way.  

It's not that tough, you just need to follow some steps and **__voila__** you reset your password.  

**Step 1:**  
Stop the MySQL service using this command.  
```  
sudo service mysql stop  
```  
I am using Ubuntu to perform this operation.  

Others like CentOS or Fedora can be stopped by typing this
```  
sudo service mysqld stop   
```  

If you are using Windows as your Operating System then i would recommend you to stop the service by going in the following flow  
Click on Start option -> Type Services in the Search box -> Select the MySQL service and stop it.  

**Step 2:**  
Now start the MySQL without a password
Type this command
```  
sudo mysqld_safe --skip-grant-tables &  
```  

**Step 3:**  
Now run this command
```  
mysql  
```  
This will connect you to mysql  

**Step 4:**  
In the MySQL shell type this to set new password.  
