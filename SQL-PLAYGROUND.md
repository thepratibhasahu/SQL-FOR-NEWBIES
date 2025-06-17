# Introduction
In this lesson, we will be learning different SQL commands to query a single table in a database.

One of the core purposes of the SQL language is to retrieve information stored in a database. This is commonly referred to as querying. Queries allow us to communicate with the database by asking questions and returning a result set with data relevant to the question.                                    
We will be querying a database with one table named movies.                           

**(1.)** We should get acquainted with the `movies` table.               
In the editor, type the following:                          
```sql
SELECT * FROM movies;
```
* What are the column names?

 → The columns are `id`, `name`, `genre`, `year`, and `imdb_rating`.
 ### 🟩 Output
```SQL
id   | name                                               | genre   | year | imdb_rating
-----+----------------------------------------------------+---------+------+--------------
1    | Avatar                                             | action  | 2009 | 7.9
2    | Jurassic World                                     | action  | 2015 | 7.3
3    | The Avengers                                       | action  | 2012 | 8.1
4    | The Dark Knight                                    | action  | 2008 | 9.0
5    | Star Wars: Episode I - The Phantom Menace          | action  | 1999 | 6.6
6    | Star Wars                                          | action  | 1977 | 8.7
7    | Avengers: Age of Ultron                            | action  | 2015 | 7.9
8    | The Dark Knight Rises                              | action  | 2012 | 8.5
9    | Pirates of the Caribbean: Dead Mans Chest          | action  | 2006 | 7.3
10   | Iron Man 3                                         | action  | 2013 | 7.3
...
221  | The Good, the Bad and the Ugly                     | NULL    | NULL | NULL
222  | Dawn of the Dead                                   | horror  | 1978 | NULL
223  | Shawn of the Dead                                  | comedy  | 2004 | NULL
224  | Star Wars: The Force Awakens                       | action  | 2015 | 8.1
225  | Star Wars: The Last Jedi                           | action  | 2017 | NULL
226  | The Shining                                        | horror  | 1985 | 8.4
227  | The Devil and Daniel Johnston                      | NULL    | 2005 | 8.0
228  | Ali Wong: Baby Cobra                               | NULL    | 2016 | NULL
229  | The Big Sick                                       | romance | 2017 | NULL
230  | Deadpool                                           | action  | 2016 | NULL
```
# Select
Previously, we learned that `SELECT` is used every time you want to query data from a database and `*` means all columns.                                           
Suppose we are only interested in two of the columns. We can select individual columns by their names (separated by a comma):
```SQL
SELECT column1, column2 
FROM table_name;
```
* To make it easier to read, we moved `FROM` to another line.

📝 Line breaks don’t mean anything specific in SQL. We could write this entire query in one line, and it would run just fine.

**(1)** Let’s only select the `name` and `genre` columns of the table.                               
In the code editor, type the following.
```SQL
SELECT name, genre FROM movies;
```
### 🟩 Output
```SQL
name	                       genre
Avatar	                       action
Jurassic World	               action
Shrek 2	                       comedy 
Toy Story 3	               comedy 
Gremlins	               horror
The Blair Witch Project	       horror
King Kong	               romance
Ghost	                       romance
Click	                       romance
The Lion King	                drama
The Devil and Daniel Johnston	  ∅
Ali Wong: Baby Cobra	          ∅
The Big Sick	               romance
Deadpool	                action
```
**2.** Now we want to include a third column.                                       
Edit your query so that it returns the `name`, `genre`, and `year` columns of the table.
```SQL
SELECT name, genre, year FROM movies;
```
### 🟩 Output
```SQL
name	                       genre         year
Avatar	                       action        2009
Jurassic World	               action        2015
Shrek 2	                       comedy        2004
Toy Story 3	               comedy        2010
Gremlins	               horror        1984
The Blair Witch Project	       horror        1999
King Kong	               romance       2005
Ghost	                       romance       1990
Click	                       romance       2006
The Lion King	                drama        1994
The Devil and Daniel Johnston	  ∅          2005
Ali Wong: Baby Cobra	          ∅          2016
The Big Sick	               romance       2017
Deadpool	                action       2016
```
# As
Knowing how `SELECT` works, suppose we have the code below:
```SQL
SELECT name AS 'Titles' FROM movies;
```
Can you guess what `AS` does?

**`AS`** is a keyword in SQL that allows you to rename a column or table using an alias. The new name can be anything you want as long as you put it inside of single quotes. Here we renamed the `name` column as `Titles`.

Some important things to note:                                      
* Although it’s not always necessary, it is considered best practice to surround your aliases with single quotes.
* Note that this practice is specific to SQLite, the RDBMS used in this exercise. When you work with other RDBMSs, notably PostgreSQL, `no quotes or double quotes` may be required in place of single quotes.
* When using `AS`, the columns are not being renamed in the table. The aliases only appear in the result.

**( 1.)** To showcase what the `AS` keyword does, select the `name` column and rename it with an alias of your choosing.           Place the alias inside single quotes:                         
* Note in the result, that the name of the column is now your alias.
```SQL
SELECT name AS 'pehchan' FROM movies;
```
### 🟩 Output
```SQL
        pehchan        
---------------------------
         Avatar         
     Jurassic World     
         Shrek 2        
       Toy Story 3      
        Gremlins        
The Blair Witch Project 
        King Kong        
          Ghost          
          Click          
      The Lion King      
The Devil and Daniel Johnston
  Ali Wong: Baby Cobra   
       The Big Sick      
         Deadpool        
```
**(2.)** Edit the query so that instead of selecting and renaming the `name` column, select the `imdb_rating` column and rename it as `IMDb`.
```SQL
SELECT imdb_rating AS 'IMDB' FROM movies;
```
### 🟩 Output
```SQL
      IMDB     
---------------
      7.9      
      7.3      
      8.1      
      9.0      
      6.6      
      8.7      
      7.9      
      8.5      
      7.3      
      NULL      
      7.3      
      6.0      
      NULL      
      7.3      
      6.3      
      7.4      
```
# Distinct
When we are examining data in a table, it can be helpful to know what distinct values exist in a particular column.         
`DISTINCT` is used to return unique values in the output. It filters out all duplicate values in the specified column(s).

→ For instance,
```SQL
SELECT tools FROM inventory;
```
→ might produce:

```SQL
      tools
-----------------
      Hammer
      Nails
      Nails
      Nails
```
→ By adding `DISTINCT` before the column name,
```SQL
SELECT DISTINCT tools FROM inventory;
```
```SQL
      tools
   ------------
      Hammer
      Nails
```
Filtering the results of a query is an important skill in SQL. It is easier to see the different possible `genres` in the `movie` table after the data has been filtered than to scan every row in the table.
**(1.)** Let’s try it out. In the code editor, type:                              
* What are the unique genres?
```SQL
SELECT DISTINCT genre FROM movies;
```
### 🟩 Output
```SQL
     genre     
---------------
    action     
    comedy     
    horror     
   romance     
    drama      
      ∅
```
📝 DISTINCT recognize empty values, too.

**(2.)** Now, change the code so we return the unique values of the year column instead.
```SQL
SELECT DISTINCT year FROM movies;
```
### 🟩 Output
```SQL
   year   
----------
  2009    
  2015    
  2012    
  2008    
  1999    
  1977    
  2006    
  2013    
  2002    
  2005    
  2004    
  2011    
  2014    
  2007    
  2010    
  1983    
  1996    
  2003    
  1980    
  1989    
  1984    
  1997    
  2001    
  1990    
  2000    
  1993    
  1992    
  1985    
  1994    
  1978    
  1979    
  1986    
  1998    
  1991    
  1939    
  1937    
  1982    
  1965    
  1995    
  1975    
  1988    
  1987
   ∅	   
  2017    
  2016    
```
# Where
We can restrict our query results using the `WHERE` clause in order to obtain only the information we want.

Following this format, the statement below filters the result set to only include top rated movies (IMDb ratings greater than 8):
```SQL
SELECT * FROM movies
WHERE imdb_rating > 8;
```
→ How does it work?
**1.** The `WHERE` clause filters the result set to only include rows where the following condition is true.

**2.** `imdb_rating > 8` is the condition. Here, only rows with a value greater than 8 in the `imdb_rating` column will be returned.                           
The `>` is an operator. Operators create a condition that can be evaluated as either true or false.                         

Comparison operators used with the `WHERE` clause are:                      
* `=` equal to
* `!=` not equal to
* `>` greater than
* `<` less than
* `>=` greater than or equal to
* `<=` less than or equal to

**(1.)** Suppose we want to take a peek at all the not-so-well-received movies in the database.                     
In the code editor, type:                           
* We are trying to retrieve all the movies with ratings lower than 5.
```SQL
SELECT * FROM movies 
WHERE imdb_rating < 5;
```
### 🟩 Output
```SQL
  id   |                   name                    |  genre  | year | imdb_rating
-------|-------------------------------------------|---------|------|-------------
  79   | Alvin and the Chipmunks: The Squeakquel   | comedy  | 2009 |     4.4     
 113   |               The Haunting                | horror  | 1999 |     4.9     
 120   | Scooby-Doo 2: Monsters Unleashed          | horror  | 2004 |     4.9     
 143   |                 Anaconda                  | horror  | 1997 |     4.6     
 149   |       The Twilight Saga: Eclipse          | romance | 2010 |     4.9     
 150   |      The Twilight Saga: New Moon          | romance | 2009 |     4.6     
 152   | The Twilight Saga: Breaking Dawn - Part 1 | romance | 2011 |     4.9     
 171   |          Fifty Shades of Grey             | romance | 2015 |     4.2     
```
**(2.)** Now retrieve all the recent movies, specifically those that were released after 2014.           
Select all the columns using *.
```SQL
SELECT * FROM movies
WHERE year > 2014;
```
### 🟩 Output
```SQL
  id  |               name               |  genre   | year | imdb_rating
------|----------------------------------|----------|------|-------------
  2   |         Jurassic World           |  action  | 2015 |     7.3     
  7   |    Avengers: Age of Ultron       |  action  | 2015 |     7.9     
 17   |          Furious Seven           |  action  | 2015 |     7.4     
 56   |            Inside Out            |  comedy  | 2015 |     8.6     
 58   |             Minions              |  comedy  | 2015 |     6.7     
156   |            Cinderella            | romance  | 2015 |     7.1     
171   |      Fifty Shades of Grey        | romance  | 2015 |     4.2     
224   |   Star Wars: The Force Awakens   |  action  | 2015 |     8.1     
225   |    Star Wars: The Last Jedi      |  action  | 2017 |    NULL     
228   |      Ali Wong: Baby Cobra        |   NULL   | 2016 |    NULL     
229   |           The Big Sick           | romance  | 2017 |    NULL     
230   |             Deadpool             |  action  | 2016 |    NULL     
```

















