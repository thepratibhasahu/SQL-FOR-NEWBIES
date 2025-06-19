# PROJECT_1
**New York Restaurants**                         
We have put together a table of restaurants called `nomnom` and we need your help to answer some questions. Use the SQL commands you just learned and find the best dinner spots in the city.

**(1.)** Start by getting a feel for the `nomnom` table:                           
* What are the column names?
```SQL
SELECT * FROM nomnom;
```
### 🟩 Output
```SQL
name                           | neighborhood | cuisine     | review | price | health
------------------------------|--------------|-------------|--------|-------|--------
Peter Luger Steak House       | Brooklyn     | Steak       | 4.4    | $$$$  | A
Jongro BBQ                    | Midtown      | Korean      | 4.5    | $$    | A
Pocha 32                      | Midtown      | Korean      | 4.0    | $$    | A
Nom Wah Tea Parlor            | Chinatown    | Chinese     | 4.2    | $     | A
Roberta's                     | Brooklyn     | Pizza       | 4.4    | $$    | A
Speedy Romeo                  | Brooklyn     | Pizza       | 4.4    | $$    | A
Bunna Cafe                    | Brooklyn     | Ethiopian   | 4.6    | $$    | A
Massawa                       | Uptown       | Ethiopian   | 4.0    | $$    | null
Buddha Bodai                  | Chinatown    | Vegetarian  | 4.2    | $$    | A
Nan Xiang Xiao Long Bao      | Queens       | Chinese     | 4.2    | $     | A
Mission Chinese Food         | Downtown     | Chinese     | 3.9    | $$    | A
Baohaus                       | Downtown     | Chinese     | 4.2    | $     | A
al di la Trattoria           | Brooklyn     | Italian     | 4.4    | $$$   | A
Locanda Vini & Olii          | Brooklyn     | Italian     | 4.4    | $$$   | A
Rao's                         | Uptown       | Italian     | 4.2    | $$$   | A
Minca                         | Downtown     | Japanese    | 4.4    | $$    | A
Kenka                         | Downtown     | Japanese    | 4.3    | $     | B
Yakitori Taisho              | Downtown     | Japanese    | 4.1    | $     | B
Xi'an Famous Foods           | Midtown      | Chinese     | 4.4    | $     | A
Shake Shack                  | Midtown      | American    | 4.4    | $     | A
The Halal Guys               | Midtown      | Mediterranean| 4.4   | $     | A
Foodcademy                   | Midtown      | American    | 4.4    | $$    | A
Sonnyboy's                   | Brooklyn     | Chinese     | 4.2    | $$    | A
The Cole Romano Experience   | Brooklyn     | Italian     | 2.1    | $$$$$ | C
Timbo Slice                  | Brooklyn     | Pizza       | 2.8    | $     | B
Scorpio Sisters              | Downtown     | American    | 4.2    | $$    | A
N.E.D                         | Uptown       | American    | 4.2    | $$$   | A
Great NY Noodletown          | Chinatown    | Chinese     | 4.1    | $$    | B
Golden Unicorn               | Chinatown    | Chinese     | 3.8    | $$    | A
Wo Hop                        | Chinatown    | Chinese     | 4.2    | $$    | null
Di Fara Pizza                | Brooklyn     | Pizza       | 4.2    | $$    | A
Kang Ho Dong Baekjeong       | Midtown      | Korean      | 4.3    | $$$   | C
Roti Roll Bombay Frankie     | Uptown       | Indian      | 4.2    | $     | A
Jacob's Pickles              | Uptown       | American    | null   | $$    | null
Dan and John's Wings         | Downtown     | American    | 4.5    | $     | A
Ping's Seafood               | Chinatown    | Chinese     | 4.2    | $$    | A
XO Kitchen                   | Chinatown    | Chinese     | 4.0    | $     | B
Carbone                      | Downtown     | Italian     | 4.3    | $$$   | A
I Sodi                       | Downtown     | Italian     | 4.5    | $$$   | A
Lilia                        | Brooklyn     | Italian     | 4.4    | $$$   | A
Enid's                       | Brooklyn     | Soul Food   | 4.0    | $$    | A
Jajaja                       | Downtown     | Vegetarian  | 4.5    | $$    | A
Smalls Jazz Club             | Downtown     | American    | null   | $$    | A
Russ & Daughters             | Downtown     | American    | 4.6    | $$    | A
The Meatball Shop            | Downtown     | American    | 4.2    | $     | A
Dirt Candy                   | Downtown     | Vegetarian  | 4.4    | $$$   | A
Ippudo                       | Downtown     | Japanese    | 4.4    | $$    | A
St. Anselm                   | Brooklyn     | Steak       | 4.5    | $$    | A
Marea                        | Midtown      | Italian     | 4.5    | $$$$  | A
Lighthouse                   | Brooklyn     | American    | 4.6    | $$    | null
Los Hermanos                 | Brooklyn     | Mexican     | 4.4    | $     | null
The Standard Biergarten      | Downtown     | American    | 4.0    | $$    | A
Ootoya                       | Downtown     | Japanese    | 4.5    | $$    | A
```
**(2.)** What are the distinct `neighborhoods`?
```SQL
SELECT DISTINCT neighborhood
FROM nomnom;
```
### 🟩 Output
```SQL
   neighborhood   
-------------------
     Brooklyn     
     Midtown      
    Chinatown     
      Uptown      
      Queens      
    Downtown      
```
**(3.)** What are the distinct `cuisine` types?
```SQL
SELECT DISTINCT cuisine
FROM nomnom;
```
### 🟩 Output
```SQL
cuisine
Steak
Korean
Chinese
Pizza
Ethiopian
Vegetarian
Italian
Japanese
American
Mediterranean
Indian
Soul Food
Mexican
```
**(4.)** Suppose we would like some `Chinese` takeout.                         
What are our options?
```SQL
SELECT * FROM nomnom
WHERE cuisine = 'Chinese';
```
### 🟩 Output
```SQL
              name              | neighborhood | cuisine | review | price | health
--------------------------------+--------------+---------+--------+-------+--------
Nom Wah Tea Parlor             | Chinatown    | Chinese |   4.2  |   $   |   A
Nan Xiang Xiao Long Bao        | Queens       | Chinese |   4.2  |   $   |   A
Mission Chinese Food           | Downtown     | Chinese |   3.9  |  $$   |   A
Baohaus                        | Downtown     | Chinese |   4.2  |   $   |   A
Xi'an Famous Foods             | Midtown      | Chinese |   4.4  |   $   |   A
Sonnyboy's                     | Brooklyn     | Chinese |   4.2  |  $$   |   A
Great NY Noodletown            | Chinatown    | Chinese |   4.1  |  $$   |   B
Golden Unicorn                 | Chinatown    | Chinese |   3.8  |  $$   |   A
Wo Hop                         | Chinatown    | Chinese |   4.2  |  $$   |  null
Ping's Seafood                 | Chinatown    | Chinese |   4.2  |  $$   |   A
XO Kitchen                     | Chinatown    | Chinese |   4.0  |   $   |   B
```
**(5.)** Return all the restaurants with `reviews` of 4 and above.
```sql
SELECT * FROM nomnom
WHERE review >= 4;
```
### 🟩 Output
```sql
| Name                       	            | Neighborhood | Cuisine       | Review | Price | Health |
|-----------------------------------------|--------------|---------------|--------|-------|--------|
| Peter Luger Steak House                | Brooklyn     | Steak         | 4.4    | $$$$  | A      |
| Jongro BBQ                             | Midtown      | Korean        | 4.5    | $$    | A      |
| Pocha 32                               | Midtown      | Korean        | 4.0    | $$    | A      |
| Nom Wah Tea Parlor                     | Chinatown    | Chinese       | 4.2    | $     | A      |
| Roberta's                              | Brooklyn     | Pizza         | 4.4    | $$    | A      |
| Speedy Romeo                           | Brooklyn     | Pizza         | 4.4    | $$    | A      |
| Bunna Cafe                             | Brooklyn     | Ethiopian     | 4.6    | $$    | A      |
| Massawa                                | Uptown       | Ethiopian     | 4.0    | $$    | null   |
| Buddha Bodai                           | Chinatown    | Vegetarian    | 4.2    | $$    | A      |
| Nan Xiang Xiao Long Bao                | Queens       | Chinese       | 4.2    | $     | A      |
| Baohaus                                | Downtown     | Chinese       | 4.2    | $     | A      |
| al di la Trattoria                     | Brooklyn     | Italian       | 4.4    | $$$   | A      |
| Locanda Vini & Olii                    | Brooklyn     | Italian       | 4.4    | $$$   | A      |
| Rao's                                  | Uptown       | Italian       | 4.2    | $$$   | A      |
| Minca                                  | Downtown     | Japanese      | 4.4    | $$    | A      |
| Kenka                                  | Downtown     | Japanese      | 4.3    | $     | B      |
| Yakitori Taisho                        | Downtown     | Japanese      | 4.1    | $     | B      |
| Xi'an Famous Foods                     | Midtown      | Chinese       | 4.4    | $     | A      |
| Shake Shack                            | Midtown      | American      | 4.4    | $     | A      |
| The Halal Guys                         | Midtown      | Mediterranean | 4.4    | $     | A      |
| Foodcademy                             | Midtown      | American      | 4.4    | $$    | A      |
| Sonnyboy's                             | Brooklyn     | Chinese       | 4.2    | $$    | A      |
| Scorpio Sisters                        | Downtown     | American      | 4.2    | $$    | A      |
| N.E.D                                  | Uptown       | American      | 4.2    | $$$   | A      |
| Great NY Noodletown                    | Chinatown    | Chinese       | 4.1    | $$    | B      |
| Wo Hop                                 | Chinatown    | Chinese       | 4.2    | $$    | null   |
| Di Fara Pizza                          | Brooklyn     | Pizza         | 4.2    | $$    | A      |
| Kang Ho Dong Baekjeong                 | Midtown      | Korean        | 4.3    | $$$   | C      |
| Roti Roll Bombay Frankie               | Uptown       | Indian        | 4.2    | $     | A      |
| Dan and John's Wings                  | Downtown     | American      | 4.5    | $     | A      |
| Ping's Seafood                         | Chinatown    | Chinese       | 4.2    | $$    | A      |
| XO Kitchen                             | Chinatown    | Chinese       | 4.0    | $     | B      |
| Carbone                                | Downtown     | Italian       | 4.3    | $$$   | A      |
| I Sodi                                 | Downtown     | Italian       | 4.5    | $$$   | A      |
| Lilia                                  | Brooklyn     | Italian       | 4.4    | $$$   | A      |
| Enid's                                 | Brooklyn     | Soul Food     | 4.0    | $$    | A      |
| Jajaja                                 | Downtown     | Vegetarian    | 4.5    | $$    | A      |
| Russ & Daughters                        | Downtown     | American      | 4.6    | $$    | A      |
| The Meatball Shop                      | Downtown     | American      | 4.2    | $     | A      |
| Dirt Candy                             | Downtown     | Vegetarian    | 4.4    | $$$   | A      |
| Ippudo                                 | Downtown     | Japanese      | 4.4    | $$    | A      |
| St. Anselm                             | Brooklyn     | Steak         | 4.5    | $$    | A      |
| Marea                                  | Midtown      | Italian       | 4.5    | $$$$  | A      |
| Lighthouse                             | Brooklyn     | American      | 4.6    | $$    | null   |
| Los Hermanos                           | Brooklyn     | Mexican       | 4.4    | $     | null   |
| The Standard Biergarten                | Downtown     | American      | 4.0    | $$    | A      |
| Ootoya                                 | Downtown     | Japanese      | 4.5    | $$    | A      |
```
**(6.)** Suppose Abbi and Ilana want to have a fancy dinner date.                  
Return all the restaurants that are `Italian` and `$$$`.

