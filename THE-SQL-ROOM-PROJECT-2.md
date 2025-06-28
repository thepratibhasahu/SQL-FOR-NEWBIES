# Analyze Hacker News Trends

<img width="270" alt="image" src="https://github.com/user-attachments/assets/528e7a62-602e-4c56-8aed-6220b1553c0c" />

**Hacker News** is a popular website run by Y Combinator. It’s widely known by people in the tech industry as a community site for sharing news, showing off projects, asking questions, among other things.

In this project, you will be working with a table named `hacker_news` that contains stories from Hacker News since its launch in 2007. It has the following columns:

* `title`: the title of the story
* `user`: the user who submitted the story
* `score`: the score of the story
* `timestamp`: the time of the story
* `url`: the link of the story

→ Let’s get started!

**(1.)** Start by getting a feel for the `hacker_news` table!                           
Let’s find the most popular Hacker News stories:                           
* What are the top five stories with the highest `scores`?
```sql
SELECT title, score
FROM hacker_news
ORDER BY score DESC
LIMIT 5;
```
### 🟩Output 
```sql
| title                                                                        | score |
| ---------------------------------------------------------------------------- | ----- |
| Penny Arcade – Surface Pro 3 update                                          | 517   |
| Hacking The Status Game                                                      | 309   |
| Postgres CLI with autocompletion and syntax highlighting                     | 304   |
| Stephen Fry hits out at ‘infantile’ culture of trigger words and safe spaces | 282   |
| Reversal: Australian Govt picks ODF doc standard over Microsoft              | 191   |
```
📝 Using `LIMIT` caps the number of rows in the result.                
📝 It is a simple way to keep queries from taking too long to run if you are dealing with a big dataset.           
📝 `ORDER BY` simply sorts the `score` column.

# Hacker News Moderating

**(2.)** Recent studies have found that online forums tend to be dominated by a small percentage of their users `(1-9-90 Rule)`.                                
* Is this true of Hacker News?                          
* Is a small percentage of Hacker News submitters taking the majority of the points?                   
* First, find the total `score` of all the stories.
```SQL
SELECT SUM(score)
FROM hacker_news;
```
### 🟩Output 
```sql
+------------+
| SUM(score) |
+------------+
|    6366    |
+------------+
```
**(3.)** Next, we need to pinpoint the users who have accumulated a lot of points across their stories.         
* Find the individual users who have gotten combined `scores` of more than 200, and their combined `scores`.           
* `GROUP BY` and `HAVING` are needed!
```SQL
SELECT user, SUM(score)
FROM hacker_news
GROUP BY user
HAVING SUM(score) > 200
ORDER BY 2 DESC;
```
### 🟩Output 
```SQL
+------------+------------+
|   user     | SUM(score) |
+------------+------------+
|  vxNsr     |    517     |
|  amirkhella|    309     |
|  dmmalam   |    304     |
|  metafunctor|   282     |
+------------+------------+
```
📝 `HAVING` does not support aliases in the same way that `ORDER BY` does, so use the full column name.

**(4.)** Then, we want to add these users’ `scores` together and divide by the total to get the percentage.               
* Add their scores together and divide it by the total sum. Like so:
```SQL
SELECT (1.0 + 2.0 + 3.0) / 6.0;
```
* So, is Hacker News dominated by these users?
```SQL
SELECT (517 + 309 + 304 + 282) / 6366.0;
```
### 🟩Output 
```SQL
+----------------------------------+
| (517 + 309 + 304 + 282) / 6366.0 |
+----------------------------------+
|          0.221803                |
+----------------------------------+
```
* That is ≈ 22%.
* These 4 users have a combined 22% of the total scores in the table. Jeez!

