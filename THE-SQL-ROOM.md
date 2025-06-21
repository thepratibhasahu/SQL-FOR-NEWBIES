# Introduction
SQL Queries don’t just access raw data, they can also perform calculations on the raw data to answer specific data questions.

Calculations performed on multiple rows of a table are called **aggregates**.

In this lesson, we have given you a table named `fake_apps` which is made up of fake mobile applications data.

Here is a quick preview of some important aggregates:-                                      
* `COUNT()`: count the number of rows.
* `SUM()`: the sum of the values in a column.
* `MAX()`/`MIN()`: the largest/smallest value.
* `AVG()`: the average of the values in a column.
* `ROUND()`: round the values in the column.

→ Let’s get started!

**(1.)** Before getting started, take a look at the data in the fake_apps table.                    
In the code editor, type the following:                             
* What are the column names?
```SQL
SELECT * FROM fake_apps;
```
### 🟩Output
```SQL
| id   | name           | category           | downloads | price |
|------|----------------|--------------------|-----------|-------|
| 3    | siliconphase   | Productivity        | 17193     | 0.0   |
| 6    | Donzolab       | Education           | 4259      | 0.99  |
| 10   | Ittechi        | Reference           | 3874      | 0.0   |
| 13   | Subdrill       | Education           | 7132      | 1.99  |
| 14   | Anzoom         | Health & Fitness    | 6941      | 14.99 |
| 21   | kanity         | Health & Fitness    | 2299      | 0.0   |
| 25   | Zathcare       | Books               | 16281     | 2.99  |
| 30   | Basecode       | Sports              | 21203     | 3.99  |
| 45   | Hayholding     | Medical             | 15845     | 14.99 |
| 59   | Sailflex       | Productivity        | 21984     | 0.99  |
| ...  | ...            | ...                 | ...       | ...   |
| 945  | Freezoom       | Books               | 13207     | 1.99  |
| 946  | Biotex         | Sports              | 14313     | 0.99  |
| 947  | Singlelam      | Finance             | 18117     | 1.99  |
| 949  | Stripplex      | Lifestyle           | 7699      | 3.99  |
| 959  | Lathouse       | Travel              | 31090     | 0.0   |
| 964  | Quoace         | Books               | 22122     | 0.0   |
| 972  | Villatouch     | Weather             | 17085     | 1.99  |
| 973  | Roundhow       | Photo & Video       | 10662     | 0.0   |
| 975  | Groovelab      | Catalogs            | 9496      | 0.0   |
| 977  | Plexlane       | Utilities           | 18050     | 0.0   |
| 982  | Zotice         | Catalogs            | 20062     | 1.99  |
| 985  | tonkix         | Games               | 19498     | 0.0   |
| 992  | Acecane        | Entertainment       | 13359     | 0.0   |
| 1000 | Plusvolzim     | News                | 11448     | 0.0   |
```
# Count
The fastest way to calculate how many rows are in a table is to use the `COUNT()` function.

`COUNT()`is a function that takes the name of a column as an argument and counts the number of non-empty values in that column.
```sql
SELECT COUNT(*) FROM table_name;
```
Here, we want to count every row, so we pass `*` as an argument inside the parenthesis.

**(1.)** Let’s count how many apps are in the table.                                             
In the code editor, run:
```SQL
SELECT COUNT(*) FROM fake_apps;
```
### 🟩Output
```SQL
   COUNT(*)
-------------
    200
```
**(2.)** Add a `WHERE` clause in the previous query to count how many free apps are in the table.
```sql
SELECT COUNT(*) FROM fake_apps
WHERE price = 0;
```
### 🟩Output
```SQL
   COUNT(*)
-------------
    73
```
# Sum
SQL makes it easy to add all values in a particular column using `SUM()`.

`SUM()` is a function that takes the name of a column as an argument and returns the sum of all the values in that column.

What is the total number of `downloads` for all of the apps combined?
```sql
SELECT SUM(downloads) FROM fake_apps;
```
* This adds all values in the downloads column.
### 🟩Output
```SQL
   SUM(downloads)
-------------------
     3322760
```
# Max / Min
The `MAX()` and `MIN()` functions return the highest and lowest values in a column, respectively.

How many downloads does the most popular app have?
```sql
SELECT MAX(downloads) FROM fake_apps;
```
### 🟩Output
```SQL
  MAX(downloads)
-------------------
     31090
```
The most popular app has 31,090 downloads!

`MAX()` takes the name of a column as an argument and returns the largest value in that column. Here, we returned the largest value in the `downloads` column.

`MIN()` works the same way but it does the exact opposite; it returns the smallest value.

**(1.)** What is the least number of times an app has been downloaded?
In the code editor, type:
```sql
SELECT MIN(downloads) FROM fake_apps;
```
### 🟩Output
```SQL
  MIN(downloads)
-------------------
     1387
```
**(2.)** Delete the previous query.                           
Write a new query that returns the price of the most expensive app.
```SQL
SELECT MAX(price) FROM fake_apps;
```
### 🟩Output
```SQL
   MIN(price)
-------------------
     14.99
```
# Average
SQL uses the `AVG()` function to quickly calculate the average value of a particular column.

