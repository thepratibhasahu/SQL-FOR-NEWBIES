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
# Like I
`LIKE` can be a useful operator when you want to compare similar values.

The `movies` table contains two films with similar titles, ‘Se7en’ and ‘Seven’.

How could we select all movies that start with ‘Se’ and end with ‘en’ and have exactly one character in the middle?
```SQL
SELECT * FROM movies
WHERE name LIKE 'Se_en';
```
* `LIKE` is a special operator used with the `WHERE` clause to search for a specific pattern in a column.
* `name LIKE 'Se_en'` is a condition evaluating the `name` column for a specific pattern.
* `Se_en` represents a pattern with a wildcard character.
* The `_` means you can substitute any individual character here without breaking the pattern. The names `Seven` and `Se7en` both match this pattern.
### 🟩 Output
```SQL
id	name	genre	year	imdb_rating
219	Se7en	drama	1995	  8.6
220	Seven	drama	1979	  6.1
```
# Like II
The percentage sign `%` is another wildcard character that can be used with `LIKE`.

This statement below filters the result set to only include movies with names that begin with the letter ‘A’:
```SQL
SELECT * FROM movies
WHERE name LIKE 'A%';
```
`%` is a wildcard character that matches zero or more missing characters in the pattern. For example:

* `A%` matches all movies with names that begin with letter ‘A’
* `%a` matches all movies that end with ‘a’

We can also use `%` both before and after a pattern:                            
→ How many movie titles contain the word ‘man’?
```SQL
SELECT * FROM movies 
WHERE name LIKE '%man%';
```
### 🟩 Output
```SQL
  id  |                name                       |  genre   | year | imdb_rating
------|-------------------------------------------|----------|------|-------------
  9   | Pirates of the Caribbean: Dead Mans Chest | action   | 2006 |     7.3     
 10   |             Iron Man 3                    |  action  | 2013 |     7.3     
 11   |             Spider-Man                    |  action  | 2002 |     7.3     
 14   |            Spider-Man 2                   |  action  | 2004 |     7.3     
 18   |            Spider-Man 3                   |  action  | 2007 |     6.2     
 21   |              Iron Man                     |  action  | 2008 |     7.9     
 23   |             Iron Man 2                    |  action  | 2010 |     7.1     
 31   |            Man of Steel                   |  action  | 2013 |     7.2     
 34   |      The Amazing Spider-Man               |  action  | 2012 |     7.1     
 39   |               Batman                      |  action  | 1989 |     7.6     
164   |            Pretty Woman                   |  romance | 1990 |     6.9     
208   |              Rain Man                     |  drama   | 1988 |     8.0
```
* Here, any movie that contains the word ‘man’ in its name will be returned in the result.                                
* `LIKE` is not case sensitive. ‘Batman’ and ‘Man of Steel’ will both appear in the result of the query above.

**(2)** Let’s try one more.                                       
Edit the query so that it selects all the information about the movie titles that begin with the word ‘The’.        
You might need a space in there!
```SQL
SELECT * FROM movies
WHERE name LIKE 'The %';
```
### 🟩 Output
```SQL
  id  |                 name                    |   genre   | year | imdb_rating
------|-----------------------------------------|-----------|------|-------------
  3   |           The Avengers                  |  action   | 2012 |     8.1     
  4   |          The Dark Knight                |  action   | 2008 |     9.0     
  8   |       The Dark Knight Rises             |  action   | 2012 |     8.5     
 33   |        The Matrix Reloaded              |  action   | 2003 |     7.2     
 34   |      The Amazing Spider-Man             |  action   | 2012 |     7.1     
 35   |          The Incredibles                |  action   | 2004 |     8.0     
 37   |           The Lego Movie                |  action   | 2014 |     7.8     
 49   |  The Lost World: Jurassic Park          |  action   | 1997 |     6.5     
 63   |           The Hangover                  |  comedy   | 2009 |     7.8     
 67   |       The Hangover Part II              |  comedy   | 2011 |     6.5     
 86   |             The Lorax                   |  comedy   | 2012 |     6.5     
101   |     The Blair Witch Project             |  horror   | 1999 |     6.4     
102   |           The Conjuring                 |  horror   | 2013 |     7.5     
103   |             The Ring                    |  horror   | 2002 |     7.1     
104   |            The Grudge                   |  horror   | 2004 |     5.9     
112   |            The Others                   |  horror   | 2001 |     7.6     
113   |          The Haunting                   |  horror   | 1999 |     4.9     
116   |     The Amityville Horror               |  horror   | 1979 |     6.2     
126   | The Texas Chainsaw Massacre             |  horror   | 2003 |     6.2     
129   |          The Ring Two                   |  horror   | 2005 |     5.4     
132   | The Exorcism of Emily Rose              |  horror   | 2005 |     6.7     
136   |       The Purge: Anarchy                |  horror   | 2014 |     6.5     
140   |         The Forgotten                   |  horror   | 2004 |     5.8     
141   |     The Final Destination               |  horror   | 2009 |     5.2     
146   |            The Purge                    |  horror   | 2013 |     5.6     
149   |   The Twilight Saga: Eclipse            | romance   | 2010 |     4.9     
150   |  The Twilight Saga: New Moon            | romance   | 2009 |     4.6     
151   |The Twilight Saga: Breaking Dawn - Part 2| romance   | 2012 |     5.6     
152   |The Twilight Saga: Breaking Dawn - Part 1| romance   | 2011 |     4.9     
173   |           The Proposal                  | romance   | 2009 |     6.7     
174   |       The Sound of Music                | romance   | 1965 |     8.0     
183   |        The Great Gatsby                 | romance   | 2013 |     7.3     
191   |          The Lion King                  |  drama    | 1994 |     8.5     
193   |         The Sixth Sense                 |  drama    | 1999 |     8.2     
196   |         The Blind Side                  |  drama    | 2009 |     7.7     
204   |        The Perfect Storm                |  drama    | 2000 |     6.4     
207   |         The Karate Kid                  |  drama    | 2010 |     6.2     
212   |             The Help                    |  drama    | 2011 |     8.1     
221   |   The Good, the Bad and the Ugly        |   NULL    | NULL |    NULL     
226   |           The Shining                   |  horror   | 1985 |     8.4     
227   | The Devil and Daniel Johnston           |   NULL    | 2005 |     8.0     
229   |           The Big Sick                  | romance   | 2017 |    NULL     
```
* There is also a space in between because we don’t want words like ‘There’, ‘They’, etc.

📝 What are the different use cases of the `LIKE` operator?

* `LIKE c%` finds any values that start with the letter ‘c’
* `LIKE %c` finds any values that end with the letter ‘c’
* `LIKE %re%` finds values that have ‘re’ in any position
* `LIKE _a%` finds any values that have the letter ‘a’ in the second index
* `LIKE a_%_%` finds any values that start with ‘a’ and are at least 3 characters in length.
* `LIKE a%r` finds any values that start with ‘a’ and end with ‘r’.
# Is Null
By this point of the lesson, you might have noticed that there are a few missing values in the `movies` table. More often than not, the data you encounter will have missing values.

Unknown values are indicated by `NULL`.

It is not possible to test for `NULL` values with comparison operators, such as `=` and `!=`.

Instead, we will have to use these operators:                                  
* `IS NULL`
(The IS NULL operator checks if a value is NULL.)
* `IS NOT NULL`
(The IS NOT NULL operator checks if a value is not equal to NULL.)

→ To filter for all movies with an IMDb rating:
```SQL
SELECT name FROM movies 
WHERE imdb_rating IS NOT NULL;
```
**(1.)** Now let’s do the opposite.                           
Write a query to find all the movies without an IMDb rating.                                      
Select only the `name` column!               
* We want to query for movies that have a missing value in their `imdb_rating` field:
```SQL
SELECT name FROM movies
WHERE imdb_rating IS NULL;
```
### 🟩 Output
```SQL
               name               
----------------------------------
 The Good, the Bad and the Ugly  
       Dawn of the Dead          
      Shawn of the Dead          
   Star Wars: The Last Jedi      
    Ali Wong: Baby Cobra         
         The Big Sick            
           Deadpool
```
# Between
The `BETWEEN` operator is used in a `WHERE` clause to filter the result set within a certain range. It accepts two values that are either numbers, text or dates.