**(5.)** Oh no! While we are looking at the power users, some users are **rickrolling** — tricking readers into clicking on a link to a funny **video** and claiming that it links to information about coding.                 
* The `url` of the video is:
* `https://www.youtube.com/watch?v=dQw4w9WgXcQ`
* How many times has each offending user posted this link?
```SQL
SELECT user,
   COUNT(*)
FROM hacker_news
WHERE url LIKE '%watch?v=dQw4w9WgXcQ%'
GROUP BY user
ORDER BY COUNT(*) DESC;
```
### 🟩Output 
```SQL
+---------------+-----------+
|     user      | COUNT(*)  |
+---------------+-----------+
| sonnynomnom   |     2     |
| scorpiosister |     1     |
+---------------+-----------+
```
**( 6.)** Hacker News stories are essentially links that take users to other websites.                  
* Which of these sites feed Hacker News the most:
* **GitHub**, **Medium**, or **New York** Times?
* First, we want to categorize each story based on their source.
* We can do this using a `CASE` statement:
```SQL
SELECT CASE
   WHEN url LIKE '%github.com%' THEN 'GitHub'
   -- WHEN statement here
   -- WHEN statement here
   -- ELSE statement here
  END AS 'Source'
FROM hacker_news;
```
* Fill in the other `WHEN` statements and the `ELSE` statement.
```sql
SELECT CASE
   WHEN url LIKE '%github.com%' THEN 'GitHub'
   WHEN url LIKE '%medium.com%' THEN 'Medium'
   WHEN url LIKE '%nytimes.com%' THEN 'New York Times'
   ELSE 'Other'
  END AS 'Source'
FROM hacker_news;
```
### 🟩Output 
```SQL
Source
------------
Other
Other
GitHub
Other
New York Times
Other
Medium
Other
```
📝 Note: If we want to be more accurate, we should use `url LIKE '%github%'` because some GitHub pages end with .io instead of .com.

**(7.)** Next, build on the previous query:                         
* Add a column for the number of stories from each URL using `COUNT()`.
* Also, `GROUP BY` the `CASE` statement.
* Remember that you can refer to a column in `GROUP BY` using a number.
```SQL
-- Which sites feed Hacker News?

SELECT CASE
   WHEN url LIKE '%github.com%' THEN 'GitHub'
   WHEN url LIKE '%medium.com%' THEN 'Medium'
   WHEN url LIKE '%nytimes.com%' THEN 'New York Times'
   ELSE 'Other'
  END AS 'Source',
  COUNT(*)
FROM hacker_news
GROUP BY 1;
```
### 🟩Output 
```SQL
Source	        COUNT(*)
GitHub	        23
Medium	        12
New York Times	13
Other	        3952
```
# What's the best time to post a story?

**(8.)** Every submitter wants their story to get a high score so that the story makes it to the front page, but…      
* What’s the best time of the day to post a story on Hacker News?
* Before we get started, let’s run this query and take a look at the `timestamp` column:
```SQL
SELECT timestamp
FROM hacker_news
LIMIT 10;
```
### 🟩Output 
```SQL
timestamp
2014-01-27T17:31:13Z
2011-10-23T18:46:40Z
2016-02-28T06:26:56Z
2014-08-12T22:13:10Z
2013-03-06T12:28:02Z
2011-04-16T21:04:23Z
2014-03-18T21:44:46Z
2012-11-19T11:54:38Z
2016-11-04T13:55:30Z
2016-07-02T22:54:47Z
```
* Notice that the values are formatted like:
`2018-05-08T12:30:00Z`

* If you ignore the T and Z, the format is:
 `YYYY-MM-DD HH:MM:SS`

📝 The `T` is just the separator between the date and time. You can read it as an abbreviation for ‘Time’.         
📝 The `Z` stands for the Zero timezone, as it is offset by 0 from the Coordinated Universal Time (UTC).          
📝 If you don’t look at the `T` and `Z`, it is easier to see the pattern in the `timestamp` column.

  **(9.)**  SQLite comes with a `strftime()` function - a very powerful function that allows you to return a formatted date.
  It takes two arguments:                                                                             
  `strftime(format, column)`                                                                 
  Let’s test this function out:
  ```SQL
SELECT timestamp,
   strftime('%H', timestamp)
FROM hacker_news
GROUP BY 1
LIMIT 20;
```
### 🟩Output 
```SQL
timestamp	          strftime('%H', timestamp)
2007-03-16T20:52:19Z	    20
2007-04-03T03:04:09Z	    03
2007-05-01T03:11:17Z	    03
2007-05-05T05:43:58Z	    05
2007-05-11T05:48:53Z	    05
2007-05-25T22:07:18Z	    22
2007-06-08T08:44:50Z	    08
2007-07-01T00:06:57Z	    00
2007-07-27T16:47:00Z	    16
2007-08-08T00:45:36Z	    00
2007-08-12T07:35:25Z	    07
2007-08-16T01:02:49Z	    01
2007-08-24T18:17:32Z	    18
2007-08-27T17:32:10Z	    17
2007-09-11T16:27:49Z	    16
2007-09-20T20:31:21Z	    20
2007-09-22T08:21:17Z	    08
2007-09-26T05:03:17Z	    05
2007-10-08T21:28:06Z	    21
```
What do you think this does? Open the hint if you’d like to learn more.

