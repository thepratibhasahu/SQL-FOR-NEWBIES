# Lyft Trip Data

Let’s practice what we learned about joins by combining rows from different tables.

Suppose you are a Data Analyst at Lyft, a ride-sharing platform. For a project, you were given three tables:

* `trips:` trips information
* `riders:` user data
* `cars:` autonomous cars

# Write the following queries:
**(1.)** Let’s examine the three tables.                                                    
What are the column names?
```sql
SELECT * FROM trips;

SELECT * FROM riders;

SELECT * FROM cars;
```
### 🟩Output
```sql
id     date        pickup  dropoff  rider_id  car_id  type  cost
1001   2017-12-05  06:45    07:10     102        1     X     28.66
1002   2017-12-05  08:00    08:15     101        3     POOL   9.11
1003   2017-12-05  09:30    09:50     104        4     X     24.98
1004   2017-12-05  13:40    14:05     105        1     X     31.27
1005   2017-12-05  15:15    16:00     103        2     POOL  18.95
1006   2017-12-05  18:20    18:55     101        3     XL    78.52

id   first   last     username      rating  total_trips  referred
101  Sonny   Li       @sonnynomnom   4.66       352        null
102  Laura   Breiman  @lauracle      4.99       687         101
103  Kassa   Korley   @kassablanca   4.63        42        null
104  Yakov   Kagan    @yakovkagan    4.52      1910         103

id   model      OS      status        trips_completed
1    Ada        Ryzac   active                82
2    Ada        Ryzac   active                30
3    Turing XL  Ryzac   active               164
4    Akira      Finux   maintenance           22
```
**(2.)** * What’s the primary key of `trips`?

* What’s the primary key of `riders`?

* What’s the primary key of `cars`?

**ANSWER**
```sql
The primary key of trips is id.

The primary key of riders is id.

The primary key of cars is id.
```
* They have the same name, but they are very different.

**(3.)** Try out a simple cross join between `riders` and `cars`.                                    
Is the result useful?
```SQL
SELECT * FROM riders
CROSS JOIN cars;
```
### 🟩Output
```sql
rider_id	first_name	last_name	username       	rating	total_trips	referred	car_id	model     	OS    	status      	trips_completed
101      	Sonny    	Li      	@sonnynomnom   	4.66  	352        	null    	1     	Ada       	Ryzac 	active       	82
101      	Sonny    	Li      	@sonnynomnom   	4.66  	352        	null    	2     	Ada       	Ryzac 	active       	30
101      	Sonny    	Li      	@sonnynomnom   	4.66  	352        	null    	3     	Turing XL	Ryzac 	active       	164
101      	Sonny    	Li      	@sonnynomnom   	4.66  	352        	null    	4     	Akira     	Finux 	maintenance  	22
102      	Laura    	Breiman 	@lauracle      	4.99  	687        	101     	1     	Ada       	Ryzac 	active       	82
102      	Laura    	Breiman 	@lauracle      	4.99  	687        	101     	2     	Ada       	Ryzac 	active       	30
102      	Laura    	Breiman 	@lauracle      	4.99  	687        	101     	3     	Turing XL	Ryzac 	active       	164
102      	Laura    	Breiman 	@lauracle      	4.99  	687        	101     	4     	Akira     	Finux 	maintenance  	22
103      	Kassa    	Korley  	@kassablanca   	4.63  	42         	null    	1     	Ada       	Ryzac 	active       	82
103      	Kassa    	Korley  	@kassablanca   	4.63  	42         	null    	2     	Ada       	Ryzac 	active       	30
103      	Kassa    	Korley  	@kassablanca   	4.63  	42         	null    	3     	Turing XL	Ryzac 	active       	164
103      	Kassa    	Korley  	@kassablanca   	4.63  	42         	null    	4     	Akira     	Finux 	maintenance  	22
104      	Yakov    	Kagan   	@yakovkagan    	4.52  	1910       	103     	1     	Ada       	Ryzac 	active       	82
104      	Yakov    	Kagan   	@yakovkagan    	4.52  	1910       	103     	2     	Ada       	Ryzac 	active       	30
104      	Yakov    	Kagan   	@yakovkagan    	4.52  	1910       	103     	3     	Turing XL	Ryzac 	active       	164
104      	Yakov    	Kagan   	@yakovkagan    	4.52  	1910       	103     	4     	Akira     	Finux 	maintenance  	22
```
**(4.)** Suppose we want to create a Trip Log with the trips and its users.                             
Find the columns to join between `trips` and `riders` and combine the two tables using a `LEFT JOIN`.               
Let `trips` be the left table.
```SQL
SELECT *
FROM trips
LEFT JOIN riders 
  ON trips.rider_id = riders.id;
```
### 🟩Output
```sql
| trip\_id | date       | pickup | dropoff | rider\_id | car\_id | type | cost  | rider\_info\_id | first | last    | username     | rating | total\_trips | referred |
| -------- | ---------- | ------ | ------- | --------- | ------- | ---- | ----- | --------------- | ----- | ------- | ------------ | ------ | ------------ | -------- |
| 1001     | 2017-12-05 | 06:45  | 07:10   | 102       | 1       | X    | 28.66 | 102             | Laura | Breiman | @lauracle    | 4.99   | 687          | 101      |
| 1002     | 2017-12-05 | 08:00  | 08:15   | 101       | 3       | POOL | 9.11  | 101             | Sonny | Li      | @sonnynomnom | 4.66   | 352          | null     |
| 1003     | 2017-12-05 | 09:30  | 09:50   | 104       | 4       | X    | 24.98 | 104             | Yakov | Kagan   | @yakovkagan  | 4.52   | 1910         | 103      |
| 1004     | 2017-12-05 | 13:40  | 14:05   | 105       | 1       | X    | 31.27 | null            | null  | null    | null         | null   | null         | null     |
| 1005     | 2017-12-05 | 15:15  | 16:00   | 103       | 2       | POOL | 18.95 | 103             | Kassa | Korley  | @kassablanca | 4.63   | 42           | null     |
| 1006     | 2017-12-05 | 18:20  | 18:55   | 101       | 3       | XL   | 78.52 | 101             | Sonny | Li      | @sonnynomnom | 4.66   | 352          | null     |
```
**(5.)** Suppose we want to create a link between the `trips` and the `cars` used during those trips.             
Find the columns to join on and combine the `trips` and `cars` table using an `INNER JOIN`.
```SQL
SELECT * FROM trips
INNER JOIN cars
ON trips.car_id = cars.id;
```
### 🟩Output
```sql
| **ride\_id** | **date**   | **pickup** | **dropoff** | **rider\_id** | **car\_id** | **ride\_type** | **cost** | **car\_id (again)** | **model** | **OS** | **status**  | **trips\_completed** |
| ------------ | ---------- | ---------- | ----------- | ------------- | ----------- | -------------- | -------- | ------------------- | --------- | ------ | ----------- | -------------------- |
| 1001         | 2017-12-05 | 06:45      | 07:10       | 102           | 1           | X              | 28.66    | 1                   | Ada       | Ryzac  | active      | 82                   |
| 1002         | 2017-12-05 | 08:00      | 08:15       | 101           | 3           | POOL           | 9.11     | 3                   | Turing XL | Ryzac  | active      | 164                  |
| 1003         | 2017-12-05 | 09:30      | 09:50       | 104           | 4           | X              | 24.98    | 4                   | Akira     | Finux  | maintenance | 22                   |
| 1004         | 2017-12-05 | 13:40      | 14:05       | 105           | 1           | X              | 31.27    | 1                   | Ada       | Ryzac  | active      | 82                   |
| 1005         | 2017-12-05 | 15:15      | 16:00       | 103           | 2           | POOL           | 18.95    | 2                   | Ada       | Ryzac  | active      | 30                   |
| 1006         | 2017-12-05 | 18:20      | 18:55       | 101           | 3           | XL             | 78.52    | 3                   | Turing XL | Ryzac  | active      | 164                  |
```
📝 The `JOIN` keyword can also be `INNER JOIN`.

