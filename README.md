 ## _Assignment No 1 : Reverse The Contents of an Input File._


Lets say the input is something like this

Input: “hello world
        I am ktgnair."
        
So the output should be like this

Output: “.riangtk ma I
         dlrow olleh”


+ **APPROACH 1**

As the question said reverse the contents so using fseek() and reading from the end of the file character by character was something that came to my mind.  
It was working smoothly for file having small size but as soon as the file size increased the execution time increased gradually which didn't seem feasible.  

```c
#include<stdio.h>
#include<stdlib.h>

int main()
{
	int size,n;
   	FILE *fp,*fp1;
 	char c;
	
  	if ((fp = fopen("1gb.txt","r")) == NULL)
	{
       printf("Error! opening file");
        }

	fp1= fopen("demo11.txt","w");

	fseek(fp, -2, SEEK_END);
	size=ftell(fp);

	printf("%d\n",size);

	while(n!=0)
	{
		c=fgetc(fp);
		fputc(c,fp1);
		fseek(fp,-2,SEEK_CUR);
		n=ftell(fp);
	}

	fclose(fp);
	fclose(fp1);
	return 0;	
}
```

+ **APPROACH 2**

The next thought that came into my mind was to use 2 files
In that method i was taking a small chunk of data, reversing it and storing it in the second file.

The only problem with that method was that i was not getting the required output.

i.e. for 

	Input: 		"hello world
        	 	I am ktgnair."
	
	Actual Output:  "dlrow olleh
			.riangtk ma I"

	Estimated Output: ".riangtk ma I
         		    dlrow olleh"

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>

int flag=0;

void append()
{
	int n,n1,n2;
  	 FILE *fp1,*fp2;
 	char c[1024];

  	if ((fp1 = fopen("demo11.txt","r")) == NULL)
	{
       		printf("Erro! opening file");
     	}
	
	fp2=fopen("demo7.txt","a");

	struct stat st;
	stat("demo11.txt", &st);
  	n=st.st_size;
	printf("\nappend %d \n",n);

	if(n<1024)
	{
		fread(c,1,n,fp1);
		fwrite(c,1,n,fp2);
	}
	else
	{
		n1=1024;
		while(n/1024)
		{
			fread(c,n1,1,fp1);
			n2=strlen(c);
			n2=n2-6;
			c[n2]='\0';
			n2=n2-1;
			//fwrite(c,n2,1,fp2);
			fputs(c,fp2);
			n=n-1024;
		}
		fgets(c,n,fp1);
		fputs(c,fp2);
	}
	fclose(fp1);
	fclose(fp2);
}

void moveto1()
{
	int n,n1,n2;
  	 FILE *fp1,*fp2;
 	char c[1024];

  	if ((fp1 = fopen("demo7.txt","r")) == NULL)
	{
       		printf("Erro! opening file");
     	}
	
	fp2=fopen("demo11.txt","w");
	
	struct stat st;
	stat("demo7.txt", &st);
  	n=st.st_size;
	printf("\nmove %d \n",n);
	
	if(n<1024)
	{
		fread(c,1,n,fp1);
		fwrite(c,1,n,fp2);
	}
	else
	{
		n1=1024;
		while(n/1024)
		{
			fread(c,n1,1,fp1);
			n2=strlen(c);
			n2=n2-6;
			c[n2]='\0';
			n2=n2-1;
			//fwrite(c,n2,1,fp2);
			fputs(c,fp2);
			n=n-1024;
		}
		fgets(c,n,fp1);
		fputs(c,fp2);
	}
	fclose(fp1);
	fclose(fp2);
}
void rev(char c[])
{
	FILE *fp1,*fp2;	
	int n,n1;
	int i,j;
	char t;
	i=0;
	
	n=strlen(c);
	n=n-6;
	c[n]='\0';
	n=n-1;
	
	while(i<n)
	{
		t=c[i];
		c[i]=c[n];
		c[n]=t;
		i++;
		n--;
	}
	
	if(flag==0)
	{
		fp1=fopen("demo11.txt","w");
		fputs(c,fp1);
		fclose(fp1);
		flag=1;	
	}
	
	if(flag==1)
	{
		fp2=fopen("demo7.txt","w");
		fputs(c,fp2);
		fclose(fp2);
		append();
		moveto1();	
	}	
}

int main()
{
	int n,n1,s;
  	 FILE *fp;
 	char c[1024];

  	if ((fp = fopen("demo2.txt","r")) == NULL)
	{
       		printf("Erro! opening file");
     	}

	struct stat st;
	stat("demo2.txt", &st);
  	n=st.st_size;
	printf("%d",n);
	s=1;

	if(n<1024)
	{
		fread(c,1,n,fp);
		rev(c);
	}
	else
	{
		n1=1024;
		while(n/1024)
		{
				fread(c,n1,1,fp);
				rev(c);
				n=n-1024;			
		}
	}
		fgets(c,n,fp);
		rev(c);
	
	fclose(fp);
	
	return 0;	
}

```

+ **APPROACH 3** 

After two failure I started thinking the problem as some puzzle and was able to come up with a solution that is _**Tower of Hanoi**_ problem.  
So with that as my approach i planned on using 3 files of which one is the input file and the next two are for data swapping.

This method can be explained best with an example

Step 1

| File 1(Input File) | File 2 | File 3 |
| ------------------- | ------ | ------ |
| a | a | b |
| b |   |   |
| c |   |   |


Step 2

| File 1(Input File) | File 2 | File 3 |
| ------------------ | ------ | ------ |
| a |   | b |
| b |   | a |
| c |   |   |


Step 3

| File 1(Input File) | File 2 | File 3 |
| ------------------ | ------ | ------ |
| a | b |   |
| b | a |   |
| c |   |   |


Step 4

| File 1(Input File) | File 2 | File 3 |
| ------------------ | ------ | ------ |
| a | b | c |
| b | a |   |
| c |   |   |

Step 5

| File 1(Input File) | File 2 | File 3 |
| ------------------ | ------ | ------ |
| a |  | c |
| b |  | b |
| c |  | a |


Step 6

| File 1(Input File) | File 2 | File 3 |
| ------------------ | ------ | ------ |
| a | c |  |
| b | b |  |
| c | a |  |

So the **Output** is data from File 2 - cba

This method worked fine but was very hectic process.  
This also ended up as a faluire

+ **APPROACH 4** 

After three successive failures came a solution which stood out till the last

Solution:

- Creating temporary files as many as output of(File size/chunk size).
- Each temporary file has a chunk of data in reversed order.
- Start reading from last file to first file in Append mode.


Since we are using temporary files the files are deleted as soon as the program is terminated so it eventually requires less memory and provides faster execution.
