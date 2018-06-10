**[Home](https://ktgnair.github.io/) / [Assignment 1](https://ktgnair.github.io/) / [Assignment 2](https://ktgnair.github.io/Assignment 2) / [Rules For Code](https://ktgnair.github.io/Rules For Code) / [Git Tutorials](https://ktgnair.github.io/Basic Github) / [Database](https://ktgnair.github.io/Database) / [Export Mysql](http://ktgnair.github.io/ExportMysql) / [How to disable root for ssh](http://ktgnair.github.io/DisableRoot) / [Things in Mysql](http://ktgnair.github.io/Things In Mysql)**  


**Tomcat taking time to start**   

_**If you are facing the issue of Tomcat taking time to start in the browser eventhough you are gettingthe message "Tomcat started" in your terminal, then try this.**_   

You need to add a particular line in catalina.sh file.  

So lets start the process,  
1. Open the file catalina.sh which is located in your Tomcat's bin folder.   
Ex: vi /opt/tomcat/bin/catalina.sh  

2. In the catalina.sh look for this particular line.  
```  
# Register custom URL handlers  
# Do this here so custom URL handles (specifically 'war:...') can be used in the security policy  
JAVA_OPTS="$JAVA_OPTS -Djava.protocol.handler.pkgs=org.apache.catalina.webresources"  
```  
Below JAVA_OPTS line add another line like this  
```  
JAVA_OPTS="$JAVA_OPTS -Djava.security.egd=file:/dev/./urandom"  
```  
3. Save this file and you should be able to solve your problem of delay to start Tomcat.  