The `AVG()` function works by taking a column name as an argument and returns the average value for that column.

**(1.)** Calculate the average number of downloads for all the apps in the table.                             
In the code editor, type:
```sql
SELECT AVG(downloads) FROM fake_apps;
```
### 🟩Output
```SQL
  AVG (downloads)
--------------------
     16613.8
```
**(2.)** Remove the previous query.                         
Write a new query that calculates the average price for all the apps in the table.
```sql
SELECT AVG (price) FROM fake_apps;
```
### 🟩Output
```SQL
  AVG (price)
--------------------
     2.02365
```
# Round
By default, SQL tries to be as precise as possible without rounding. We can make the result table easier to read using the `ROUND()` function.

`ROUND()` function takes two arguments inside the parenthesis:
* a column name                               
* an integer

It rounds the values in the column to the number of decimal places specified by the integer.
```sql
SELECT ROUND(price, 0) FROM fake_apps;
```
### 🟩Output
```sql
ROUND(price, 0)
0.0  
1.0  
0.0  
2.0  
15.0  
0.0  
3.0  
4.0  
15.0  
1.0  
```
Here, we pass the column `price` and integer `0` as arguments. SQL rounds the values in the column to 0 decimal places in the output.

**(1.)** Let’s return the `name` column and a rounded `price` column.                               
In the code editor, type:
```sql
SELECT name, ROUND(price, 0) FROM fake_apps;
```
### 🟩Output
```sql
| name          	        | ROUND(price, 0) |
|------------------------|-----------------|
| siliconphase           | 0.0             |
| Donzolab             	| 1.0             |
| Ittechi              	| 0.0             |
| Subdrill             	| 2.0             |
| Anzoom               	| 15.0            |
| kanity               	| 0.0             |
| Zathcare             	| 3.0             |
| Basecode             	| 4.0             |
| Hayholding           	| 15.0            |
| Sailflex             	| 1.0             |
| waretam              	| 3.0             |
| Donelectrics         	| 2.0             |
| sonelectrics         	| 2.0             |
| Zoodom               	| 15.0            |
| Quohouse             	| 0.0             |
| Quotetech            	| 0.0             |
| Funtexon             	| 1.0             |
| Ozerphase            	| 0.0             |
| Kintonflex           	| 0.0             |
| Tamptom              	| 3.0             |
```
**(2.)** Remove the previous query.                                           
In the last exercise, we were able to get the average price of an app ($2.02365) using this query:
```sql
SELECT AVG(price) FROM fake_apps;
```
Now, let’s edit this query so that it rounds this result to 2 decimal places.
```sql
SELECT ROUND(AVG(price), 2) FROM fake_apps;
```
### 🟩Output
```sql
         ROUND(AVG(price), 2)         
                  2.02                
```
📝 You can treat `AVG(price)` just like any other value and place it inside the `ROUND` function like so.                 
📝 Here, `AVG(price)` is the 1st argument and `2` is the 2nd argument because we want to round it to two decimal places:

# Group By I
Oftentimes, we will want to calculate an aggregate for data with certain characteristics.

For instance, we might want to know the mean IMDb ratings for all movies each year. We could calculate each number by a  series of queries with different `WHERE` statements, like so:
```sql
SELECT AVG(imdb_rating)
FROM movies
WHERE year = 1999;

SELECT AVG(imdb_rating)
FROM movies
WHERE year = 2000;

SELECT AVG(imdb_rating)
FROM movies
WHERE year = 2001;
```
and so on.

Luckily, there’s a better way!                             
We can use `GROUP BY` to do this in a single step:
```sql
SELECT year, AVG(imdb_rating) FROM movies
GROUP BY year
ORDER BY year;
```
`GROUP BY` is a clause in SQL that is used with `aggregate functions`. It is used in collaboration with the `SELECT` statement to arrange identical data into groups.

The `GROUP BY` statement comes after any `WHERE` statements, but before `ORDER BY` or `LIMIT`.

**(1.)** In the code editor, type:                  
Here, our aggregate function is `COUNT()` and we arranged `price` into groups.                     
What do you expect the result to be?
```sql
SELECT price, COUNT(*) FROM fake_apps
GROUP BY price;
```
### 🟩Output
```sql
     price     |   COUNT(*)  
---------------|-------------
     0.0       |     73      
     0.99      |     43      
     1.99      |     42      
     2.99      |     21      
     3.99      |     9       
    14.99      |     12      
```
📝 The result contains the total number of apps for each price.                     
📝 It is organized into two columns, making it very easy to see the number of apps at each price.