📝 This returns the hour, `HH`, of the `timestamp` column!

For `strftime(__, timestamp)`:

* `%Y` returns the year (YYYY)
* `%m` returns the month (01-12)
* `%d` returns the day of the month (1-31)
* `%H` returns 24-hour clock (00-23)
* `%M` returns the minute (00-59)
* `%S` returns the seconds (00-59)
* if `timestamp` format is `YYYY-MM-DD HH:MM:SS`.

**(10.)** Okay, now we understand how `strftime()` works. Let’s write a query that returns three columns:             
* The hours of the `timestamp`
* The average `score` for each hour
* The count of stories for each hour
```sql
SELECT strftime('%H', timestamp), 
   AVG(score),
   COUNT(*)
FROM hacker_news
GROUP BY 1
ORDER BY 2 DESC;
```
### 🟩Output
```SQL
strftime('%H', timestamp)	        AVG(score)	                  COUNT(*)
18	                             27.0277777777778	                    266
07	                             21.3333333333333	                    104
19	                             20.4137931034483	                    238
20	                             18.2758620689655	                    239
12	                             14.3103448275862	                    123
09	                                 11.125	                            119
16                                   9.75555555555556	                    237
15	                             9.49122807017544	                    268
17	                             8.86046511627907	                    215
23	                             8.43478260869565	                    170
11	                             8.32258064516129	                    113
06	                                   7.5	                            110
03	                             6.91304347826087	                    134
13	                             5.67647058823529	                    164
00	                             5.09090909090909	                    137
01	                             4.40740740740741	                    146
04	                                  3.875	                            116
05	                             3.55172413793103	                    125
14	                             3.51515151515152	                    213
21	                                   3.25	                            234
22	                             3.20833333333333	                    185
10	                             3.07894736842105	                    112
02	                                   2.45	                            136
08	                             2.04166666666667	                     90
NULL                                      NULL                                6
```
**(11.)** Let’s edit a few things in the previous query:                                    
Round the average `scores` `(ROUND())`.                                                 
Rename the columns to make it more readable `(AS)`.                             
Add a `WHERE` clause to filter out the `NULL` values in `timestamp`.                                       
Take a look at the result again:                                                   
What are the best hours to post a story on Hacker News?
```SQL
SELECT strftime('%H', timestamp) AS 'Hour', 
   ROUND(AVG(score), 1) AS 'Average Score', 
   COUNT(*) AS 'Number of Stories'
FROM hacker_news
WHERE timestamp IS NOT NULL
GROUP BY 1
ORDER BY 2 DESC;
```
### 🟩Output
```SQL
| Hour | Average Score | Number of Stories |
| ---- | ------------- | ----------------- |
| 00   | 5.1           | 137               |
| 01   | 4.4           | 146               |
| 02   | 2.5           | 136               |
| 03   | 6.9           | 134               |
| 04   | 3.9           | 116               |
| 05   | 3.6           | 125               |
| 06   | 7.5           | 110               |
| 07   | 21.3          | 104               |
| 08   | 2.0           | 90                |
| 09   | 11.1          | 119               |
| 10   | 3.1           | 112               |
| 11   | 8.3           | 113               |
| 12   | 14.3          | 123               |
| 13   | 5.7           | 164               |
| 14   | 3.5           | 213               |
| 15   | 9.5           | 268               |
| 16   | 9.8           | 237               |
| 17   | 8.9           | 215               |
| 18   | 27.0          | 266               |
| 19   | 20.4          | 238               |
| 20   | 18.3          | 239               |
| 21   | 3.3           | 234               |
| 22   | 3.2           | 185               |
| 23   | 8.4           | 170               |
```






