**[Assignment 2](https://ktgnair.github.io/Assignment 2) / [My Experience](https://ktgnair.github.io/LearnedThings2)**

This Assignment also had the same constraints as previous assignment.  
 
The Constraints are as follows:-  
+ Test with very large inputs files, e.g. 5GB.  
+ The program should be robust in that it should be independent of the file size. The memory requirements should be more or less same for input files of varying sizes 1 KB, 5 KB, or 5 GB  
+ Also give memory and speed reading for 1 GB, 5 GB.  

In this Assignment the most important topic that i learned is about Ehcache which was completely new to me and i am also sure that its new for most of the other new programmers.  

Now lets speak about cache memory  


1. Its a high speed memory to increase the speed of processing of the CPU.  
2. Main function of cache memory is to store the copy of frequently used program or data.  
3. There are 3 levels of cache  
  * Level 1  
  * Level 2  
  * Level 3  
4. Level 1 and Level 2 are stored in CPU and Level 3 is stored in motherboard.  
5. Capacity wise Level 1 has smallest capacity say 2-64KB, then Level 2 256-512KB and the last Lvel 3 has the highest that is 1-8MB.  
6. Cache memory is stored in SRAM and main memory in DRAM.  
7. SRAM is expensive as compared to DRAM because SRAM uses 6 transistors while DRAM has only 1 transistors.   

Ehcache library  

Ehcache is an open-source standard cache for boosting performance.  

It is the most widely used java based cache.  

Now i will tell you why i used Ehcache for my Assignment 2 when i could have used Collections.  

> In Ehcache we can limit the maximum element a cache can have as well as how much memory a cache can consume.  

> If it reaches the limit then Ehcache has the algorithms such as LRU,LFU etc to clean itself. (Which is not possible in Map or HashMap interfaces, We have to add those functionality explicitly).

> Ehcache provides the functionality of when the memory cache exceeds a certain limit then overflowing to the disk is possible.  

> In Ehcache suppose the system crashes or goes into unplanned shutdowm then the data will stay persistant.

For Configuring Ehcache using Maven Dependency Which i used(Another way is using gradle)  

There are two xml files that need to be included in your program those are pom.xml and ehcache.xml  

> pom.xml  

```xml
<dependency>
	<groupid>net.sf.ehcache</groupid>
	<artifactid>EHcache</artifactid>
	<version>2.10.4</version>
</dependency>

```
   
> ehcache.xml  

```xml
<?xml version="1.0" encoding="UTF-8"?>

<ehcache xsi:noNamespaceSchemaLocation="ehcache.xsd" updateCheck="true" monitoring="autodetect" dynamicConfig="true">
<diskStore path="java.io.tmpdir"/>

	<cache name="mycache1"
		maxEntriesLocalHeap="10000"
		maxEntriesLocalDisk="100000"
		overflowToDisk="false"
		eternal="true"
		diskSpoolBufferSizeMB="20">
	</cache>

</ehcache>
 
```
While configuring the ehcache make sure you place the .xml file in right path or else it will take the default failsafe xml file.  
And also gives you a warning as this  

> No configuration found Configuring ehcache from ehcache-failsafe.xml  found in the classpath: //...

Final Test Case:  
After completing the code on running it, it took me 13 seconds for 50mb file and 240 seconds for 1gb file.

