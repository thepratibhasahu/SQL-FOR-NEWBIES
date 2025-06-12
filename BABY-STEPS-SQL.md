# Introduction to SQL

SQL Structured Query Language, is a programming language designed to manage data stored in 
Preview: Docs A relational database is a store of data organized in tables made of columns and rows, and the relationships between those tables.
relational databases. SQL operates through simple, declarative statements. This keeps data accurate and secure, and helps maintain the integrity of 
Preview: Docs Loading link description
databases, regardless of size.

The SQL language is widely used today across web frameworks and database applications. Knowing SQL gives you the freedom to explore your data, and the power to make better decisions. By learning SQL, you will also learn concepts that apply to nearly every data storage system.

# Types of Statements

SQL statements can be broadly grouped into four different classes, or sub-languages:

**Data Query Language (DQL):** Includes commands for performing queries on data within schema objects, retrieving some schema relation based on the query passed to it.

**SELECT:** retrieves data from the database.

**Data Definition Language (DDL):** Includes commands used to define the database schema. These commands are used to create and modify the structure of database objects.

**CREATE:** creates an object in the database.

**DROP:** deletes an object from the database.

**ALTER:** changes the definition of an existing object in the database.

**Data Manipulation Language (DML):** Includes commands used to modify the data stored in the database. Examples include:

**INSERT:** inserts new data into a database table.

**UPDATE:** alters data in a database table.

**DELETE:** removes data from a database table.

**Data Control Language (DCL):** Includes commands dealing with the controls and properties of the DBMS, such as rights and permissions to database objects.

**GRANT:** grants a user permissions on a database object.

**REVOKE:** removes a user’s permissions on a database object.


**1. Let’s begin by entering a SQL command.**

```SQL
 SELECT * FROM celebs;
```

**Common errors:**                 
* Did you forget the *?           
* Did you forget the ;?               
* The table should show four rows of data and three columns (id, name, and age).            
We will explain what this line means in a bit!

# Database

A database is a collection of structured information stored so it can be easily accessed and updated. In a computer system, databases are commonly accessed through a database management system, referred to as a DBMS.

# Types of Databases
There are many different ways for database systems to structure and organize data. The type of database used is dependent on the type of data being stored, and the intended use for it.

# Object Databases
Object databases structure their data in the form of objects (as used in object-oriented programming) rather than tables. This is useful in software development where the application using the data, and the DBMS manipulating the data, can both use the same model of the data.

# Object-Relational Databases
A hybrid of the above two models. Unlike pure object databases where the database is primarily a persistent store for objects created by a program written in an object-oriented programming language, object-relational databases are manipulated via a query language as in relational databases. Yet they still support objects, classes and inheritance like a pure object database.

# NoSQL Databases
NoSQL databases are also known as nonrelational databases. They are a wide variety of databases that use different structures for data rather than the tables used in relational databases. They are implemented using various different structures for different purposes. For example:

* Key–Value Store: Stores data in an associative array where data is stored as a collection of key-value pairs where any possible key only appears once in the collection.            
* Document Store: Stores data as documents in some standard format such as XML, TAML or JSON. Documents are stored in the database with a unique key representing that document.                  
* Graph Database: Stores data as elements connected by a finite number of relations, such as a subway map or a network of friends on Facebook.
  
# Relational Databases

 A relational database is a database that organizes information into one or more tables. Here, the relational database contains one table.                
 A table is a collection of data organized into rows and columns. Tables are sometimes referred to as relations. Here the table is `celebs`.                        
 A column is a set of data values of a particular type. Here, `id`, `name`, and `age` are the columns.           

 A row is a single record in a table. The first row in the celebs table has:                
* An `id` of `1`                
* A `name` of `Justin Bieber`
* An `age` of `29`

All data stored in a relational database is of a certain data type.       
Some of the most common data types are:          
* `INTEGER`, a positive or negative whole number
* `TEXT`, a text string
* `DATE`, the date formatted as YYYY-MM-DD
* `REAL`, a decimal value
  
# Data Types           
Data types provide categories for values we store in tables. Types are assigned to fields through table creation and are responsible for determining some of the attributes and constraints (such as the amount of memory allocated) of data stored within a given table.                      
SQL supports a range of data types across widely used classes of data, such as the following:            
* Numeric types                     
* String or character types                       
* Temporal types for dates and times

These data types are found across all flavors of SQL. However, some versions of SQL may support several distinct data types of a particular class while others may only have one (the definitions below are specific to PostgreSQL).

* **integer:** A whole number between -2147483648 and 2147483647. Postgres also includes alternatives smallint and bigint.
* **real:** A floating-point type that has variable-precision with a maximum range of 6 decimals.       
* **text:** A range of characters of unlimited length.      
* **char:** A range of characters of fixed length n, an error will be raised for any entries that exceed length n. Entries that are shorter than n will be space-padded.              
* **varchar:** A range of characters of variable length with a maximum length n. However, unlike char there is no space-padding to extend entries shorter than n.            
* **date:** A date (without any time value), such as 2022-06-21 (ISO 8601 format) and 6/21/2022.


















