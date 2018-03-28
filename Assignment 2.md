 **[Home](https://ktgnair.github.io/) / [Assignment 1](https://ktgnair.github.io/Assignment 1) / [Git Tutorials](https://ktgnair.github.io/Basic Github) / [Rules For Code](https://ktgnair.github.io/Rules For Code)**  
 
 **PROGRAM NO 2**  
 
 _**Count the Occurrences of every word in an Input File.**_  


Lets say the input is  

“Apple is healthy food. Soda is junk food.”  
        
So the output will be  

Apple: 1, is: 2, healthy: 1, food: 2, Soda: 1, junk: 1  

> **APPROACH 1**  

After doing the First Assignment i realized that i need to think differently to solve this Assignment No 2.  
So this is what i thought could be the solution, I am not writing the code directly as it is not the best way to finalize an approach but to write the Pseudo Code is.  


```
MAIN()  

WHILE  
	READ THE FILE BY FIXED CHUNK SIZE.  
	SPLIT THE CHUNK WORD BY WORD.  
	PUT THE WORDS IN THE ARRAY OF COLLECTION OBJECT.  

	FUNCTION CALL TO UPDATE_DB()  

LOOP UNTIL END OF FILE.  
READ THE NEXT CHUNK(REPEAT WHILE).  


FUNCTION UPDATE_DB()  
	
	WHILE  
	READ THE ARRAY OF COLLECTION OBJECT  

	CHECK WHETHER THE WORD(COLLECTION OBJECT) IS PRESENT IN THE DATABASE TABLE.  

	IF PRESENT  
	  UPDATE THE COUNT IN DB.  
	ELSE  
	  INSERT THE WORD IN DB.  

	END WHILE.	

	RETURN TO MAIN().  

END UPDATE_DB.  
 

NOTE:  
COLLECTION OBJECT WILL BE STORED IN <KEY,VALUE> PAIR WHERE KEY = WORD AND VALUE = COUNT.  

```

This is a good approach but the person who gave me this Assignment increased the level of complexity by giving me the challenge of not using Database. So this was rejected.  

> **APPROACH 2**  

Thinking for a new way to do the assignment lead me to think how can i store the data without the database.  
The most appropriate way at that time was to use Files.  

```
MAIN()  

CREATE 36 TEMP FILES(TO STORE WORDS AND DIGITS)  

WHILE  

   READ FILE WITH FIXED BUFFER.  
   SPLIT THAT BUFFER INTO WORDS OR DIGITS.  
   STORE THOSE WORDS OR DIGITS ACCORDING TO THEIR FIRST CHARACTER INTO RESPECTIVE FILES.  

READ NEXT BUFFER.  
REPEAT WHILE UNTIL END OF FILE.  

END WHILE  

WHILE  

   READ THE TEMP FILE.  
   STORE IT IN ARRAY OF COLLECTION OBJECT.  
   PRINT THE ARRAY OF COLLECTION OBJECTS IN OUTPUT FILE.  
   REMOVE ALL DATA FROM ARRAY OF COLLECTION OBJECT.  

REPEAT WHILE UNTIL LAST FILE(36th).  

END WHILE  


FOR EXAMPLE  

SAY A SENTENCE "THIS IS SAMPLE 1 AND 2" NEEDS TO BE STORED  

SO THE SENTENCE WILL BE STORED AS  
"THIS" WILL BE STORED IN t.txt  
"IS" WILL BE STORED IN i.txt  
"SAMPLE" WILL BE STORED IN s.txt   
"1" WILL BE STORED IN 1.txt  
"AND" WILL BE STORED IN a.txt  
"2" WILL BE STORED IN 2.txt  

``` 

I realised this is not a solution because  


* I am reading the same word twice, one from the main file and once from temp file.  

> **APPROACH 3**  

After the previous approach got rejected my mind started searching for answers in all possible ways.  
This is one such approach that is using Serialization.  

```
MAIN()

CREATE OUTPUT FILE.
WHILE 
	READ THE INPUT FILE BY FIXED CHUNK SIZE.
	SPLIT THE CHUNK WORD BY WORD.
	PUT THE WORDS IN THE ARRAY OF COLLECTION OBJECT TEMP_COLL.
	
	FUNCTION CALL TO MAKE_SERIALIZE()

LOOP UNTIL END OF FILE. 
READ THE NEXT CHUNK(REPEAT WHILE).

FUNCTION MAKE_SERIALIZE()

WHILE

	DECLARE  COLLECTION OBJECT MASTER_COLL.
	READ THE ARRAY OF COLLECTION OBJECT TEMP_COLL.

	RETRIVE THE CONTENTS OF MASTER_COLL FROM THE OUTPUT FILE.

	CHECK WHETHER THE WORD(COLLECTION OBJECT TEMP_COLL) IS PRESENT IN THE MASTER_COLL.

	IF PRESENT
	  UPDATE THE COUNT IN MASTER_COLL.
	ELSE
	  INSERT THE WORD IN MASTER_COLL.

	WRITE THE MASTER_COLL OBJECT INTO THE OUTPUT FILE.(SERIALIZTION OF OBJECTS)
	CLEAR MASTER_COLL DATA.

	END WHILE.	

	RETURN TO MAIN().

END MAKE_SERIALIZE().

```

But after writing the Pseudo Code i felt that its too complex and can be made little more simple, my mentor told me to read about cache which was a hint from his side to do the assignment in a different way.  

After reading about cache i came across an open source library which is widly used by java developers across the world that is ***Ehcache***.  
I have mentioned about the configuration in My Experience page at the end of this article.  


> **APPROACH 4**  

```java

package Assisn;

import net.sf.ehcache.Cache;
import net.sf.ehcache.CacheManager;
import net.sf.ehcache.Element;
import java.util.*;
import java.io.*;

public class word {

    public word() {
    }
   
    public static void storeToCache(String str,Cache cache)
    {
        StringTokenizer string_token = new StringTokenizer(str," ");                                             //Split chunk by space to get individual words.
       
       
        while (string_token.hasMoreTokens()) { 
        
         String str_word = string_token.nextToken();
       
        if(cache.isKeyInCache(str_word))
        {
            Element el = cache.get(str_word);
           
            cache.put(new Element(str_word ,Integer.parseInt(el.getObjectValue().toString())+1));                //If word is present there just increment word count.
           
        }
        else
        {
       
            cache.put(new Element(str_word,1));                                                                  //New word is inserted in cache and word count is 1
       
        }
       
        }//while
       
       
    }
   
    public static void main(String[] args) throws IOException{
       
        long startTime = System.nanoTime();
       
        File file= new File("demo1.txt");
       
        FileReader filereader = new FileReader("demo1.txt");
        FileWriter filewriter = new FileWriter("output.txt");

        BufferedReader buffreader = new BufferedReader(filereader);
        BufferedWriter buffwriter = new BufferedWriter(filewriter);
       
        CacheManager cachemanager = CacheManager.newInstance("src/ehcache.xml");
       
        Cache cache = cachemanager.getCache("mycache1");
               
        cachemanager.clearAll();   
               
        long filesize = file.length();
               
        char cbuf[] = new char[4999990];                                                                        //To store chunk
               
        long remainder= filesize % 4999990;
               
        String temp_str;
               
        int index;    
                    
	do
           {
              buffreader.read(cbuf, 0, (int)remainder);                                                         // Reading by chunk size of n bytes
              filesize = filesize - remainder;
              remainder=4999990;
                       
              temp_str=new String(cbuf);   

              temp_str=temp_str.replaceAll("[^a-zA-Z0-9]"," ");                                                 //Remove special characters.
               
              word.storeToCache(temp_str , cache);                                                              //Function call to storeTocache
               
            }while(filesize>0);
               
               
                List keylist = cache.getKeys();                                                                 //Retrieving all keys present in  the cache
               
                int size = keylist.size();
               
                ListIterator iterator = keylist.listIterator();
               
                System.out.println("Reading from cache");
               
                while(iterator.hasNext())
                {
                    String key= iterator.next().toString();
                   
                    Element el = cache.get(key);                                                                //Getting value according to key.
                   
                    String value = el.getObjectValue().toString();
                   
                    buffwriter.write(key+" -> "+value+"\n");                                                    //Storing key values in text file.  
                }
               
                System.out.println("Read successful from cache");
                   
                long memsize = cache.getMemoryStoreSize();
                System.out.println("On Memory = "+memsize);
               
                long disksize=cache.getDiskStoreSize();
                System.out.println("On Disk = "+disksize);
               
                cachemanager.clearAll();
                cachemanager.shutdown();

                buffreader.close();
                buffwriter.close();
               
                filereader.close();
                filewriter.close();
       
                long endTime   = System.nanoTime();
                long totalTime = (endTime - startTime)/1000000000;
               
                System.out.println("execution time for program="+totalTime+" secs");
                System.out.println("getkeys size = "+ size);
               
        }

}

```
  
Check out **[My Experience](https://ktgnair.github.io/LearnedThings2)** for information about cache and Ehcache configuration.  