**(2.)**  In the previous query, add a `WHERE` clause to count the total number of apps that have been downloaded more than 20,000 times, at each price.
```sql
SELECT price, COUNT(*) 
FROM fake_apps
WHERE downloads > 20000
GROUP BY price;
```
### 🟩Output
```sql
   price   | COUNT(*)
-----------|----------
   0.0     |   26     
   0.99    |   17     
   1.99    |   18     
   2.99    |   7      
   3.99    |   5      
  14.99    |   5      
```
**(3.)** Remove the previous query.                             
Write a new query that calculates the total number of downloads for each category.                       
Select category and SUM(downloads).
```sql
SELECT category, SUM(downloads)
FROM fake_apps
GROUP BY category;
```
### 🟩Output
```sql
      category       | SUM(downloads)
---------------------|---------------
      Books          |   160864      
     Business        |   178726      
     Catalogs        |   186158      
     Education       |   184724      
   Entertainment     |    95168      
      Finance        |   178163      
   Food & Drink      |    90950      
       Games         |   256083      
Health & Fitness     |   165555      
     Lifestyle       |   166832      
      Medical        |    77191      
       Music         |    59367      
    Navigation       |   152114      
        News         |   103259      
  Photo & Video      |   184848      
   Productivity      |   117811      
     Reference       |   162032      
Social Networking    |   126549      
       Sports        |   176988      
       Travel        |   242116      
     Utilities       |    96099      
      Weather        |   161163      
```
# Group By II
Sometimes, we want to  in each group `GROUP BY` a calculation done on a column.

For instance, we might want to know how many movies have IMDb ratings that round to 1, 2, 3, 4, 5. We could do this using the following syntax:
```SQL
SELECT ROUND(imdb_rating),
   COUNT(name)
FROM movies
GROUP BY ROUND(imdb_rating)
ORDER BY ROUND(imdb_rating);
```
However, this query may be time-consuming to write and more prone to error.

SQL lets us use column reference(s) in our `GROUP BY` that will make our lives easier.

* `1` is the first column selected
* `2` is the second column selected
* `3` is the third column selected
and so on.

The following query is equivalent to the one above:
```sql
SELECT ROUND(imdb_rating),
   COUNT(name)
FROM movies
GROUP BY 1
ORDER BY 1;
```
Here, the `1` refers to the first column in our `SELECT` statement, `ROUND(imdb_rating)`.

**(1.)** Suppose we have the query below:
```sql
SELECT category, 
   price,
   AVG(downloads)
FROM fake_apps
GROUP BY category, price;
```
Write the exact query, but use column reference numbers instead of column names after `GROUP BY`.
```sql
SELECT category, 
   price,
   AVG(downloads)
FROM fake_apps
GROUP BY 1, 2;
```
### 🟩Output
```sql
       category        | price |     AVG(downloads)
------------------------|-------|-------------------------
        Books           |  0.0  |       11926.5
        Books           |  0.99 |       27709.5
        Books           |  1.99 |       21770.33
        Books           |  2.99 |       16281.0
      Business          |  0.0  |       14744.25
      Business          |  0.99 |       15753.0
      Business          |  1.99 |       18155.5
      Business          |  2.99 |       19598.5
      Business          | 14.99 |       28488.0
      Catalogs          |  0.0  |       19393.0
      Catalogs          |  0.99 |        4937.0
      Catalogs          |  1.99 |       20062.0
      Catalogs          |  2.99 |       27862.33
      Education         |  0.0  |       28911.0
      Education         |  0.99 |        8619.8
      Education         |  1.99 |       14815.67
      Education         |  2.99 |       10843.5
      Education         | 14.99 |       17669.0
   Entertainment        |  0.0  |       14577.0
   Entertainment        |  0.99 |       14814.5
```
📝 Note: Even if you use column names instead of numbers, it will still be correct because these two queries are exactly the same!
# Having
In addition to being able to group data using `GROUP BY`, SQL also allows you to filter which groups to include and which to exclude.

For instance, imagine that we want to see how many movies of different genres were produced each year, but we only care about years and genres with at least 10 movies.

We can’t use `WHERE` here because we don’t want to filter the rows; we want to filter groups.

This is where `HAVING` comes in.

`HAVING` is very similar to `WHERE`. In fact, all types of `WHERE` clauses you learned about thus far can be used with `HAVING`.

We can use the following for the problem:
```sql
SELECT year,
   genre,
   COUNT(name)
FROM movies
GROUP BY 1, 2
HAVING COUNT(name) > 10;
```
* When we want to limit the results of a query based on values of the individual rows, use `WHERE`.
* When we want to limit the results of a query based on an aggregate property, use `HAVING`.

`HAVING` statement always comes after `GROUP BY`, but before `ORDER BY` and `LIMIT`.

**(1.)** Suppose we have the query below:
```sql
SELECT price, 
   ROUND(AVG(downloads)),
   COUNT(*)
FROM fake_apps
GROUP BY price;
```
It returns the average downloads (rounded) and the number of apps – at each price point.

However, certain price points don’t have very many apps, so their average downloads are less meaningful.

Add a `HAVING` clause to restrict the query to price points that have more than 10 apps.`
```sql
SELECT price, 
   ROUND(AVG(downloads)),
   COUNT(*)
FROM fake_apps
GROUP BY price
HAVING COUNT(*) > 10;
```
### 🟩Output
```sql
 price  |  ROUND(AVG(downloads))  |  COUNT(*)
--------|--------------------------|-----------
  0.0   |        15762.0           |     73
  0.99  |        15972.0           |     43
  1.99  |        16953.0           |     42
  2.99  |        17725.0           |     21
 14.99  |        19369.0           |     12
```


















































