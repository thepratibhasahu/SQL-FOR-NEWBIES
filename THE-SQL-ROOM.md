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
```sql
**(1.)** What is the least number of times an app has been downloaded?
In the code editor, type:



