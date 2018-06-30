**[Home](https://ktgnair.github.io/) / [Assignment 1](https://ktgnair.github.io/) / [Assignment 2](https://ktgnair.github.io/Assignment 2) / [Rules For Code](https://ktgnair.github.io/Rules For Code) / [Git Tutorials](https://ktgnair.github.io/Basic Github) / [Database](https://ktgnair.github.io/Database) / [Export Mysql](http://ktgnair.github.io/ExportMysql) / [How to disable root for ssh](http://ktgnair.github.io/DisableRoot) / [Things in Mysql](http://ktgnair.github.io/Things In Mysql)**  


**To use AJP as a connector in Apache for reverse proxy**   

> STEP 1: To check if AJP port is uncommented in your Tomcat's server.xml.  

The file _**server.xml**_ is located in your Apache-Tomcat's _**conf**_ folder.  

In the file this is the line you need to uncomment  
```  
 <!-- Define an AJP 1.3 Connector on port 8009 -->  
    <!-- <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" /> -->  
 
After removing the comment  
<!-- Define an AJP 1.3 Connector on port 8009 -->  
    <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />  
```  
The connector port is by default 8009 for AJP  

> STEP 2: Comment the HTTP connector.  

Now since you will be using AJP connector there is no need for the HTTP connector so comment it out. 
This means you will be using Port no 8009 henceforth instead of 8080.  

Comment out these lines from your server.xml file.  
```  
<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443"/>  

After commenting the lines  
<!-- <Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443"/> -->  
```  

> STEP 3: Check module installations.  

To configure the AJP we need to have the appropriate modules installed.  

Type this command on your terminal to see the list of all the modules loaded in your Apache.  
```  
httpd -M  
```  
It provides you a list of all the modules, in that check for proxy_ajp_module (shared)  

You can also check modules inside the folder where your Apache is installed.  
In my case it was this /etc/httpd/conf.modules.d/   
```  
vi /etc/httpd/conf.modules.d/00-proxy.conf  
```  
This file has configurations of all the proxy modules.  

Check if you have uncommented this line, if not the do it.  
```  
LoadModule proxy_ajp_module modules/mod_proxy_ajp.so  
```  
Now save the file and restart the Apache by running this command.  
```  
service httpd restart  
```  
After that check the status by typing this command.  
```  
service httpd status  
```  

It will show you that Apache is ACTIVE alongwith the time since it's last been started.  

> STEP 4: Configuration in Apache.  

Now got to _**conf**_ folder in your folder where Apache is installed.  
Usually it's in  _**/etc/httpd/conf**_  

Open the _**httpd.conf**_ file.  
```  
vi httpd.conf  
```  
Inside that file just check if this line is uncommented.  
```  
Include conf.modules.d/*.conf  
```  
The meaning of the above line is that take all the files from conf.modules.d file.  

Now at the end of the file add these lines.  
```  
<VirtualHost *:80>  
ServerName 188.166.174.63  
ProxyPreserveHost On  
ProxyPass / ajp://188.166.174.63:8009/ retry=0  
ProxyPassReverse / ajp://188.166.174.63:8009/ retry=0  
</VirtualHost>  
```  
Save this file and again restart the Apache  
```  
service httpd restart  
```  
After that check the status  
```  
service httpd status   
```  

> STEP 5: The final step  

Now that you have finished the configurations its time for you to run it.  

Open your browser and type your URL(ip address)  

Just doing that your request will be passed to Tomcat from Apache and it will load any apps you have in your Tomcat  
**Example:** Say you have installed Jenkins in your Tomcat then after running the URL, it will open your Jenkins login page.   

After doing all these configurations we will be accessing our apps using just the ip address and not with the port no as we were doing earlier.   
i.e  
**YOU CANNOT USE THIS URL**     
**ip address:8009**     
