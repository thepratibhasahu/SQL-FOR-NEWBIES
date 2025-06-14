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

# Statements

The code below is a SQL statement. A statement is text that the database recognizes as a valid command. Statements always end in a semicolon `;`.

```SQL
CREATE TABLE table_name (
   column_1 data_type, 
   column_2 data_type, 
   column_3 data_type
);
```
Let’s break down the components of a statement:

**1.** `CREATE TABLE` is a clause. Clauses perform specific tasks in SQL. By convention, clauses are written in capital              letters. Clauses can also be referred to as commands.           

**2.** `table_name` refers to the name of the table that the command is applied to.             

**3.** `(column_1 data_type`, `column_2 data_type`, `column_3 data_type)` is a parameter. A parameter is a list of columns, data types, or values that are passed to a clause as an argument. Here, the parameter is a list of column names and the associated data type.

The structure of SQL statements vary. The number of lines used does not matter. A statement can be written all on one line, or split up across multiple lines if it makes it easier to read. 

**1.** Let’s take a closer look at the statement we wrote before. In the code editor, type:
```SQL
SELECT * FROM celebs;
```
Run the code to observe the results, and ask yourself:

* Which parts of the statement are the clauses?                                                                             → `SELECT` and `FROM` are the clauses here.

* What table are we applying the command to?                                                                                 → We are applying the command to the `celebs` table.

# Create

`CREATE` statements allow us to create a new table in the database. You can use the CREATE statement anytime you want to `create` a new table from scratch. The statement below creates a new table named `celebs`.

**1.** `CREATE TABLE` is a clause that tells SQL you want to create a new table.                     
**2.** `celebs` is the name of the table.                                  
**3.** `(id INTEGER, name TEXT, age INTEGER)` is a list of parameters defining each column, or attribute in the table and its data type.

* `id` is the first column in the table. It stores values of data type `INTEGER`.
* `name` is the second column in the table. It stores values of data type `TEXT`.
* `age` is the third column in the table. It stores values of data type `INTEGER`.

**(1)** let’s create a celebs table.                                  
In the code editor, type:

```SQL
CREATE TABLE celebs (
   id INTEGER, 
   name TEXT, 
   age INTEGER
); 
```
### 🟩 Output
```SQL
Database Schema
   celebs
name	type
id	INTEGER
name	TEXT
age	INTEGER
```
📝 Insert commas after the first two columns are declared.                       
📝 End your statement with a `;`.

# Insert

The `INSERT` statement inserts a new row into a table.                                             
We can use the `INSERT` statement when you want to add new records.

**(1)** Write an SQL statement to insert a row into the celebs table with Name = 'Justin Bieber', ID = 1, and Age = 29.     In the code editor, type:

```SQL
INSERT INTO celebs (id, name, age) 
VALUES (1, 'Justin Bieber', 29);

SELECT * FROM celebs; 
```
### 🟩 Output
```sql
id	  name  	age
1	Justin Bieber	29
```

* `INSERT INTO` is a clause that adds the specified row or rows.
* `Celebs` is the table the row is added to.
* `(id, name, age)` is a parameter identifying the columns that data will be inserted into.
* `VALUES` is a clause that indicates the data being inserted.
* `(1, 'Justin Bieber', 29)` is a parameter identifying the values being inserted.
* `1`: an integer that will be added to `id` column.
* `'Justin Bieber'`: text that will be added to `name` column.
* `29`: an integer that will be added to `age` column.

📝 Make sure there is a set of parentheses around the column names and values to be inserted into the table!        
📝 Notice the single quotes around Justin Bieber. This is because text strings require quotes around them, while numbers don’t.

**(2)** Add three more celebrities to the table. Beneath your previous `INSERT` statement type.
```SQL
INSERT INTO celebs (id, name, age) 
VALUES (2, 'Beyonce Knowles', 42); 

INSERT INTO celebs (id, name, age) 
VALUES (3, 'Jeremy Lin', 35); 

INSERT INTO celebs (id, name, age) 
VALUES (4, 'Taylor Swift', 33);

SELECT * FROM celebs; 
```
### 🟩 Output
```SQL
id	  name	        age	
1 	Justin Bieber	 29       
2	Beyonce Knowles  42      
3	Jeremy Lin	 35       	
4	Taylor Swift	 33
```
# Select

`SELECT` statements are used to fetch data from a database. In the statement below, `SELECT` returns all data in the `name` column of the `celebs` table.
```SQL
SELECT name FROM celebs;
```
### 🟩 Output
```sql
   name
Justin Bieber
Beyonce Knowles
Jeremy Lin
Taylor Swift
```
**1.** `SELECT` is a clause that indicates that the statement is a query. You will use SELECT every time you query data from a database.                        
**2.** `name` specifies the column to query data from.                          
**3.** `FROM celebs` specifies the name of the table to query data from. In this statement, data is queried from the `celebs` table.

