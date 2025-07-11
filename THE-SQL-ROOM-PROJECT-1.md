# Trends in Startups
Howdy! It’s your first day as a `TechCrunch` reporter. Your first task is to write an article on the rising trends in the startup world.

To get you started with your research, your boss emailed you a `project.sqlite` file that contains a table called `startups`. It is a portfolio of some of the biggest names in the industry.

Write queries with aggregate functions to retrieve some interesting insights about these companies.

**(1.)** Getting started, take a look at the startups table:                                  
How many columns are there?
```sql
SELECT * FROM startups;
```
### 🟩Output
```sql
| Name                  | Location       | Category        | Employees | Raised    | Valuation   | Founded | Stage    | CEO                   | Info                                   |
| --------------------- | -------------- | --------------- | --------- | --------- | ----------- | ------- | -------- | --------------------- | -------------------------------------- |
| Pied Piper            | Silicon Valley | Cloud Computing | 6         | 5000000   | 50000000    | 2014    | A        | Richard Hendricks     | A Middle-Out Compression Solution      |
| Hooli                 | Silicon Valley | Enterprise      | 9000      | 580000000 | 49500000000 | 1997    | null     | Gavin Bensen          | Hooli Is About People                  |
| Raviga Capital        | Silicon Valley | Venture Capital | 12        | 300000000 | 3000000000  | 2012    | null     | Peter Gregory         | Share Only In Success                  |
| Aviato                | Silicon Valley | Travel          | 3         | 250000    | 2500000     | 2006    | Acquired | Erlich Bachman        | Software Aggregation Program           |
| SEE FOOD              | Silicon Valley | Mobile          | 2         | null      | 15000000    | 2016    | Acquired | Jian-Yang             | The Shazam of Food                     |
| Forbid                | New York       | Mobile          | 25        | 1400000   | 5000000     | 2013    | Acquired | Charlie Dattolo       | Charge Users \$10 for Calling Their Ex |
| Soulstice             | New York       | Fitness         | 300       | 30000000  | 120000000   | 2014    | B        | null                  | What are your goals today?             |
| E-Corp                | New York       | Enterprise      | 10000     | null      | 66000000000 | 2006    | null     | Phillip Price         | Together We Can Change the Wolrd       |
| Allsafe Cybersecurity | New York       | Security        | 250       | 123000000 | 1000000000  | 2014    | null     | Gideon Goddard        | null                                   |
| fsociety              | Brooklyn       | Games           | 5         | null      | null        | 2015    | Stealth  | Elliot Alderson       | Fun Society Arcade                     |
|                       |                |                 |           |           |             |         |          |                       |                                        |
| **...**               | **...**        | **...**         | **...**   | **...**   | **...**     | **...** | **...**  | **...**               | **...**                                |
|                       |                |                 |           |           |             |         |          |                       |                                        |
| Aviato                | Silicon Valley | Travel          | 3         | 250000    | 2500000     | 2006    | Acquired | Erlich Bachman        | Software Aggregation Program           |
| SEE FOOD              | Silicon Valley | Mobile          | 2         | null      | 15000000    | 2016    | Acquired | Jian-Yang             | The Shazam of Food                     |
| Forbid                | New York       | Mobile          | 25        | 1400000   | 5000000     | 2013    | Acquired | Charlie Dattolo       | Charge Users \$10 for Calling Their Ex |
| Soulstice             | New York       | Fitness         | 300       | 30000000  | 120000000   | 2014    | B        | null                  | What are your goals today?             |
| E-Corp                | New York       | Enterprise      | 10000     | null      | 66000000000 | 2006    | null     | Phillip Price         | Together We Can Change the Wolrd       |
| Allsafe Cybersecurity | New York       | Security        | 250       | 123000000 | 1000000000  | 2014    | null     | Gideon Goddard        | null                                   |
| fsociety              | Brooklyn       | Games           | 5         | null      | null        | 2015    | Stealth  | Elliot Alderson       | Fun Society Arcade                     |
| Unfade                | New York       | Fashion         | 4         | 400000    | 5600000     | 2016    | A        | Peggy Grimes          | Everything Hair                        |
| OrangeYouLonely       | Minneapolis    | Social          | 20        | 1200000   | 14000000    | 2012    | Seed     | Gus Dawson            | Dating App for Farmers                 |
| WellDeserved          | San Francisco  | E-commerce      | 4         | null      | null        | 2015    | Seed     | Kasima Tharnpipitchai | The Premiere Marketplace for Privilege |
```
**(2.)** Calculate the total number of companies in the table.
```SQL
SELECT COUNT(*) FROM startups;
```
### 🟩Output
```SQL
  count(*) 
+----------+
     70
```
**(3.)** We want to know the total value of all companies in this table.                         
Calculate this by getting the `SUM()` of the `valuation` column.
```sql
SELECT SUM(valuation) FROM startups;
```
### 🟩Output
```SQL
  SUM(valuation) 
-------------------
   974455790000
```
**(4.)** What is the highest amount raised by a startup?                       
Return the maximum amount of money `raised`.
```sql
SELECT MAX(raised) FROM startups;
```
### 🟩Output
```SQL
   MAX(raised) 
-------------------
   11500000000
```
**(5.)** Edit the query so that it returns the maximum amount of money `raised`, during ‘Seed’ stage.
```sql
SELECT MAX(raised) FROM startups
WHERE stage = 'Seed';
```
### 🟩Output
```SQL
   MAX(raised) 
-------------------
    1800000
```
**(6.)** In what year was the oldest company on the list founded?
```sql
SELECT MIN(founded) FROM startups;
```
### 🟩Output
```SQL
   MIN(founded) 
-------------------
      1994
```
# Let's find out the valuations among different sectors:
**(7.)** Return the average `valuation`.
```sql
SELECT AVG(valuation) FROM startups;
```
### 🟩Output
```SQL
  AVG(valuation) 
-------------------
 15974685081.9672
```
**(8.)** Return the average `valuation`, in each `category`.
```sql
SELECT category, AVG(valuation) FROM startups
GROUP BY category;
```
### 🟩Output
```SQL
+---------------------+----------------------+
|      category       |   AVG(valuation)     |
+---------------------+----------------------+
| General             |      4290000.00      |
| Algorithms          |      7600000.00      |
| Augmented Reality   |   8000000000.00      |
| Big Data Analytics  |     15000000.00      |
| Cloud Computing     |     95000000.00      |
| Customer Service    |    640000000.00      |
| Data Analytics      |         null         |
| E-commerce          |     60250000.00      |
| Education           |   2023800000.00      |
| Enterprise          |  38508333333.33      |
| Fashion             |      3200000.00      |
| Fitness             |     67500000.00      |
| Gambling            |    322000000.00      |
| Games               |      1600000.00      |
| Health Care         | 380490000000.00      |
| Logistics           |     70000000.00      |
| Mobile              |      9600000.00      |
| Nanotechnology      |    150000000.00      |
| Real Estate         |  20000000000.00      |
| SaaS                |    401000000.00      |
| Security            |   6333333333.33      |
| Social              |    82425833.33       |
| Technology          |   3100000000.00      |
| Travel              |  12501250000.00      |
| Venture Capital     |   3000000000.00      |
| Video Streaming     |         null         |
| Virtual Reality     |      2150000.00      |
+---------------------+----------------------+
```
**( 9.)** Return the average `valuation`, in each `category`.                                
Round the averages to two decimal places.
```sql
SELECT category, ROUND(AVG(valuation), 2) FROM startups
GROUP BY category;
```
### 🟩Output
```SQL
+---------------------+--------------------------+
|      category       | ROUND(AVG(valuation), 2) |
+---------------------+--------------------------+
| General             |       4290000.00         |
| Algorithms          |       7600000.00         |
| Augmented Reality   |    8000000000.00         |
| Big Data Analytics  |      15000000.00         |
| Cloud Computing     |      95000000.00         |
| Customer Service    |     640000000.00         |
| Data Analytics      |          null            |
| E-commerce          |      60250000.00         |
| Education           |    2023800000.00         |
| Enterprise          |   38508333333.33         |
| Fashion             |       3200000.00         |
| Fitness             |      67500000.00         |
| Gambling            |     322000000.00         |
| Games               |       1600000.00         |
| Health Care         |  380490000000.00         |
| Logistics           |      70000000.00         |
| Mobile              |       9600000.00         |
| Nanotechnology      |     150000000.00         |
| Real Estate         |   20000000000.00         |
| SaaS                |     401000000.00         |
| Security            |    6333333333.33         |
| Social              |      82425833.33         |
| Technology          |    3100000000.00         |
| Travel              |   12501250000.00         |
| Venture Capital     |    3000000000.00         |
| Video Streaming     |          null            |
| Virtual Reality     |       2150000.00         |
+---------------------+--------------------------+
```
**(10.)** Return the average `valuation`, in each `category`.                      
Round the averages to two decimal places.                                 
Lastly, order the list from highest averages to lowest.
```SQL
SELECT category, ROUND(AVG(valuation), 2)
FROM startups
GROUP BY 1
ORDER BY 2 DESC;
```
### 🟩Output
```SQL
category              ROUND(AVG(valuation), 2)
General               4290000.00
Algorithms            7600000.00
Augmented Reality     8000000000.00
Big Data Analytics    15000000.00
Cloud Computing       95000000.00
Customer Service      640000000.00
Data Analytics        null
E-commerce            60250000.00
Education             2023800000.00
Enterprise            38508333333.33
Fashion               3200000.00
Fitness               67500000.00
Gambling              322000000.00
Games                 1600000.00
Health Care           380490000000.00
Logistics             70000000.00
Mobile                9600000.00
Nanotechnology        150000000.00
Real Estate           20000000000.00
SaaS                  401000000.00
Security              6333333333.33
Social                82425833.33
Technology            3100000000.00
Travel                12501250000.00
Venture Capital       3000000000.00
Video Streaming       null
Virtual Reality       2150000.00
```
**(11.)** First, return the name of each `category` with the total number of companies that belong to it.
```sql
SELECT category, COUNT(*)
FROM startups
GROUP BY category;
```
### 🟩Output
```SQL
category              COUNT(*)
General               3
Algorithms            1
Augmented Reality     1
Big Data Analytics    1
Cloud Computing       2
Customer Service      1
Data Analytics        1
E-commerce            3
Education             5
Enterprise            3
Fashion               2
Fitness               3
Gambling              1
Games                 2
Health Care           2
Logistics             1
Mobile                10
Nanotechnology        1
Real Estate           1
SaaS                  2
Security              3
Social                12
Technology            3
Travel                2
Venture Capital       1
Video Streaming       1
Virtual Reality       2
```
**(12.)** Next, filter the result to only include categories that have more than three companies in them.      
What are the most competitive markets?
```sql
SELECT category, COUNT(*)
FROM startups
GROUP BY category
HAVING COUNT(*) > 3
ORDER BY 2 DESC;
```
### 🟩Output
```SQL
+-----------+-----------+
| category  | COUNT(*)  |
+-----------+-----------+
| Social    |    12     |
| Mobile    |    10     |
| Education |     5     |
+-----------+-----------+
```
📝 you are filtering on a condition that has an aggregate function, you need to use `HAVING` instead of `WHERE`.        
📝 If you want to go a step further, sort the result using `ORDER BY`.

