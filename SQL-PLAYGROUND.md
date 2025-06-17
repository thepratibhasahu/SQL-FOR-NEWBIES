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