**(6.)** The new riders data are in! There are three new users this month.                           
Stack the `riders` table on top of the new table named `riders2`.
```SQL
SELECT *
FROM riders
UNION
SELECT *
FROM riders2;
```
### 🟩Output
```sql
id     | first    | last      | username      | rating | total_trips | referred
-------|----------|-----------|---------------|--------|--------------|----------
101    | Sonny    | Li        | @sonnynomnom  | 4.66   | 352          | NULL
102    | Laura    | Breiman   | @lauracle     | 4.99   | 687          | 101
103    | Kassa    | Korley    | @kassablanca  | 4.63   | 42           | NULL
104    | Yakov    | Kagan     | @yakovkagan   | 4.52   | 1910         | 103
105    | Zach     | Sims      | @zsims        | 4.85   | 787          | NULL
106    | Eric     | Vaught    | @posturelol   | 4.96   | 54           | 101
107    | Jilly    | Beans     | @jillkuzmin   | 4.70   | 32           | 101
```
📝 For stacking one dataset on top of another, we use `UNION`.

# Bonus: Queries and Aggregates

**(7.)** What is the average `cost` for a trip?
```sql
SELECT AVG(cost)
FROM trips;
```
### 🟩Output
```sql
+------------+
| AVG(cost)  |
+------------+
|   31.915   |
+------------+
```
**(8.)** Lyft is looking to do an email campaign for all the irregular users.                        
Find all the `riders` who have used Lyft less than 500 times!
```sql
SELECT *
FROM riders
WHERE total_trips < 500;
```
### 🟩Output
```sql
| id  | first | last   | username     | rating | total\_trips | referred |
| --- | ----- | ------ | ------------ | ------ | ------------ | -------- |
| 101 | Sonny | Li     | @sonnynomnom | 4.66   | 352          | NULL     |
| 103 | Kassa | Korley | @kassablanca | 4.63   | 42           | NULL     |
```
* If we want to search in both `riders` and `riders2`, then we might have to do something like this:
```sql
SELECT *
FROM riders
WHERE total_trips < 500
UNION
SELECT *
FROM riders2
WHERE total_trips < 500;
```
### 🟩Output
```sql
| id  | first | last   | username     | rating | total\_trips | referred |
| --- | ----- | ------ | ------------ | ------ | ------------ | -------- |
| 101 | Sonny | Li     | @sonnynomnom | 4.66   | 352          | NULL     |
| 103 | Kassa | Korley | @kassablanca | 4.63   | 42           | NULL     |
| 106 | Eric  | Vaught | @posturelol  | 4.96   | 54           | 101      |
| 107 | Jilly | Beans  | @jillkuzmin  | 4.70   | 32           | 101      |
```
**(9.)** Calculate the number of cars that are `active`.
```sql
SELECT COUNT(*)
FROM cars
WHERE status = 'active';
```
### 🟩Output
```SQL
COUNT(*)
  3
```
**(10.)** It’s safety recall time for cars that have been on the road for a while.                        
Write a query that finds the two cars that have the highest `trips_completed`.
```sql
SELECT *
FROM cars
ORDER BY trips_completed DESC
LIMIT 2;
```
### 🟩Output
```SQL
| id | model     | OS    | status | trips\_completed |
| -- | --------- | ----- | ------ | ---------------- |
| 3  | Turing XL | Ryzac | active | 164              |
| 1  | Ada       | Ryzac | active | 82               |
```