For example, this statement filters the result set to only include movies with `years` from 1990 up to, and including 1999.
```SQL
SELECT * FROM movies
WHERE year BETWEEN 1990 AND 1999;
```
When the values are text, `BETWEEN` filters the result set for within the alphabetical range.

In this statement, `BETWEEN` filters the result set to only include movies with `names` that begin with the letter ‘A’ up to, but not including ones that begin with ‘J’.
```SQL
SELECT * FROM movies
WHERE name BETWEEN 'A' AND 'J';
```
However, if a movie has a name of simply ‘J’, it would actually match. This is because BETWEEN goes up to the second value — up to ‘J’. So the movie named ‘J’ would be included in the result set but not ‘Jaws’.

**(1)** Using the `BETWEEN` operator, write a query that selects all information about movies whose `name` begins with the letters ‘D’, ‘E’, and ‘F’.
```SQL
SELECT * FROM movies
WHERE name BETWEEN 'D' AND 'G';
```
### 🟩 Output
```SQL
  id  |               name                |  genre   | year | imdb_rating
------|-----------------------------------|----------|------|-------------
203   |       Dances with Wolves          |  drama   | 1990 |     8.0     
128   |           Dark Shadows            |  horror  | 2012 |     6.2     
222   |         Dawn of the Dead          |  horror  | 1978 |    NULL     
200   | Dawn of the Planet of the Apes    |  drama   | 2014 |     7.7     
230   |             Deadpool              |  action  | 2016 |    NULL     
 68   |          Despicable Me            |  comedy  | 2010 |     7.7     
 55   |         Despicable Me 2           |  comedy  | 2013 |     7.5     
122   |             Dracula               |  horror  | 1992 |     7.5     
168   |               Elf                 | romance  | 2003 |     6.9     
139   |           End of Days             |  horror  | 1999 |     5.7     
 45   |        Fast & Furious 6           |  action  | 2013 |     7.2     
171   |      Fifty Shades of Grey         | romance  | 2015 |     4.2     
 54   |          Finding Nemo             |  comedy  | 2003 |     8.2     
148   |           Forrest Gump            | romance  | 1994 |     8.8     
123   |        Freddy vs. Jason           |  horror  | 2003 |     5.8     
145   |        Friday the 13th            |  horror  | 2009 |     5.6     
 53   |              Frozen               |  comedy  | 2013 |     7.6     
 17   |           Furious Seven           |  action  | 2015 |     7.4     
```
📝 `BETWEEN 'D' AND 'F'` should not be the condition because it would return names that begin with ‘D’ and ‘E’, but not ‘F’ (unless there was a movie with the single letter name of “F”).                          
📝 And don’t forget to capitalize `D` and `G`!                                 
📝 `BETWEEN` is case-sensitive. If the condition is `BETWEEN 'a' AND 'z'`, it would only return lowercase (a-z) results and not uppercase (A-Z).

**(2.)** Using the `BETWEEN` operator, write a new query that selects all information about movies that were released from the year 1970 up to and including 1979.
```SQL
SELECT * FROM movies
WHERE year BETWEEN 1970 AND 1979;
```
### 🟩 Output
```SQL
  id  |            name             |  genre  | year | imdb_rating
------|-----------------------------|---------|------|-------------
  6   |          Star Wars          | action  | 1977 |     8.7     
109   |           Jaws 2            | horror  | 1978 |     5.7     
116   |  The Amityville Horror      | horror  | 1979 |     6.2     
194   |            Jaws             | drama   | 1975 |     8.1     
220   |           Seven             | drama   | 1979 |     6.1     
222   |       Dawn of the Dead      | horror  | 1978 |    NULL     
```
📝 Remember, `BETWEEN` two numbers is inclusive of the second number.                
📝 Notice that there is a movie from 1979 in the result.                       
📝 Also, numeric values (INTEGER or REAL data types) don’t need to be wrapped with single quotes, whereas TEXT values do.

# And
Sometimes we want to combine multiple conditions in a `WHERE` clause to make the result set more specific and useful.

