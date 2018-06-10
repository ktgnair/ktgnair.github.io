**[Database](https://ktgnair.github.io/Database) / [Installation Guide](https://ktgnair.github.io/Installation Guide) / [Session II](https://ktgnair.github.io/Session II) / [Session III](https://ktgnair.github.io/Session III)**  


_**This is a tutorial to get you all started with basics of database using MYSQL.**_   

Following are the topics which will be covered in this session    
- [x] Create a database  
- [x] Create table  
- [x] Insert records into the table  
- [x] Select query  
- [x] Where clause  
- [x] Using Wildcards  
In my whole tutorial i will explain the complete mysql using examples and not just syntax since explaining with examples is more understandable as compared to syntax.  

<b>Step 1: Create a database.</b>  
To create any powerfull database in mysql a simple line as shown below is used.  
> ![Create DB](/images/db/createdb.png)

Here TestDb is the name of the database.  
After creating the database you need to type this  
> ![Use DB](/images/db/usedb.png)  
to tell mysql that you are going to use this database.  

<b>Step 2: Create table.</b>  
Next step is to create a table.  
The syntax for creating a table is  
> ![Create Table](/images/db/createtableEmp.png)  
Where Employee is name of table which has the following fields.  

<b>Step 3: Insert records into the table.</b>  
> ![Insert](/images/db/InsertinEmp.png)  
As you can see while inserting i have also specified the names of the fields right after table name and then wrote the values that needs to be inserted, this is a good practice.  
And if you have noticed properly then you will know that i have not inserted the Employee_id -- <b>Why?</b>  
Because while creating the table i mentioned it as auto-increment, so it will automatically place the id.  

In the same way try inserting more records.  

<b>Step 4: Select query</b>   
This query will display all the records that you have inserted in your table.  
> ![Select All](/images/db/select*Emp.png)  
The * in the query indicates all records, if you need a particular record then write the name of that like this.  

To show the names of all the Employee  
> ![Select Particular](/images/db/selectnameEmp.png)  

<b>Step 5: Using 'where' clause</b>  
For explaining this i have created another table and also inserted some records into it, which is shown below  
> ![Item](/images/db/itemtable.png)  

The where clause is to filter records.  
Say I have to write query for getting all the names of items whose language is "Hindi", so the most often thought that comes to mind is to use '=' but that's not right because we need the exact match that can be obtained by using this.  
> ![Where](/images/db/whereclause.png)  

We are using LIKE since we are finding for text but if we need to find integers then we can use '='  
Getting all the details where no of items is 10   
> ![Using =](/images/db/using=.png)  

<b>Using Wildcards</b>  
Wildcards are used for pattern matching  

1. _like%_  
I need all the records from the Item table whose name starts with 'The'  
> ![Like %](/images/db/like%.png)  
Here i have used 'The%' which means anything after 'The'.  

2. _%like_  
I need all the records from the Item table whose name ends with 'd'(just an example not a real case senario)  
> ![% Like](/images/db/%d.png)
The '%d' means anything before 'd'.  

3. _%like%_  
I need all the records from the Item table whose genre has '/'  
> ![% Like %](/images/db/%like%.png)  
The '%/%' means anything before or after '/'  

This concludes our Session I.  
Hope you all understood this small part of database, now lets move on to Session II  