* You can also query data from all columns in a table with `SELECT`.
```SQL
SELECT * FROM celebs;
```
### 🟩 Output
```SQL
id	  name	        age	
1 	Justin Bieber	 29       
2	Beyonce Knowles  42      
3	Jeremy Lin	 35       	
4	Taylor Swift	 33
```
* `*` is a special wildcard character that we have been using. It allows you to select every column in a table without having to name each one individually.

# Alter

The `ALTER TABLE` statement adds a new column to a table. You can use this command when you want to add columns to a table.

**(1)** Write an SQL statement to add a new column twitter_handle to the celebs table. In the code editor, type the command to add this column.

```SQL
ALTER TABLE celebs 
ADD COLUMN twitter_handle TEXT;

SELECT * FROM celebs; 
```
### 🟩 Output
```SQL
id	  name	        age	twitter_handle
1 	Justin Bieber	 29       ∅
2	Beyonce Knowles  42       ∅
3	Jeremy Lin	 35       ∅	
4	Taylor Swift	 33       ∅
```
**1.** `ALTER TABLE` is a clause that lets you make the specified changes.                        
**2.** `celebs` is the name of the table that is being changed.                               
**3.** `ADD COLUMN` is a clause that lets you add a new column to a table:                      
 * `twitter_handle` is the name of the new column being added.
 * `TEXT` is the data type for the new column.

 **4.** `NULL` is a special value in SQL that represents missing or unknown data. Here, the rows that existed before the column was added have `NULL` (∅) values for `twitter_handle`.

 # Update

The `UPDATE` statement edits a row in a table. You can use the `UPDATE` statement when you want to change existing records.

**(1)** Write an SQL statement to update the record in the celebs table where the id is 4, setting the twitter_handle to @taylorswift13. In the code editor, type the command to update Taylor Swift’s Twitter handle.

```sql
UPDATE celebs 
SET twitter_handle = '@taylorswift13' 
WHERE id = 4;

SELECT * FROM celebs; 
```
### 🟩 Output
```SQL
id	  name	        age	twitter_handle
1 	Justin Bieber	 29       ∅
2	Beyonce Knowles  42       ∅
3	Jeremy Lin	 35       ∅	
4	Taylor Swift	 33     @taylorswift13
```
**1.** `UPDATE` is a clause that edits a row in the table.                              
**2.** `celebs` is the name of the table.                                   
**3.** `SET` is a clause that indicates the column to edit.

* `twitter_handle` is the name of the column that is going to be updated.
* `@taylorswift13` is the new value that is going to be inserted into the `twitter_handle` column.

**4.** WHERE is a clause that indicates which row(s) to update with the new column value. Here the row with a 4 in the id column is the row that will have the twitter_handle updated to @taylorswift13.

# Delete

The `DELETE FROM` statement deletes one or more rows from a table. You can use the statement when you want to delete existing records.

**(1)** Delete all of the rows that have a `NULL` value in the twitter handle column. In the code editor type:  
& How many rows exist in the `celebs` table now?

```SQL
DELETE FROM celebs 
WHERE twitter_handle IS NULL;

SELECT * FROM celebs; 
```
### 🟩 Output
```SQL
id	  name	        age	twitter_handle
4	Taylor Swift	 33     @taylorswift13
```
**1.** `DELETE FROM` is a clause that lets you delete rows from a table.             
**2.** `celebs` is the name of the table we want to delete rows from.                  
**3.** `WHERE` is a clause that lets you select which rows you want to delete. Here we want to delete all of the rows where the twitter_handle column IS NULL.                             
**4.** `IS NULL` is a condition in SQL that returns true when the value is `NULL` and false otherwise.

# Constraints

Constraints in SQL are the rules applied to the values of individual columns. They add information about how a column can be used after specifying the data type for a column. They can be used to tell the database to reject inserted data that does not adhere to a certain restriction.             
The statement below sets constraints on the celebs table.
```SQL
CREATE TABLE celebs (
   id INTEGER PRIMARY KEY, 
   name TEXT UNIQUE,
   date_of_birth TEXT NOT NULL,
   date_of_death TEXT DEFAULT 'Not Applicable'
);
```
* `PRIMARY KEY` columns can be used to uniquely identify the row. Attempts to insert a row with an identical value to a row already in the table will result in a constraint violation which will not allow you to insert the new row.                   → `id` column is the `PRIMARY KEY`.

* `UNIQUE` columns have a different value for every row. This is similar to `PRIMARY KEY` except a table can have many different `UNIQUE` columns.                                                                                                 → `name` column is `UNIQUE`.

* `NOT NULL` columns must have a value. Attempts to insert a row without a value for a `NOT NULL` column will result in a constraint violation and the new row will not be inserted.
→ `date_of_birth` column is `NOT NULL`.

* `DEFAULT` columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column.                                                                                            →  `date_of_death` column has a `DEFAULT` of 'Not Applicable'.

 📝 Note: There can be only one `PRIMARY KEY` column per table, but there can be multiple `UNIQUE` columns.



































































