**[Assignment 1](https://ktgnair.github.io/) / [My Experience](https://ktgnair.github.io/LearnedThings)**

Overall my experience while doing this assignment was challenging as well as great.

While i was doing this program,i was practically experiencing the most famous English Idiom 'Don't judge a book by its cover'.   After reading the question for the first time i felt whooe now i just need to reverse the file contents but by looking at the program constraints my mind started to look for answers and different approaches.  

The Constraints are as follows:-
+ Test with very large inputs files, e.g. 5GB.
+ The program should be robust in that it should be independent of the file size. The memory requirements should be more or less    same for input files of varying sizes 1 KB, 5 KB, or 5 GB
+ Also give memory and speed reading for 1 GB, 5 GB.  

I was able to learn different things like internal working, functions, Unix Commands, Naming Conventions and debugging methods which i will be showcasing in the coming lines.  

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
There are other approaches also of which one is using UNIX command 'cat' which helps in merging the files.  
So if you have a 1gb file and you need to generate a 5 gb file just type this  

> cat 1gb.txt 1gb.txt 1gb.txt 1gb.txt 1gb.txt > 5gb.txt

The next thing is finding the size of input file

Use 'stat' function as used below

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
One way of doing that is using UNIX command which is shown in the below block  
> ls -l filename

My first way of doing the code was using fseek()  
What fseek() does is that it helps us to move the file pointer position to a given location.  

> Syntax:int fseek(FILE *pointer, long int offset, int position)  

where position provides us 3 options those are  
SEEK_END : It denotes end of the file.  
SEEK_SET : It denotes starting of the file.  
SEEK_CUR : It denotes file pointer’s current position.    

For creating temporary file when doing my final approach i used sprintf() so that i can get different file name sequentially.  

When i had finished coding i realized that making the code in a readable format is also necessary so that when in future some guy looks into your code he should be able to understand it quickly instead of having doubts.  
+ So to make that happen i changed the names of the variables from my code like for example int n was changed to int file_size because the variables actual function is to store the file size.  

+ Next is to avoid all unwanted tabs, spaces.