# Let's see if there's a difference in startups sizes among different locations:
 
**(13.)** What is the average size of a startup in each `location`?
```SQL
SELECT location, AVG(employees)
FROM startups
GROUP BY location;
```
### 🟩Output
```SQL
+--------------------+------------------+
|     location       | AVG(employees)   |
+--------------------+------------------+
| Atlanta            |     3.00         |
| Boulder            |     3.00         |
| Brooklyn           |   502.67         |
| Chicago            |    12.00         |
| Columbus           |     2.00         |
| Denver             |    12.00         |
| Fort Lauderdale    |   500.00         |
| Irvine             |     2.00         |
| Long Island        |     5.00         |
| Los Angeles        |     6.83         |
| Minneapolis        |    20.00         |
| New Delhi          |   250.00         |
| New York           |   702.75         |
| Omaha              |    65.00         |
| Palo Alto          |   125.83         |
| Paris              |    30.00         |
| San Francisco      |  1920.40         |
| Savannah           |     6.00         |
| Scranton           |     6.00         |
| Seattle            |     9.67         |
| Silicon Valley     |  1804.60         |
| Virginia Beach     |    15.00         |
| Washington DC      |     8.00         |
+--------------------+------------------+
```
**(14.)** What is the average size of a startup in each `location`, with average sizes above 500?
```sql
SELECT location, AVG(employees)
FROM startups
GROUP BY location
HAVING AVG(employees) > 500;
```
### 🟩Output
```SQL
+------------------+------------------+
|     location     | AVG(employees)   |
+------------------+------------------+
|     Brooklyn     |     502.67       |
|    New York      |     702.75       |
| San Francisco    |    1920.40       |
| Silicon Valley   |    1804.60       |
+------------------+------------------+
```
