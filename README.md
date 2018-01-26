 ## _Assignment No 1 : Reverse The Contents of an Input File._


Lets say the input is something like this

Input: “hello world
        I am ktgnair."
        
So the output should be like this

Output: “.riangtk ma I
         dlrow olleh”


> **APPROACH 1**

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

> **APPROACH 2**

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

> **APPROACH 3** 

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

> **APPROACH 4** 

After three successive failures came a solution which stood out till the last

Solution:

- Creating temporary files as many as output of(File size/chunk size).
- Each temporary file has a chunk of data in reversed order.
- Start reading from last file to first file in Append mode.


Since we are using temporary files the files are deleted as soon as the program is terminated so it eventually requires less memory and provides faster execution.

```c
#include<stdio.h>
#include<string.h>
#include <sys/stat.h>
#include<errno.h>

int temp_file_num = 0;

void reverse_buffer(char buffer[])
{
	FILE *write_file_pointer = NULL;	
	int buffer_length = 0;
	int index = 0;
	char temp_char = '\0';
	char temp_file[15] = {NULL};
	
	buffer_length = strlen(buffer);
	buffer_length = buffer_length - 2;
	buffer[buffer_length] = '\0';
	buffer_length = buffer_length - 1;
	
	while(index < buffer_length)				//for reversing buffer array.
	{
	   temp_char = buffer[index];
	   buffer[index] = buffer[buffer_length];
	   buffer[buffer_length] = temp_char;
	   index++;
	   buffer_length--;
	}

	sprintf(temp_file,"%d.txt",temp_file_num++);		//generate temp file name.
	write_file_pointer = fopen(temp_file,"w");		//creating temp file.
	fputs(buffer,write_file_pointer);			//writing buffer to temp file.
	fclose(write_file_pointer);				//close temp file.
			
}

void file_append(int temp_file_num)
{
	FILE *read_file_pointer = NULL,*write_file_pointer = NULL;
	char temp_file[11] = {NULL};
	char buffer[3999990] = {NULL};
	int file_size = 0;
	
	sprintf(temp_file,"%d.txt",temp_file_num);
	write_file_pointer = fopen("output1.txt","a");			//opening output file in append mode
	read_file_pointer = fopen(temp_file,"r");			//opening temp file to read data
	fread(buffer, 3999990 , 1 , read_file_pointer);			//reading chunk 
	buffer[3999990]='\0';
	   
	fputs(buffer,write_file_pointer);				//appending to ouput file.
	
	fclose(read_file_pointer);
	fclose(write_file_pointer);
}
void file_delete(int temp_file_num)			
{
	char temp_file[11]={NULL};
	
	sprintf(temp_file,"%d.txt",temp_file_num);
	unlink(temp_file);
}

int main()
{
	long file_size=0,index=0;
	FILE *file_pointer=NULL, *read_file_pointer=NULL;
	char buffer[3999990]={NULL};
	char temp_file[15]={NULL};
	
  	file_pointer = fopen("a.txt","r");

	struct stat file_info;
	stat("a.txt", &file_info);
  	file_size=file_info.st_size;
	printf("Size of input file: %ld\n",file_size);		//retriving input file size.
	
        while(file_size>3999990-1)				//reading input file chunk by chunk file.
	{
             fread(buffer,3999990,1,file_pointer);
	     reverse_buffer(buffer);
	     file_size=file_size-3999990;	
	 }
				
	buffer[file_size]='\0';							
	fread(buffer,file_size,1,file_pointer);		
	reverse_buffer(buffer);

	fclose(file_pointer);

	file_pointer = NULL;
	file_pointer = fopen("output1.txt","w");

	sprintf(temp_file,"%d.txt",temp_file_num - 1);		//retriving filename.
	read_file_pointer = fopen(temp_file,"r");		//open that temp file in read mode.

	stat(temp_file, &file_info);
  	file_size = file_info.st_size;				//retriving file size.

	fread(buffer, file_size , 1 , read_file_pointer);	//read in buffer
  	buffer[file_size]='\0';

	fputs(buffer, file_pointer);				//write to ouput file.
	
	fclose(file_pointer);
	fclose(read_file_pointer);				//closing opened files.

	for(index = temp_file_num - 2 ; index >=0 ; index--)	//for appending
	file_append(index);

	for(index = temp_file_num - 1 ; index >=0 ; index--)	//for deleting files
	file_delete(index);
	
	return 0;	
}
```
The above source code seems good as compared to my other approches but its not efficient.  
My mentor suggested me some tricks to make it efficient such as making the reverse function short, avoiding the duplication of code in main() just after while loop the next 3 lines of operation are already been done in the while loop.  

