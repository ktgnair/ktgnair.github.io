**[Home](https://ktgnair.github.io/) / [Assignment 1](https://ktgnair.github.io/) / [Assignment 2](https://ktgnair.github.io/Assignment 2) / [Rules For Code](https://ktgnair.github.io/Rules For Code) / [Git Tutorials](https://ktgnair.github.io/Basic Github) / [Database](https://ktgnair.github.io/Database) / [Export Mysql](http://ktgnair.github.io/ExportMysql) / [How to disable root for ssh](http://ktgnair.github.io/DisableRoot) / [Things in Mysql](http://ktgnair.github.io/Things In Mysql) / [Issues during Tomcat](http://ktgnair.github.io/Tomcat_Issues)**  

*__Step by Step installation of JAVA JDK.__*   

The steps which will be explained below will help a beginner to install the JDK package on Windows 10.  
JDK package is necessary to run java programs.   

Note:  
Before following the installation steps we need to check if java is already installed or not?  
To perform that check you just need to open your command prompt and type 'javac' command and the resulting output will tell you whether there is a need for you to install the java or not.    

If you notice any error which states that 'javac' is not recognized then you will know that java is not installed in your system.  

<b>Step 1: Download JDK</b>   

You need to download the JDK from internet.  
Just search java jdk in your browser and click on the official link for downloading the JDK  

The official link is the usually the first link as shown in the screenshot below.  
> ![Search for JDK in your browser](/images/Install Java jdk/Step 1-searchJDK.PNG)  

On clicking the first link you will be taken to the downloads section(as shown in image 1.1), where you need to select the appropriate version of JDK which you need(as shown in image 1.2). At the time of this tutorial I used JDK 8.  

After selecting the version of JDK as per your need, you will be redirected to another page which has all the downloads for different OS.  
Download the JDK package as per your OS requirements from the list(as shown in image 1.3).  

Image 1.1  

> ![Download page](/images/Install Java jdk/Step 1.1.PNG)  

Image 1.2  

> ![Version select image](/images/Install Java jdk/Step 1.2.PNG)  

Image 1.3  

> ![Download JDK](/images/Install Java jdk/Step 2-downloadjdk.PNG)  

<b>Step 2: Installing the downloaded file</b>  

Now comes the actual part of installing the JDK which you downloaded in step 1  

Open the downloaded file and just follow the steps which will be guided to you by the installer.  
Once the JDK is successfully installed, you can confirm it by going to your folder where JDK has been installed.  

In my case I kept the destination path as default so it's installed in the C:\Program Files\Java  
In that folder there will be 2 other subfolders(JDK and JRE).  

<b>Step 3: Setting up environment variables</b>  

Just installing the JDK is not enough!  

You need to set up the environment variables, so that whenever you run a JAVA program it will recognize the JDK and JRE, which will help to compile your programs successfully.  

Now go to this path <b>Control Panel\System and Security\System</b> of your machine.  
In there click on the Advanced system setting(as shown in the below image)  
> ![Step 3.1](/images/Install Java jdk/Step 3.1.PNG)  

After that a popup stating System Properties will be opened, in that click on Environment Variables(as shown in the below image)  
> ![Step 3.2](/images/Install Java jdk/Step 3.2.PNG)  


;C:\Program Files\Java\jdk8\bin;C:\Program Files\Java\jre8\bin;