One way of doing this is to use the `AND` operator. Here, we use the `AND` operator to only return 90’s romance movies.
```SQL
SELECT * FROM movies
WHERE year BETWEEN 1990 AND 1999
AND genre = 'romance';
```
* `year BETWEEN 1990 AND 1999` is the 1st condition.
* `genre = 'romance'` is the 2nd condition.
* `AND` combines the two conditions.

<img width="268" alt="image" src="https://github.com/user-attachments/assets/ff2eb538-3bac-4d99-a91c-1e24d5d67ac5" />

With AND, both conditions must be true for the row to be included in the result.

**(1.)** In the previous exercise, we retrieved every movie released in the 1970’s.              
Now, let’s retrieve every movie released in the 70’s, that’s also well received.                   
In the code editor, type:
```SQL
SELECT * FROM movies
WHERE year BETWEEN 1970 AND 1979
AND imdb_rating > 8;
```
* We are putting `AND imdb_rating > 8` on another line and indented just so it is easier to read.
### 🟩 Output
```SQL
 id  |    name    | genre  | year | imdb_rating
-----|------------|--------|------|-------------
  6  | Star Wars  | action | 1977 |     8.7     
194  |   Jaws     | drama  | 1975 |     8.1     
```
**(2.)** Remove the previous query.              
Suppose we have a picky friend who only wants to watch old horror films.                   
Using `AND`, write a new query that selects all movies made prior to 1985 that are also in the `horror` genre.
```SQL
SELECT * FROM movies
WHERE year < 1985
AND genre = 'horror';
```
### 🟩 Output
```SQL
  id  |           name            |  genre  | year | imdb_rating
------|----------------------------|---------|------|-------------
100   |         Gremlins          | horror  | 1984 |     7.2     
109   |          Jaws 2           | horror  | 1978 |     5.7     
116   |  The Amityville Horror    | horror  | 1979 |     6.2     
222   |      Dawn of the Dead     | horror  | 1978 |    NULL     
```
# Or
Similar to `AND`, the `OR` operator can also be used to combine multiple conditions in `WHERE`, but there is a fundamental difference:

* `AND` operator displays a row if all the conditions are true.
* `OR` operator displays a row if any condition is true.

 → Suppose we want to check out a new movie or something action-packed:
 ```SQL
SELECT * FROM movies
WHERE year > 2014
OR genre = 'action';
```
* `year > 2014` is the 1st condition.
* `genre = 'action'` is the 2nd condition.
* `OR` combines the two conditions.

 <img width="271" alt="image" src="https://github.com/user-attachments/assets/aa2d0a4d-328e-48e4-94d7-76def3eaa2bc" />

With `OR`, if any of the conditions are true, then the row is added to the result.

### 🟩 Output
```SQL
 id  |                  name                   |   genre   | year | imdb_rating
-----|-----------------------------------------|-----------|------|-------------
  1  |                Avatar                   |  action   | 2009 |     7.9     
  2  |           Jurassic World                |  action   | 2015 |     7.3     
  3  |            The Avengers                 |  action   | 2012 |     8.1     
  4  |          The Dark Knight                |  action   | 2008 |     9.0     
  6  |              Star Wars                  |  action   | 1977 |     8.7     
  7  |      Avengers: Age of Ultron            |  action   | 2015 |     7.9     
  8  |       The Dark Knight Rises             |  action   | 2012 |     8.5     
 10  |             Iron Man 3                  |  action   | 2013 |     7.3     
 11  |              Spider-Man                 |  action   | 2002 |     7.3     
 12  | Transformers: Revenge of the Fallen     |  action   | 2009 |     6.0     
 14  |             Spider-Man 2                |  action   | 2004 |     7.3     
 15  | Transformers: Dark of the Moon          |  action   | 2011 |     6.3     
 16  |           American Sniper               |  action   | 2014 |     7.4     
 17  |            Furious Seven                |  action   | 2015 |     7.4     
 18  |             Spider-Man 3                |  action   | 2007 |     6.2     
 19  |       Guardians of the Galaxy           |  action   | 2014 |     8.1     
 20  |             Transformers                |  action   | 2007 |     7.1     
 21  |              Iron Man                   |  action   | 2008 |     7.9     
 23  |              Iron Man 2                 |  action   | 2010 |     7.1     
 25  | Pirates of the Caribbean: At Worlds End |  action   | 2007 |     7.1     
 27  |           Independence Day              |  action   | 1996 |     6.9     
 29  |                Skyfall                  |  action   | 2012 |     7.8     
 30  |               Inception                 |  action   | 2010 |     8.8     
 31  |             Man of Steel                |  action   | 2013 |     7.2     
 33  |         The Matrix Reloaded             |  action   | 2003 |     7.2     
 34  |      The Amazing Spider-Man             |  action   | 2012 |     7.1     
 35  |           The Incredibles               |  action   | 2004 |     8.0     
 36  | Captain America: The Winter Soldier     |  action   | 2014 |     7.8     
 37  |            The Lego Movie               |  action   | 2014 |     7.8     
 38  |               Star Trek                 |  action   | 2009 |     8.0     
 39  |                Batman                   |  action   | 1989 |     7.6     
 40  |        Night at the Museum              |  action   | 2006 |     6.4     
 41  | Transformers: Age of Extinction         |  action   | 2014 |     5.8     
 42  |                Twister                  |  action   | 1996 |     6.3     
 43  |              Maleficent                 |  action   | 2014 |     7.0     
 45  |          Fast & Furious 6               |  action   | 2013 |     7.2     
 46  |         Beverly Hills Cop               |  action   | 1984 |     7.3     
 47  |       X-Men: The Last Stand             |  action   | 2006 |     6.8     
 48  |    X-Men: Days of Future Past           |  action   | 2014 |     8.1     
 49  | The Lost World: Jurassic Park           |  action   | 1997 |     6.5     
 50  |       Star Trek Into Darkness           |  action   | 2013 |     7.8     
 56  |              Inside Out                 |  comedy   | 2015 |     8.6     
 58  |               Minions                   |  comedy   | 2015 |     6.7     
156  |             Cinderella                  | romance   | 2015 |     7.1     
171  |       Fifty Shades of Grey              | romance   | 2015 |     4.2     
224  |     Star Wars: The Force Awakens        |  action   | 2015 |     8.1     
225  |       Star Wars: The Last Jedi          |  action   | 2017 |    NULL     
228  |         Ali Wong: Baby Cobra            |   NULL    | 2016 |    NULL     
229  |             The Big Sick                | romance   | 2017 |    NULL     
230  |               Deadpool                  |  action   | 2016 |    NULL     
```
**(1)** Suppose we are in the mood for a good laugh or a good cry.                      
Using `OR`, write a query that returns all movies that are either a romance or a comedy.
```SQL
SELECT * FROM movies
WHERE  genre ='romance' OR genre ='comedy';
```
### 🟩 Output
```SQL
 id   |           name            |   genre   | year | imdb_rating
------|----------------------------|-----------|------|--------------
  51  |          Shrek 2           |  comedy   | 2004 |     7.2     
  54  |      Finding Nemo          |  comedy   | 2003 |     8.2     
  59  |            Up              |  comedy   | 2009 |     8.3     
  60  |      Monsters, Inc.        |  comedy   | 2001 |     8.1     
  61  |       Home Alone           |  comedy   | 1990 |     7.4     
  65  |          Shrek             |  comedy   | 2001 |     7.9     
  68  |     Despicable Me          |  comedy   | 2010 |     7.7     
  70  |      Toy Story 2           |  comedy   | 1999 |     7.9     
  71  |           Cars             |  comedy   | 2006 |     7.2     
  78  |       Big Hero 6           |  comedy   | 2014 |     7.9     
 147  |          Titanic           | romance   | 1997 |     7.7     
 153  |  Beauty and the Beast      | romance   | 1991 |     8.0     
 156  |        Cinderella          | romance   | 2015 |     7.1     
 159  |          Twilight          | romance   | 2008 |     5.2     
 164  |      Pretty Woman          | romance   | 1990 |     6.9     
 167  | Something About Mary       | romance   | 1998 |     7.1     
 168  |            Elf             | romance   | 2003 |     6.9     
 170  |       Bridesmaids          | romance   | 2011 |     6.8     
 174  |     Sound of Music         | romance   | 1965 |     8.0     
 188  |   Slumdog Millionaire      | romance   | 2008 |     8.0     
```
# Order By
That’s it with `WHERE` and its operators. Moving on!                              
It is often useful to list the data in our result set in a particular order.