So after those changes the final code which he approved :+1: looked something like this

```c
#include<stdio.h>
#include<string.h>
#include <sys/stat.h>
#include<errno.h>

int temp_file_num = 0;

void reverse_buffer(char buffer[])
{
	FILE *write_file_pointer = NULL;	
	int i=0,j=0;
	char temp_file[15] = {NULL},rev_buffer[3999990]={NULL};
	
	for(i=0,j= strlen(buffer)-1 ; j >= 0 ; i++,j--)
	rev_buffer[i]=buffer[j];
	
	sprintf(temp_file,"%d.txt",temp_file_num++);		//generate temp file name.
	write_file_pointer = fopen(temp_file,"w");		//creating temp file.
	fputs(rev_buffer,write_file_pointer);			//writing buffer to temp file.
	fclose(write_file_pointer);				//close temp file.
}

void file_append(int temp_file_num)
{
	FILE *read_file_pointer = NULL,*write_file_pointer = NULL;
	char temp_file[11] = {NULL};
	char buffer[3999990] = {NULL};
	int file_size = 0;
	
	sprintf(temp_file,"%d.txt",temp_file_num);
	write_file_pointer = fopen("output1.txt","a");			//opening output file in append mode
	read_file_pointer = fopen(temp_file,"r");			//opening temp file to read data
	
	fread(buffer, 3999990 , 1 , read_file_pointer);			//reading chunk 
	buffer[3999990]='\0';
	   
	fputs(buffer,write_file_pointer);				//appending to ouput file.
		
	fclose(read_file_pointer);

	fclose(write_file_pointer);
}
void file_delete(int temp_file_num)			
{
	char temp_file[11]={NULL};
	
	sprintf(temp_file,"%d.txt",temp_file_num);
	unlink(temp_file);
}

int main()
{
	long file_size=0,index=0,n=0;
	FILE *file_pointer=NULL, *read_file_pointer=NULL;
	char buffer[3999990]={NULL};
	char temp_file[15]={NULL};

  	file_pointer = fopen("1gb.txt","r");
	
	struct stat file_info;
	stat("1gb.txt", &file_info);
  	file_size=file_info.st_size;
	printf("Size of input file: %ld\n",file_size);		//retriving input file size.
	
	n= 3999990 % file_size;
		
        do			//reading input file chunk by chunk file.
	{
             fread(buffer,n,1,file_pointer);
	     reverse_buffer(buffer);
	     file_size=file_size-n;
	     n=3999990;

	 }while(file_size>0);

	fclose(file_pointer);
	
	file_pointer = NULL;
	file_pointer = fopen("output1.txt","w");

	sprintf(temp_file,"%d.txt",temp_file_num - 1);		//retriving filename.
	read_file_pointer = fopen(temp_file,"r");		//open that temp file in read mode.

	stat(temp_file, &file_info);
  	file_size = file_info.st_size;				//retriving file size.

	fread(buffer, file_size , 1 , read_file_pointer);	//read in buffer
  	buffer[file_size]='\0';

	fputs(buffer, file_pointer);				//write to ouput file.
	
	fclose(file_pointer);
	fclose(read_file_pointer);				//closing opened files.

	for(index = temp_file_num - 2 ; index >=0 ; index--)	//for appending
	file_append(index);

	for(index = temp_file_num - 1 ; index >=0 ; index--)	//for deleting files
	file_delete(index);

	return 0;	
}
```
:smile:
