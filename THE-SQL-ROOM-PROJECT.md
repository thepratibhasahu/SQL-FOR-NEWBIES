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

