 **[Assignment 1](https://ktgnair.github.io/) / [Assignment 2](https://ktgnair.github.io/Assignment 2) / [Rules For Code](https://ktgnair.github.io/Rules For Code)**  
 
 **Rules for Indentation in a Code**  
 
 _**In this page i am going to discuss some basic points which we need to follow or lets say which if we follow will make our code look well structured and increase the readability.**_  


> **Variable Name**  

While writing the code most of the times we just blankly do the coding without any proper names given to the variables.
But in real world you need to make sure that you follow some rules.
Which might be those is what you might be thinking, so let me tell you nothing major just some basic points like

The variable names should be valid to the point.
Eg: For holding the name of company the variable name that should be defined can be simply “name” that is the variable declaration:
String name (is valid for the class Company.)

But String “companyname” is not. Because since we are creating a class for Company it’s obvious that the name variable defined in the scope of the class company contains the name of the company.

And the next thing is
The variable names should be in Camel-Case :
Eg: ‘errorCode’ is valid. 
    But errorcode, ErrorCode and Errorcode are invalid.


> **Class Name**  

Just like we had rules for variables we also have for class names.

The class name should follow “JAVA naming conventions” (In every new word in the class name the first character should be an upper-case ).
Eg: For class containing “Company detail” the class name should be

```
          CompanyDetail {
            class body...
         }
```

> **Method Name**  

The method names should be relevant to the scenario and should be written in Camel-Case
i.e  For a method to “create company” we’ll create a method named ‘createCompany()’ (As it’s valid and it follows both the rules.)

> **Proper Java Indentation**  

* Import Statements:

1. Should add setting in editor to alphabetically sort the importing statements.
2. Should import same packages in contiguous lines without an interrupting blank space. 

If you didn't understand the above statement please feel free to have a look in the example below

(It's the right way)                                   
import com.krishagni.CRM.rest.Company;                     
import com.krishagni.CRM.rest.Factory;
import com.krishagni.CRM.rest.Dao.CompanyDao;

(Its not)
import com.krishagni.CRM.rest.Company;

import com.krishagni.CRM.rest.Factory;
import com.krishagni.CRM.rest.Dao.CompanyDao;

* Curly Braces

The curly braces used in any Class, Method, Loops and Statements should be in proper format for enhancing the readability of the code.
Eg: 

```java
public CompanyDao getDao() {
    return dao;
}
```
It should not be like this one below because eventhough it might seem sweeter  believe me  it's not.
```java
public CompanyDao getDao() 
{
        return dao;
}
```
* Alignment

1. The code must be aligned in the proper way keeping 4 spaces before any method or variables.

*Code with Proper alignment*
```java 
public class Company {
    CompanyDao dao;
    Company comp = new Company();    
    
    public Factory getAddcomp() {
            return addcomp;
    }
}
```

2. There should be proper spacing before and after an operator.

Like:
int name = 10; 

Unlike:
    int name=10;

* Remove unwanted Spaces

Spaces which are not needed should not be used, the code should be kept in compact size and in readable format.

* Line Length

Maximum characters in a line should not be more than 120.

> **XML, HTML Indentation**

Before every tag two spaces need to be given to make it in standard format.

Like:
<bean id = "dao" class = "com.krishagni.CRM.rest.Dao.CompanyDaoImpl">
  <property name = "sessionFactory" ref = "sessionFactory"> </property>
</bean>

Unlike:
<bean id = "dao" class = "com.krishagni.CRM.rest.Dao.CompanyDaoImpl">
        <property name="sessionFactory" ref = "sessionFactory"></property>
</bean>

> **Database**

While integrating the hibernate file with database the database name, table name, column name need to be in upper-case so that it can be differentiated with java object properties.  

Something like this 
    <id name = "id" type = "int">
              <column name = "ID" />
            </id>
Which helps us understand that id (java object property) is different from ID (Database column name)