We can sort the results using `ORDER BY`, either alphabetically or numerically. Sorting the results often makes the data more useful and easier to analyze.

For example, if we want to sort everything by the movie’s title from A through Z:
```sql
SELECT * FROM movies
ORDER BY name;
```
* `ORDER BY` is a clause that indicates you want to sort the result set by a particular column.
* `name` is the specified column.

Sometimes we want to sort things in a decreasing order. For example, if we want to select all of the well-received movies, sorted from highest to lowest by their year:
```SQL
SELECT * FROM movies
WHERE imdb_rating > 8
ORDER BY year DESC;
```
* `DESC` is a keyword used in `ORDER BY` to sort the results in descending order (high to low or Z-A).
* `ASC` is a keyword used in `ORDER BY` to sort the results in ascending order (low to high or A-Z).

The column that we `ORDER BY` doesn’t even have to be one of the columns that we’re displaying.

📝 Note: `ORDER BY` always goes after `WHERE` (if `WHERE`is present).

**(1.)** Suppose we want to retrieve the `name` and `year` columns of all the movies, ordered by their name alphabetically.
```SQL
SELECT name, year FROM movies
ORDER BY name;
```
### 🟩 Output
```SQL
| Name                                    | Year |
| --------------------------------------- | ---- |
| 1408                                    | 2007 |
| 3 Men and a Baby                        | 1987 |
| A Beautiful Mind                        | 2001 |
| Air Force One                           | 1997 |
| Aladdin                                 | 1992 |
| Ali Wong: Baby Cobra                    | 2016 |
| Aliens                                  | 1986 |
| Alvin and the Chipmunks: The Squeakquel | 2009 |
| American Sniper                         | 2014 |
| Austin Powers in Goldmember             | 2002 |
| Austin Powers: The Spy Who Shagged Me   | 1999 |
| Avengers: Age of Ultron                 | 2015 |
| Back to the Future                      | 1985 |
| Batman                                  | 1989 |
| Beauty and the Beast                    | 1991 |
| Beverly Hills Cop                       | 1984 |
| Blade                                   | 1998 |
| Brave                                   | 2012 |
| Bridesmaids                             | 2011 |
| Bruce Almighty                          | 2003 |
```
📝 We didn’t add `ASC` here because ascending order is the default.                             
📝 If you run this code, the result will start with ‘1408’, ‘3 Men and a Baby’ and then A-Z.

**(2.)** Your turn! Remove the previous query.                                 
Write a new query that retrieves the `name`, `year`, and `imdb_rating` columns of all the `movies`, ordered highest to lowest by their ratings.
```SQL
SELECT name, year, imdb_rating FROM movies
ORDER BY imdb_rating DESC;
```
* We added `DESC` here because we want to sort it in a descending order.
* If you run this query, the result will start with movies with an `IMDb rating` of `9.0` all the way down to `4.2`.
### 🟩 Output
```SQL
| No. | Name                                           | Year | IMDb Rating |
| --- | ---------------------------------------------- | ---- | ----------- |
| 1   | The Dark Knight                                | 2008 | 9.0         |
| 2   | Inception                                      | 2010 | 8.8         |
| 3   | Star Wars: Episode V - The Empire Strikes Back | 1980 | 8.8         |
| 4   | Forrest Gump                                   | 1994 | 8.8         |
| 5   | Star Wars                                      | 1977 | 8.7         |
| 6   | Interstellar                                   | 2014 | 8.7         |
| 7   | Inside Out                                     | 2015 | 8.6         |
| 8   | Saving Private Ryan                            | 1998 | 8.6         |
| 9   | Se7en                                          | 1995 | 8.6         |
| 10  | The Dark Knight Rises                          | 2012 | 8.5         |
| 11  | Runaway Bride                                  | 1999 | 5.4         |
| 12  | Alvin and the Chipmunks                        | 2007 | 5.3         |
| 13  | Scary Movie 2                                  | 2001 | 5.2         |
| 14  | The Final Destination                          | 2009 | 5.2         |
| 15  | Twilight                                       | 2008 | 5.2         |
| 16  | The Haunting                                   | 1999 | 4.9         |
| 17  | The Twilight Saga: Eclipse                     | 2010 | 4.9         |
| 18  | The Twilight Saga: Breaking Dawn - Part 1      | 2011 | 4.9         |
| 19  | The Twilight Saga: New Moon                    | 2009 | 4.6         |
| 20  | Fifty Shades of Grey                           | 2015 | 4.2         |
```
# Limit
We’ve been working with a fairly small table (fewer than 250 rows), but most SQL tables contain hundreds of thousands of records. In those situations, it becomes important to cap the number of rows in the result.

