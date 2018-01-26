**[Assignment 1](https://ktgnair.github.io/) / [My Experience](https://ktgnair.github.io/LearnedThings)**

Overall my experience while doing this assignment was challenging as well as great.

While i was doing this program,i was practically experiencing the most famous English Idiom 'Don't judge a book by its cover'.   After reading the question for the first time i felt whoo now i just need to reverse the file contents but by looking at the program constraints my mind started to look for answers and different approaches.  

The Constraints are as follows:-
+ Test with very large inputs files, e.g. 5GB.
+ The program should be robust in that it should be independent of the file size. The memory requirements should be more or less    same for input files of varying sizes 1 KB, 5 KB, or 5 GB
+ Also give memory and speed reading for 1 GB, 5 GB.  

I was able to learn different thinks like internal working, functions, Unix Commands, Naming Conventions and debugging methods which i will be showcasing in the coming lines.  

The first thing while doing the program was to create a text file which is of the size 5gb.

For doing that this is something that i did and was able to generate the file. 
```c
#include <stdio.h>

int main()
{
    FILE *fp=NULL;
    long int size=0;

    int i,n;
 
    
    fp=fopen("1gb.txt","w");
     

    /*for(i=0;i<=9999999;i++)
        fputs("1 My name is ktgn 2 This is 2 This is a 1 gb file",fp);

    fclose(fp); 
    return 0;
}
```
There are other approaches also of which one is using UNIX command cat which helps in merging the files.  
So if you have a 1gb file and you need to generate a 5 gb file just type this  

> cat 1gb.txt 1gb.txt 1gb.txt 1gb.txt 1gb.txt > 5gb.txt

The next thing is finding the size of input file

Use stat function as used below

```c
#include <stdio.h>
#include <sys/stat.h>

int main()
{
   int n;
   
    	struct stat st;
	stat("1gb.txt", &st);
  	n=st.st_size;
	printf("%d",n);   
    return 0;
}
```
