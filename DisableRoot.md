**[Home](https://ktgnair.github.io/) / [Assignment 1](https://ktgnair.github.io/Assignment 1) / [Assignment 2](https://ktgnair.github.io/Assignment 2) / [Git Tutorials](https://ktgnair.github.io/Basic Github) / [Database](https://ktgnair.github.io/Database)**  

**This post talks about how to disable root for ssh**  

> Create a new server from lets say _Droplet_  

Creating the new server will provide us the following  
* Droplet Name  
* IP Adress  
* Username  
* Password   

> Using the details from the earlier step we log in from terminal   
Syntax: ssh username@ipaddress   
**Example:** ssh root@188.167.164.36

It will ask you for a password(Type your password which was provided to you by Droplet and press Enter).  

Which leads to a message to change your current password  
* Type your current password and press enter  
* Enter your new password.  
* Re-type your new password.   

> Create a new user  
To create a new user type this command in your terminal  
```  
useradd NewUserName  
```  
**Example:** useradd jenkins  
This will create the new user now is to get inside the new user.  
To do that we need to switch user from root to newly created user i.e jenkins.  

```  
[root@os ~]# su jenkins      (newly created user)  
```  
After typing the above you will notice that we are still in the root directory  
```  
[jenkins@os root]$  
```  
Type the below line to get into the user directory i.e jenkins.  
```  
[jenkins@os root]$ cd  
```  

> Set password to your user.  
* Go to root and type this   
```  
[root@os ~]# passwd jenkins  
```   

* Which will ask you to do the following.  
```  
Changing password for user jenkins.  
New UNIX password:  
Retype new UNIX password:  
passwd: all authentication tokens updated successfully.  
```   
> Sudo privileges to new user  
Now to give sudo privileges to the newly created user i.e jenkins  
* Go to your root user.  

* Open the sudoers file which is located in etc folder.  
```  
[root@os ~]$ cd /etc  
[root@os etc]$ vi sudoers  
```  
In that file add the below line at the end of that file.  
To add the line press Esc and i (for inserting inside a vi editor)  
```  
jenkins ALL=(ALL)   ALL  
```  
Press Esc and the save the file by pressing Shift :wq and Enter  

> Try to login to your newly created user. (Below the process)  
```  
[root@os ~]# ssh jenkins@ip_address  
**Example:**  
[root@os ~]# ssh jenkins@188.167.164.36  
jenkins@188.166.174.63's password:  
[jenkins@os ~]$   
```  
Last line from the above tells you that you have been able to successfully log in from your new user.  

But our main task is to disable the root so that you can access this server using only your newly created user.  

Now switch back to your root from the newly created user  
```  
[jenkins@os ~]$ su -
Password:(type your root [password)  
```   
> To disable the root ssh login.  
* Go inside the folder ssh which is located inside etc.  
```  
[root@os ~]# cd /etc/ssh  
```  
Open a file named sshd_config using vi editor.  
```  
vi sshd_config  
```  

In that following file search for this line.
```  
#PermitRootLogin yes  
```  

Edit the line to this:  
```  
PermitRootLogin no  
```  

You will notice that what i have done is remove the comment and write it as no.  
Save the file  

> Retart the sshd.  
**Note:** Before performing sshd restart make sure you open a new terminal and do root login to avoid locking yourself out of the server.  

Type this line.  
```  
[root@os ~]# /etc/init.d/sshd restart  
```  
After this line following should be displayed into your terminal.  
```  
Stopping sshd: [ OK ]   
Starting sshd: [ OK ]   
[root@os ~]#  
```  
But if it's not displayed and you get a message something like this  
```  
-bash: /etc/init.d/sshd: No such file or directory  
```  
Do not worry, just follow the below steps and you will be able to restart.  
```  
[root@os ~]# systemctl restart sshd.service   
```  

Now check the status.  
```  
[root@os ~]# systemctl status sshd   
```  

The following output will be dispalyed.    
```  
● sshd.service - OpenSSH server daemon  
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)  
   Active: active (running) since Fri 2018-04-13 12:15:12 UTC; 2 days ago  
     Docs: man:sshd(8)  
           man:sshd_config(5)  
 Main PID: 3610 (sshd)  
   CGroup: /system.slice/sshd.service  
           └─3610 /usr/sbin/sshd -D  
Apr 16 06:30:01 os-build systemd[1]: Starting OpenSSH server daemon...  
Apr 16 06:30:01 os-build sshd[8353]: Server listening on 0.0.0.0 port 22.  
Apr 16 06:30:01 os-build sshd[8353]: Server listening on :: port 22.  
Apr 16 06:30:01 os-build systemd[1]: Started OpenSSH server daemon.  
```  

Now logout to close the connection.  
```  
[root@os ~]# logout  
[jenkins@os ~]$ logout  
Connection to 188.166.174.63 closed.  
[root@os ~]# logout  
Connection to 188.166.174.63 closed.  
```  
You had to perform so many logouts since you just switched the user from one to another so you need to logout all the users.  

> Final step    
Now that you have loged out completely from one terminal(do not close or logout from the second terminal in which we had logged in as root)  
Try to log in using root.  
```  
user@user-Lenovo-ideapad-320-15ISK:~$ ssh root@188.167.164.36   
root@188.167.164.36's password:   
```  
You will get this  
```  
Permission denied, please try again.  
```  

If you got this message then you have successfully disabled the root form ssh.    
Try logging in using the newly created user.    
You will be able to login successfully.  

Now after completing the above steps just remember that you cannot login using root as you have disabled it and gave sudo privileges to new user i.e jenkins.  