For instance, imagine that we just want to see a few examples of records.
```SQL
SELECT * FROM movies
LIMIT 10;
```
`LIMIT` is a clause that lets you specify the maximum number of rows the result set will have. This saves space on our screen and makes our queries run faster.

Here, we specify that the result set can’t have more than 10 rows.

`LIMIT` always goes at the very end of the query. Also, it is not supported in all SQL databases.

**(1.)** Combining your knowledge of LIMIT and ORDER BY, write a query that returns the top 3 highest rated movies.   
Select all the columns.
```SQL
SELECT * FROM movies
ORDER BY imdb_rating DESC
LIMIT 3;
```
### 🟩 Output
```SQL
| id | Name                                           | Genre  | Year | IMDb Rating |
| -- | ---------------------------------------------- | ------ | ---- | ----------- |
| 4  | The Dark Knight                                | Action | 2008 | 9.0         |
| 30 | Inception                                      | Action | 2010 | 8.8         |
| 32 | Star Wars: Episode V - The Empire Strikes Back | Action | 1980 | 8.8         |
```
# Case
A `CASE` statement allows us to create different outputs (usually in the `SELECT` statement). It is SQL’s way of handling `if-then` logic.

Suppose we want to condense the ratings in `movies` to three levels:

* If the rating is above 8, then it is Fantastic.
* If the rating is above 6, then it is Poorly Received.
* Else, Avoid at All Costs.
```SQL
SELECT name,
 CASE
  WHEN imdb_rating > 8 THEN 'Fantastic'
  WHEN imdb_rating > 6 THEN 'Poorly Received'
  ELSE 'Avoid at All Costs'
 END
FROM movies;
```
* Each `WHEN` tests a condition and the following `THEN` gives us the string if the condition is true.
* The `ELSE` gives us the string if all the above conditions are false.
* The `CASE` statement must end with `END`.

→ In the result, you have to scroll right because the column name is very long. To shorten it, we can rename the column to ‘Review’ using `AS`:
```SQL
SELECT name,
 CASE
  WHEN imdb_rating > 8 THEN 'Fantastic'
  WHEN imdb_rating > 6 THEN 'Poorly Received'
  ELSE 'Avoid at All Costs'
 END AS 'Review'
FROM movies;
```
**(1)** Let’s try one on your own.                              
Select the `name` column and use a `CASE` statement to create the second column that is:                          
* ‘Chill’ if `genre = 'romance'`
* ‘Chill’ if `genre = 'comedy'`
* ‘Intense’ in all other cases
Optional: Rename the whole `CASE` statement to ‘Mood’ using `AS`.
Give it your best shot! Check hint for the answer.
```SQL
SELECT name,
 CASE
  WHEN genre = 'romance' THEN 'Chill'
  WHEN genre = 'comedy'  THEN 'Chill'
  ELSE 'Intense'
 END AS 'Mood'
FROM movies;
```
### 🟩 Output
```SQL
| Name            | Mood    |
| --------------- | ------- |
| The Dark Knight | Intense |
| Inception       | Intense |
| Interstellar    | Intense |
| Se7en           | Intense |
| The Conjuring   | Intense |
| Finding Nemo    | Chill   |
| Despicable Me   | Chill   |
| The Hangover    | Chill   |
| Aladdin         | Chill   |
| Shrek           | Chill   |
```















































