 ## _**Assignment No 1 :** Reverse The Contents of an Input File._


Lets say the input is something like this
Input: “hello world
        I am ktgnair."
        
So the output should be like this
Output: “.riangtk ma I
         dlrow olleh”


+ APPROACH 1
As the question said reverse the contents so using fseek() and reading from the end of the file character by character was something that came to my mind.
It was working smoothly for file having small size but as soon as the file size increased the execution time increased gradually which didn't seem feasible.

+ APPROACH 2

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

+ APPROACH 3 
After two failure I started thinking the problem as some puzzle and was able to come up with a solution that is Tower of Honoi problem.

So with that as my approach i planned on using 3 files of which one is the input file and the next two are for swapping.

This method can be explained best with an example


Step 1
File 1(Input File) | File 2 | File 3
------------------ | ------ | ------
	a | a | b
	b |		
	c |
Step 2
File 1(Input File)	File 2	File 3 (Append a to file 3)
	a			b
	b			a
	c
Step 3
File 1(Input File)	File 2	File 3 (Move to file 2)
	a		b	
	b		a	
	c
Step 4
File 1(Input File)	File 2	File 3 (New data in file 3)
	a		b	c
	b		a
	c	
Step 5
File 1(Input File)	File 2	File 3 (Append file 2 to file 3)
	a			c
	b			b
	c 			a
Step 6
File 1(Input File)	File 2	File 3 (Move to file 2)
	a		c	
	b		b
	c		a


So Output can be data from file 2 - cba

This method worked fine but was very hectic process.
This also ended up as a faluire

+ APPROACH 4 

After three successive failures came a solution which stood out till the last

Solution:

- Creating temporary files as many as output of(File size/chunk size).
- Each temporary file has a chunk of data in reversed order.
- Start reading from last file to first file in Append mode.


Since we are using temporary files the files are deleted as soon as the program is terminated so it eventually requires less memory and provides faster execution.