📝 If you want to find Italian restaurants with exactly three dollar signs:
```sql
SELECT * FROM nomnom
WHERE cuisine = 'Italian'
AND price = '$$$';
```
### 🟩 Output
```sql
| Name                 	     | Neighborhood | Cuisine | Review | Price | Health |
|----------------------------|--------------|---------|--------|-------|--------|
| al di la Trattoria        | Brooklyn     | Italian | 4.4    | $$$   | A      |
| Locanda Vini & Olii       | Brooklyn     | Italian | 4.4    | $$$   | A      |
| Rao's                     | Uptown       | Italian | 4.2    | $$$   | A      |
| Carbone                   | Downtown     | Italian | 4.3    | $$$   | A      |
| I Sodi                    | Downtown     | Italian | 4.5    | $$$   | A      |
| Lilia                     | Brooklyn     | Italian | 4.4    | $$$   | A      |
```
📝 If you want to find Italian restaurants with at least three dollar signs: 
```sql
SELECT * FROM nomnom
WHERE cuisine = 'Italian'
AND price LIKE '%$$$%';
```
### 🟩 Output
```sql
| Name                      	        | Neighborhood | Cuisine | Review | Price  | Health |
|------------------------------------|--------------|---------|--------|--------|--------|
| al di la Trattoria              	| Brooklyn     | Italian | 4.4    | $$$    | A      |
| Locanda Vini & Olii             	| Brooklyn     | Italian | 4.4    | $$$    | A      |
| Rao's                           	| Uptown       | Italian | 4.2    | $$$    | A      |
| The Cole Romano Experience      	| Brooklyn     | Italian | 2.1    | $$$$$  | C      |
| Carbone                         	| Downtown     | Italian | 4.3    | $$$    | A      |
| I Sodi                          	| Downtown     | Italian | 4.5    | $$$    | A      |
| Lilia                           	| Brooklyn     | Italian | 4.4    | $$$    | A      |
| Marea                           	| Midtown      | Italian | 4.5    | $$$$   | A      |
```
**(7.)** Your coworker Trey can’t remember the exact name of a restaurant he went to but he knows it contains the word ‘meatball’ in it.                                             
Can you find it for him using a query?
```sql
SELECT * FROM nomnom
WHERE name LIKE '%meatball%';
```
### 🟩 Output
```sql
| id | name              | neighborhood | cuisine  | review | price | health |
| -- | ----------------- | ------------ | -------- | ------ | ----- | ------ |
| 1  | The Meatball Shop | Downtown     | American | 4.2    | \$    | A      |
```
**(8.)** Let’s order delivery to the house!                          
Find all the close by spots in `Midtown`, `Downtown` or `Chinatown`.    
(`OR` can be used more than once)                                    
<img width="253" alt="image" src="https://github.com/user-attachments/assets/7e354dad-2fbe-4a58-b8d8-d42c007593df" />

