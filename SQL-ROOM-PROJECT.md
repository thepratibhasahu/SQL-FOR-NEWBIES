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