```sql
SELECT *
FROM nomnom
WHERE neighborhood = 'Midtown'
   OR neighborhood = 'Downtown'
   OR neighborhood = 'Chinatown'; 
```
### 🟩 Output
```sql
| **Name**                | **Neighborhood** | **Cuisine**   | **Review** | **Price** | **Health** |
| ----------------------- | ---------------- | ------------- | ---------- | --------- | ---------- |
| Jongro BBQ              | Midtown          | Korean        | 4.5        | \$\$      | A          |
| Pocha 32                | Midtown          | Korean        | 4.0        | \$\$      | A          |
| Nom Wah Tea Parlor      | Chinatown        | Chinese       | 4.2        | \$        | A          |
| Buddha Bodai            | Chinatown        | Vegetarian    | 4.2        | \$\$      | A          |
| Mission Chinese Food    | Downtown         | Chinese       | 3.9        | \$\$      | A          |
| Baohaus                 | Downtown         | Chinese       | 4.2        | \$        | A          |
| Minca                   | Downtown         | Japanese      | 4.4        | \$\$      | A          |
| Kenka                   | Downtown         | Japanese      | 4.3        | \$        | B          |
| Yakitori Taisho         | Downtown         | Japanese      | 4.1        | \$        | B          |
| Xi'an Famous Foods      | Midtown          | Chinese       | 4.4        | \$        | A          |
| Shake Shack             | Midtown          | American      | 4.4        | \$        | A          |
| The Halal Guys          | Midtown          | Mediterranean | 4.4        | \$        | A          |
| Foodcademy              | Midtown          | American      | 4.4        | \$\$      | A          |
| Scorpio Sisters         | Downtown         | American      | 4.2        | \$\$      | A          |
| Great NY Noodletown     | Chinatown        | Chinese       | 4.1        | \$\$      | B          |
| Golden Unicorn          | Chinatown        | Chinese       | 3.8        | \$\$      | A          |
| Wo Hop                  | Chinatown        | Chinese       | 4.2        | \$\$      | null       |
| Kang Ho Dong Baekjeong  | Midtown          | Korean        | 4.3        | \$\$\$    | C          |
| Dan and John's Wings    | Downtown         | American      | 4.5        | \$        | A          |
| Ping's Seafood          | Chinatown        | Chinese       | 4.2        | \$\$      | A          |
| XO Kitchen              | Chinatown        | Chinese       | 4.0        | \$        | B          |
| Carbone                 | Downtown         | Italian       | 4.3        | \$\$\$    | A          |
| I Sodi                  | Downtown         | Italian       | 4.5        | \$\$\$    | A          |
| Jajaja                  | Downtown         | Vegetarian    | 4.5        | \$\$      | A          |
| Smalls Jazz Club        | Downtown         | American      | null       | \$\$      | A          |
| Russ & Daughters        | Downtown         | American      | 4.6        | \$\$      | A          |
| The Meatball Shop       | Downtown         | American      | 4.2        | \$        | A          |
| Dirt Candy              | Downtown         | Vegetarian    | 4.4        | \$\$\$    | A          |
| Ippudo                  | Downtown         | Japanese      | 4.4        | \$\$      | A          |
| Marea                   | Midtown          | Italian       | 4.5        | \$\$\$\$  | A          |
| The Standard Biergarten | Downtown         | American      | 4.0        | \$\$      | A          |
| Ootoya                  | Downtown         | Japanese      | 4.5        | \$\$      | A          |
```
**(9.)** Find all the `health` grade pending restaurants (empty values).
```sql
SELECT * FROM nomnom
WHERE health IS NULL;
```
### 🟩 Output
```SQL
| **Name**        | **Neighborhood** | **Cuisine** | **Review** | **Price** | **Health** |
| --------------- | ---------------- | ----------- | ---------- | --------- | ---------- |
| Massawa         | Uptown           | Ethiopian   | 4.0        | \$\$      | null       |
| Wo Hop          | Chinatown        | Chinese     | 4.2        | \$\$      | null       |
| Jacob's Pickles | Uptown           | American    | null       | \$\$      | null       |
| Lighthouse      | Brooklyn         | American    | 4.6        | \$\$      | null       |
| Los Hermanos    | Brooklyn         | Mexican     | 4.4        | \$        | null       |
```
**(10.)** Create a Top 10 Restaurants Ranking based on `reviews`.
```SQL
SELECT * FROM nomnom
ORDER BY review DESC
LIMIT 10;
```
### 🟩 Output
```SQL
| **Name**             | **Neighborhood** | **Cuisine** | **Review** | **Price** | **Health** |
| -------------------- | ---------------- | ----------- | ---------- | --------- | ---------- |
| Bunna Cafe           | Brooklyn         | Ethiopian   | 4.6        | \$\$      | A          |
| Russ & Daughters     | Downtown         | American    | 4.6        | \$\$      | A          |
| Lighthouse           | Brooklyn         | American    | 4.6        | \$\$      | null       |
| Jongro BBQ           | Midtown          | Korean      | 4.5        | \$\$      | A          |
| Dan and John's Wings | Downtown         | American    | 4.5        | \$        | A          |
| I Sodi               | Downtown         | Italian     | 4.5        | \$\$\$    | A          |
| Jajaja               | Downtown         | Vegetarian  | 4.5        | \$\$      | A          |
| St. Anselm           | Brooklyn         | Steak       | 4.5        | \$\$      | A          |
| Marea                | Midtown          | Italian     | 4.5        | \$\$\$\$  | A          |
| Ootoya               | Downtown         | Japanese    | 4.5        | \$\$      | A          |
```
**(11.)** Use a `CASE` statement to change the rating system to:                              
* `review > 4.5` is Extraordinary
* `review > 4` is Excellent
* `review > 3` is Good
* `review > 2` is Fair
* Everything else is Poor
Don’t forget to rename the new column!
```sql
SELECT name,
 CASE
  WHEN review > 4.5 THEN 'Extraordinary'
  WHEN review > 4 THEN 'Excellent'
  WHEN review > 3 THEN 'Good'
  WHEN review > 2 THEN 'Fair'
  ELSE 'Poor'
 END AS 'Review'
FROM nomnom;
```
### 🟩 Output
```sql
| **Name**                   | **REVIEW**    |
| -------------------------- | ------------- |
| Peter Luger Steak House    | Excellent     |
| Jongro BBQ                 | Excellent     |
| Pocha 32                   | Good          |
| Nom Wah Tea Parlor         | Excellent     |
| Roberta's                  | Excellent     |
| Speedy Romeo               | Excellent     |
| Bunna Cafe                 | Extraordinary |
| Massawa                    | Good          |
| Buddha Bodai               | Excellent     |
| Nan Xiang Xiao Long Bao    | Excellent     |
| Mission Chinese Food       | Good          |
| Baohaus                    | Excellent     |
| al di la Trattoria         | Excellent     |
| Locanda Vini & Olii        | Excellent     |
| Rao's                      | Excellent     |
| Minca                      | Excellent     |
| Kenka                      | Excellent     |
| Yakitori Taisho            | Excellent     |
| Xi'an Famous Foods         | Excellent     |
| Shake Shack                | Excellent     |
| The Halal Guys             | Excellent     |
| Foodcademy                 | Excellent     |
| Sonnyboy's                 | Excellent     |
| The Cole Romano Experience | Fair          |
| Timbo Slice                | Fair          |
| Scorpio Sisters            | Excellent     |
| N.E.D                      | Excellent     |
| Great NY Noodletown        | Excellent     |
| Golden Unicorn             | Good          |
| Wo Hop                     | Excellent     |
| Di Fara Pizza              | Excellent     |
| Kang Ho Dong Baekjeong     | Excellent     |
| Roti Roll Bombay Frankie   | Excellent     |
| Jacob's Pickles            | Poor          |
| Dan and John's Wings       | Excellent     |
| Ping's Seafood             | Excellent     |
| XO Kitchen                 | Good          |
| Carbone                    | Excellent     |
| I Sodi                     | Excellent     |
| Lilia                      | Excellent     |
| Enid's                     | Good          |
| Jajaja                     | Excellent     |
| Smalls Jazz Club           | Poor          |
| Russ & Daughters           | Extraordinary |
| The Meatball Shop          | Excellent     |
| Dirt Candy                 | Excellent     |
| Ippudo                     | Excellent     |
| St. Anselm                 | Excellent     |
| Marea                      | Excellent     |
| Lighthouse                 | Extraordinary |
| Los Hermanos               | Excellent     |
| The Standard Biergarten    | Good          |
| Ootoya                     | Excellent     |
```

