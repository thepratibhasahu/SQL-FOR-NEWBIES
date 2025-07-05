# Introduction

In order to efficiently store data, we often spread related information across multiple tables.

For instance, imagine that we’re running a magazine company where users can have different types of subscriptions to different products. Different subscriptions might have many different properties. Each customer would also have lots of associated information.

We could have one table with all of the following information:                                                        
* `order_id`
* `customer_id`
* `customer_name`
* `customer_address`
* `subscription_id`
* `subscription_description`
* `subscription_monthly_price`
* `subscription_length`
* `purchase_date`

However, a lot of this information would be repeated. If the same customer has multiple subscriptions, that customer’s name and address will be reported multiple times. If the same subscription type is ordered by multiple customers, then the subscription price and subscription description will be repeated. This will make our table big and unmanageable.

So instead, we can split our data into three tables:

1. `orders` would contain just the information necessary to describe what was ordered:

* `order_id`, `customer_id`, `subscription_id`, `purchase_date`

2. `subscriptions` would contain the information to describe each type of subscription:

* `subscription_id`, `description`, `price_per_month`, `subscription_length`

3. `customers` would contain the information for each customer:

* `customer_id`, `customer_name`, `address`

📝 In this lesson, we’ll learn the `SQL commands` that will help us work with data that is stored in multiple tables.

**(1.)** Examine these tables by pasting the following code into the editor:
```SQL
SELECT *
FROM orders
LIMIT 5;

SELECT *
FROM subscriptions
LIMIT 5;

SELECT * 
FROM customers
LIMIT 5;
```
### 🟩Output 
```SQL
 → Orders Table
| order_id  | customer_id  | subscription_id  | purchase_date  |
| --------- | ------------ | ---------------- | -------------- |
| 1         | 3            | 2                | 01-10-2017     |
| 2         | 2            | 4                | 01-09-2017     |
| 3         | 3            | 4                | 01-26-2017     |
| 4         | 9            | 9                | 01-04-2017     |
| 5         | 7            | 5                | 01-25-2017     |

→ Subscriptions Table
| subscription_id  | description       | price_per_month   | subscription_length  |
| ---------------- | ----------------- | ----------------- | -------------------- |
| 1                | Politics Magazine | 10                | 12 months            |
| 2                | Politics Magazine | 11                | 6 months             |
| 3                | Politics Magazine | 12                | 3 months             |
| 4                | Fashion Magazine  | 15                | 12 months            |
| 5                | Fashion Magazine  | 17                | 6 months             |

→  Customers Table
| customer_id  | customer_name    | address          |
| ------------ | ---------------- | ---------------- |
| 1            | Allie Rahaim     | 123 Broadway     |
| 2            | Jacquline Diddle | 456 Park Ave.    |
| 3            | Lizabeth Letsche | 789 Main St.     |
| 4            | Jessia Butman    | 1 Columbus Ave.  |
| 5            | Inocencia Goyco  | 12 Amsterdam Ave |
```
# Combining Tables Manually
Let’s return to our magazine company. Suppose we have the three tables described in the previous exercise – shown in the browser on the right (we are going to try something new!):

* orders
* subscriptions
* customers

If we just look at the `orders` table, we can’t really tell what’s happened in each order. However, if we refer to the other tables, we can get a complete picture.

Let’s examine the order with an `order_id` of 2. It was purchased by the customer with a `customer_id` of 2.

To find out the customer’s name, we look at the `customers` table and look for the item with a `customer_id` value of 2. We can see that Customer 2’s name is ‘Jane Doe’ and that she lives at ‘456 Park Ave’.

Doing this kind of matching is called **joining** two tables.

**(1.)** Using the tables displayed, what is the `description` of the magazine ordered in `order_id` 1?              
Type your answer on line 1 of the code editor (this is not a query).                                  
Be sure to capitalize it the same as in the table.

![Screenshot 2025-06-29 222912](https://github.com/user-attachments/assets/587d8152-9265-4b28-a9af-309c3efa70d3)
![Screenshot 2025-06-29 222948](https://github.com/user-attachments/assets/fef9ab55-85c1-4806-8d3b-bad9a46d762c)
![Screenshot 2025-06-29 223024](https://github.com/user-attachments/assets/9136ce29-dd82-4eca-9eee-0f1e2e4832f8)

* First, we look at the `orders` table.                                      
* The order with an `order_id` of 1 is in the first row. Its `subscription_id` is 3.
* Then we look at the `subscriptions` table.
* The subscription with a `subscription_id` of 3 is in the third row. Its `description` is Sports Magazine.

```sql
Answer: Sports Magazine
```

**(2.)** Using the tables displayed, what is the `customer_name` of the customer in `order_id` 3?                  
Type your answer on line 2 of the code editor.                                 
Be sure to capitalize it the same as in the table.

![Screenshot 2025-06-29 222912](https://github.com/user-attachments/assets/587d8152-9265-4b28-a9af-309c3efa70d3)
![Screenshot 2025-06-29 222948](https://github.com/user-attachments/assets/fef9ab55-85c1-4806-8d3b-bad9a46d762c)
![Screenshot 2025-06-29 223024](https://github.com/user-attachments/assets/9136ce29-dd82-4eca-9eee-0f1e2e4832f8)

```sql
Answer: Joe Schmo
```
# Combining Tables with SQL
Combining tables manually is time-consuming. Luckily, SQL gives us an easy sequence for this: it’s called a `JOIN`.

If we want to combine `orders` and `customers`, we would type:
```sql
SELECT *
FROM orders
JOIN customers
  ON orders.customer_id = customers.customer_id;
```
→ Let’s break down this command:

**1.** The first line selects all columns from our combined table. If we only want to select certain columns, we can specify which ones we want.

**2.** The second line specifies the first table that we want to look in, `orders`.

**3.** The third line uses `JOIN` to say that we want to combine information from `orders` with `customers`.

**4.** The fourth line tells us how to combine the two tables. We want to match `orders` table’s `customer_id` column with `customers` table’s `customer_id` column.

Because column names are often repeated across multiple tables, we use the syntax `table_name.column_name` to be sure that our requests for columns are unambiguous. In our example, we use this syntax in the `ON` statement, but we will also use it in the `SELECT` or any other statement where we refer to column names.

For example: Instead of selecting all the columns using `*`, if we only wanted to select `orders` table’s `order_id` column and `customers` table’s `customer_name` column, we could use the following query:
```sql
SELECT orders.order_id,
   customers.customer_name
FROM orders
JOIN customers
  ON orders.customer_id = customers.customer_id;
```
**(1.)** Join `orders` table and `subscriptions` table and select all columns.                    
Make sure to join on the `subscription_id` column.
```sql
SELECT *
FROM orders
JOIN subscriptions
  ON orders.subscription_id = subscriptions.subscription_id;
```
### 🟩Output
```sql
| order_id  | customer_id  | subscription_id  | purchase_date  | description       | price_per_month   | subscription_length  |
| --------- | ------------ | ---------------- | -------------- | ----------------- | ----------------- | -------------------- |
| 1         | 3            | 2                | 01-10-2017     | Politics Magazine | 11                | 6 months             |
| 2         | 2            | 4                | 01-9-2017      | Fashion Magazine  | 15                | 12 months            |
| 3         | 3            | 4                | 01-26-2017     | Fashion Magazine  | 15                | 12 months            |
| 4         | 9            | 9                | 01-4-2017      | Sports Magazine   | 13                | 3 months             |
| 5         | 7            | 5                | 01-25-2017     | Fashion Magazine  | 17                | 6 months             |
| 6         | 8            | 2                | 01-18-2017     | Politics Magazine | 11                | 6 months             |
| 7         | 5            | 8                | 01-11-2017     | Sports Magazine   | 12                | 6 months             |
| 8         | 9            | 5                | 01-26-2017     | Fashion Magazine  | 17                | 6 months             |
| 9         | 4            | 4                | 01-25-2017     | Fashion Magazine  | 15                | 12 months            |
| 10        | 1            | 7                | 01-26-2017     | Sports Magazine   | 11                | 12 months            |
| 11        | 5            | 4                | 01-7-2017      | Fashion Magazine  | 15                | 12 months            |
| 12        | 3            | 2                | 01-21-2017     | Politics Magazine | 11                | 6 months             |
| 13        | 3            | 5                | 01-3-2017      | Fashion Magazine  | 17                | 6 months             |
| 14        | 6            | 5                | 01-22-2017     | Fashion Magazine  | 17                | 6 months             |
| 15        | 1            | 2                | 01-6-2017      | Politics Magazine | 11                | 6 months             |
| 16        | 1            | 2                | 01-11-2017     | Politics Magazine | 11                | 6 months             |
| 17        | 3            | 6                | 01-17-2017     | Fashion Magazine  | 19                | 3 months             |
| 18        | 3            | 8                | 01-29-2017     | Sports Magazine   | 12                | 6 months             |
| 19        | 4            | 9                | 01-3-2017      | Sports Magazine   | 13                | 3 months             |
| 20        | 1            | 7                | 01-24-2017     | Sports Magazine   | 11                | 12 months            |
```
**(2.)** Don’t remove the previous query.                                                  
Add a second query after your first one that only selects rows from the join where `description` is equal to ‘Fashion Magazine’.
```sql
-- Checkpoint 1

SELECT *
FROM orders
JOIN subscriptions
  ON orders.subscription_id = subscriptions.subscription_id;

-- Checkpoint 2

SELECT *
FROM orders
JOIN subscriptions
  ON orders.subscription_id = subscriptions.subscription_id
WHERE subscriptions.description = 'Fashion Magazine';
```
### 🟩Output
```sql
| order_id  | customer_id  | subscription_id  | purchase_date  | description       | price_per_month   | subscription_length  |
| --------- | ------------ | ---------------- | -------------- | ----------------- | ----------------- | -------------------- |
| 1         | 3            | 2                | 01-10-2017     | Politics Magazine | 11                | 6 months             |
| 2         | 2            | 4                | 01-9-2017      | Fashion Magazine  | 15                | 12 months            |
| 3         | 3            | 4                | 01-26-2017     | Fashion Magazine  | 15                | 12 months            |
| 4         | 9            | 9                | 01-4-2017      | Sports Magazine   | 13                | 3 months             |
| 5         | 7            | 5                | 01-25-2017     | Fashion Magazine  | 17                | 6 months             |
| 6         | 8            | 2                | 01-18-2017     | Politics Magazine | 11                | 6 months             |
| 7         | 5            | 8                | 01-11-2017     | Sports Magazine   | 12                | 6 months             |
| 8         | 9            | 5                | 01-26-2017     | Fashion Magazine  | 17                | 6 months             |
| 9         | 4            | 4                | 01-25-2017     | Fashion Magazine  | 15                | 12 months            |
| 10        | 1            | 7                | 01-26-2017     | Sports Magazine   | 11                | 12 months            |
| 11        | 5            | 4                | 01-7-2017      | Fashion Magazine  | 15                | 12 months            |
| 12        | 3            | 2                | 01-21-2017     | Politics Magazine | 11                | 6 months             |
| 13        | 3            | 5                | 01-3-2017      | Fashion Magazine  | 17                | 6 months             |
| 14        | 6            | 5                | 01-22-2017     | Fashion Magazine  | 17                | 6 months             |
| 15        | 1            | 2                | 01-6-2017      | Politics Magazine | 11                | 6 months             |
| 16        | 1            | 2                | 01-11-2017     | Politics Magazine | 11                | 6 months             |
| 17        | 3            | 6                | 01-17-2017     | Fashion Magazine  | 19                | 3 months             |
| 18        | 3            | 8                | 01-29-2017     | Sports Magazine   | 12                | 6 months             |
| 19        | 4            | 9                | 01-3-2017      | Sports Magazine   | 13                | 3 months             |
| 20        | 1            | 7                | 01-24-2017     | Sports Magazine   | 11                | 12 months            |

| order_id  | customer_id  | subscription_id  | purchase_date  | description      | price_per_month   | subscription_length  |
| --------- | ------------ | ---------------- | -------------- | ---------------- | ----------------- | -------------------- |
| 2         | 2            | 4                | 01-9-2017      | Fashion Magazine | 15                | 12 months            |
| 3         | 3            | 4                | 01-26-2017     | Fashion Magazine | 15                | 12 months            |
| 9         | 4            | 4                | 01-25-2017     | Fashion Magazine | 15                | 12 months            |
| 11        | 5            | 4                | 01-7-2017      | Fashion Magazine | 15                | 12 months            |
| 5         | 7            | 5                | 01-25-2017     | Fashion Magazine | 17                | 6 months             |
| 8         | 9            | 5                | 01-26-2017     | Fashion Magazine | 17                | 6 months             |
| 13        | 3            | 5                | 01-3-2017      | Fashion Magazine | 17                | 6 months             |
| 14        | 6            | 5                | 01-22-2017     | Fashion Magazine | 17                | 6 months             |
| 17        | 3            | 6                | 01-17-2017     | Fashion Magazine | 19                | 3 months             |
```
📝 The `WHERE` clause goes after the `JOIN`!

# Inner Joins
Let’s revisit how we joined `orders` and `customers`. For every possible value of `customer_id` in `orders`, there was a corresponding row of `customers` with the same `customer_id`.

What if that wasn’t true?

* For instance, imagine that our `customers` table was out of date, and was missing any information on customer 11. If that customer had an order in `orders`, what would happen when we joined the tables?

* When we perform a simple `JOIN` (often called an inner join) our result only includes rows that match our `ON` condition.

* Consider the following animation, which illustrates an inner join of two tables on `table1.c2 = table2.c2`:

<img width="269" alt="image" src="https://github.com/user-attachments/assets/2be21eea-dd87-4c3e-b06b-35ca2b39ad5a" />
<img width="267" alt="image" src="https://github.com/user-attachments/assets/a6bb6f65-6d5d-448b-bd57-722a16a547a0" />
<img width="268" alt="image" src="https://github.com/user-attachments/assets/598adb1c-4162-4261-961c-368006cc6021" />

The first and last rows have matching values of `c2`. The middle rows do not match. The final result has all values from the first and last rows but does not include the non-matching middle row.

**(1.)** Suppose we are working for The Codecademy Times, a newspaper with two types of subscriptions:          
* print newspaper
* online articles

Some users subscribe to just the newspaper, some subscribe to just the online edition, and some subscribe to both.    
There is a `newspaper` table that contains information about the newspaper subscribers.                 
Count the number of subscribers who get a print newspaper using `COUNT()`.
```SQL
SELECT COUNT(*)
FROM newspaper;
```
### 🟩Output
```SQL
  COUNT(*)
------------
    60
```
**(2.)** Don’t remove your previous query.                                  
There is also an `online` table that contains information about the online subscribers.                     
Count the number of subscribers who get an online newspaper using `COUNT()`.
```sql
SELECT COUNT(*) FROM newspaper;

SELECT COUNT(*) FROM online;
```
### 🟩Output
```SQL
  COUNT(*)
------------
    60

 COUNT(*)
------------
    65
```
**(3.)** Don’t remove your previous queries.                            
Join `newspaper` table and `online` table on their `id` columns (the unique ID of the subscriber).              
How many rows are in this table?
```SQL
SELECT COUNT(*) FROM newspaper;

SELECT COUNT(*) FROM online;

SELECT COUNT(*) FROM newspaper
JOIN online 
ON newspaper.id = online.id;
```
### 🟩Output
```SQL
  COUNT(*)
------------
    60

 COUNT(*)
------------
    65

 COUNT(*)
------------
    50
```
# Left Joins
What if we want to combine two tables and keep some of the un-matched rows?

SQL lets us do this through a command called `LEFT JOIN`. A left join will keep all rows from the first table, regardless of whether there is a matching row in the second table.

Consider the following animation:

<img width="267" alt="image" src="https://github.com/user-attachments/assets/62191e4b-000d-446c-81e6-4566bedfdfc4" />
<img width="268" alt="image" src="https://github.com/user-attachments/assets/2afb0bc7-5965-46b7-9507-6bb3fb12a281" />
<img width="269" alt="image" src="https://github.com/user-attachments/assets/fd8c7526-abda-4363-af88-ac8ba439e8f6" />

The first and last rows have matching values of `c2`. The middle rows do not match. The final result will keep all rows of the first table but will omit the un-matched row from the second table.

This animation represents a table operation produced by the following command:
```SQL
SELECT *
FROM table1
LEFT JOIN table2
  ON table1.c2 = table2.c2;
```
* The first line selects all columns from both tables.
* The second line selects `table1` (the “left” table).
* The third line performs a `LEFT JOIN` on `table2` (the “right” table).
* The fourth line tells SQL how to perform the join (by looking for matching values in column `c2`).

**(1.)** Let’s return to our `newspaper` and `online` subscribers.                                  
Suppose we want to know how many users subscribe to the print newspaper, but not to the online.         
Start by performing a left join of `newspaper` table and `online` table on their `id` columns and selecting all columns.
```sql
SELECT *
FROM newspaper
LEFT JOIN online
  ON newspaper.id = online.id;
```
### 🟩Output
```SQL
id_1     first_name_1  last_name_1   email_1                        start_month_1  end_month_1   id_2    first_name_2  last_name_2    email_2                        start_month_2  end_month_2
21253    Vinnie        Sagaser       Vinnie.Sagaser@yoohoo.com       1              5            21253    Vinnie        Sagaser       Vinnie.Sagaser@yoohoo.com       1              5
39075    Francesco     Maddron       FrancescoMaddron81@gsnail.com   1              5            39075    Francesco     Maddron       FrancescoMaddron81@gsnail.com   1              5
30648    Hellen        Broadwater    HBroadwater1992@gsnail.com      2              3            30648    Hellen        Broadwater    HBroadwater1992@gsnail.com      2              3
71778    Ouida         Pardini       Ouida.Pardini@gsnail.com        2              6            NULL     NULL          NULL           NULL                          NULL           NULL
32436    Wenona        Tankson       WTankson1989@gsnail.com         2              6            32436    Wenona        Tankson       WTankson1989@gsnail.com         2              6
55580    Clora         Werking       CWerking1996@gsnail.com         2              5            55580    Clora         Werking       CWerking1996@gsnail.com         2              5
79652    Esteban       Pitner        Esteban.Pitner@gsnail.com       2              4            NULL     NULL          NULL           NULL                          NULL           NULL
11322    Carmel        Deasis        CD3012@gsnail.com               2              6            11322    Carmel        Deasis        CD3012@gsnail.com               2              6
73893    Jessi         Vinson        JessiVinson65@gsnail.com        2              6            73893    Jessi         Vinson        JessiVinson65@gsnail.com        2              6
84750    Ayana         Hodapp        AHodapp1976@coldmail.com        3              6            84750    Ayana         Hodapp        AHodapp1976@coldmail.com        3              6
34187    Francoise     Feliberty     FFeliberty1984@inlook.com       3              7            34187    Francoise     Feliberty     FFeliberty1984@inlook.com       3              7
82566    Dusty         Morrical      DMorrical1977@gsnail.com        3              7            82566    Dusty         Morrical      DMorrical1977@gsnail.com        3              7
31446    Collin        Dobos         CollinDobos57@coldmail.com      3              5            31446    Collin        Dobos         CollinDobos57@coldmail.com      3              5
23496    Fredia        Bi            Fredia.Bi@gsnail.com            4              8            23496    Fredia        Bi            Fredia.Bi@gsnail.com            4              8
34664    Troy          Underwood     Troy.Underwood@gsnail.com       4              6            34664    Troy          Underwood     Troy.Underwood@gsnail.com       4              6
58869    Cordia        Schingeck     CordiaSchingeck82@gsnail.com    4              6            58869    Cordia        Schingeck     CordiaSchingeck82@gsnail.com    4              6
96977    Peter         Haddaway      Peter.Haddaway@gsnail.com       4              8            96977    Peter         Haddaway      Peter.Haddaway@gsnail.com       4              8
17873    Vilma         Colaizzi      VColaizzi1973@gsnail.com        4              5            17873    Vilma         Colaizzi      VColaizzi1973@gsnail.com        4              5
49633    Lane          Dittman       LaneDittman80@gsnail.com        5              9            49633    Lane          Dittman       LaneDittman80@gsnail.com        5              9
37471    Sharice       Mcmindes      SM2234@gsnail.com               5              6            37471    Sharice       Mcmindes      SM2234@gsnail.com               5              6
14227    Grady         Antinore      Grady.Antinore@gsnail.com       5              7            14227    Grady         Antinore      Grady.Antinore@gsnail.com       5              7
90240    Mandy         Ferber        Mandy.Ferber@gsnail.com         5              9            90240    Mandy         Ferber        Mandy.Ferber@gsnail.com         5              9
22237    Olimpia       Padden        OP5814@inlook.com               5              6            22237    Olimpia       Padden        OP5814@inlook.com               5              6
84308    Mechelle      Mcgarrell     MM4920@gsnail.com               5              6            84308    Mechelle      Mcgarrell     MM4920@gsnail.com               5              6
46343    Cecelia       Filipponi     CFilipponi1977@gsnail.com       5              8            NULL     NULL          NULL           NULL                           NULL           NULL
17951    Latasha       Pasket        Latasha.Pasket@gsnail.com       5              6            17951    Latasha       Pasket        Latasha.Pasket@gsnail.com       5              6
32353    Nichole       Vogenthaler   NicholeVogenthaler58@gsnail.com 5              6            32353    Nichole       Vogenthaler   NicholeVogenthaler58@gsnail.com 5              6
59400    Hiedi         Dwight        Hiedi.Dwight@gsnail.com         5              6            59400    Hiedi         Dwight        Hiedi.Dwight@gsnail.com         5              6
12575    Loni          Manchester    LoniManchester25@gsnail.com     5              8            12575    Loni          Manchester     LoniManchester25@gsnail.com    5              8
56665    Maple         Yonts         MY2659@coldmail.com             6              8            56665    Maple         Yonts         MY2659@coldmail.com             6              8
58002    Brooke        Tandetzke     BT7427@gsnail.com               6              7            NULL     NULL          NULL           NULL                           NULL           NULL    |
```
**(2.)** Don’t remove your previous query.                                       
In order to find which users do not subscribe to the online edition, we need to add a `WHERE` clause.                      
Add a second query after your first one that adds the following `WHERE` clause and condition:
```sql
WHERE online.id IS NULL
```
This will select rows where there was no corresponding row from the `online` table.
```sql
SELECT *
FROM newspaper
LEFT JOIN online
  ON newspaper.id = online.id;

  SELECT *
FROM newspaper
LEFT JOIN online
  ON newspaper.id = online.id
  WHERE online.id IS NULL;
```
### 🟩Output
```SQL
id_1     first_name_1  last_name_1   email_1                        start_month_1  end_month_1   id_2    first_name_2  last_name_2    email_2                        start_month_2  end_month_2
21253    Vinnie        Sagaser       Vinnie.Sagaser@yoohoo.com       1              5            21253    Vinnie        Sagaser       Vinnie.Sagaser@yoohoo.com       1              5
39075    Francesco     Maddron       FrancescoMaddron81@gsnail.com   1              5            39075    Francesco     Maddron       FrancescoMaddron81@gsnail.com   1              5
30648    Hellen        Broadwater    HBroadwater1992@gsnail.com      2              3            30648    Hellen        Broadwater    HBroadwater1992@gsnail.com      2              3
71778    Ouida         Pardini       Ouida.Pardini@gsnail.com        2              6            NULL     NULL          NULL           NULL                          NULL           NULL
32436    Wenona        Tankson       WTankson1989@gsnail.com         2              6            32436    Wenona        Tankson       WTankson1989@gsnail.com         2              6
55580    Clora         Werking       CWerking1996@gsnail.com         2              5            55580    Clora         Werking       CWerking1996@gsnail.com         2              5
79652    Esteban       Pitner        Esteban.Pitner@gsnail.com       2              4            NULL     NULL          NULL           NULL                          NULL           NULL
11322    Carmel        Deasis        CD3012@gsnail.com               2              6            11322    Carmel        Deasis        CD3012@gsnail.com               2              6
73893    Jessi         Vinson        JessiVinson65@gsnail.com        2              6            73893    Jessi         Vinson        JessiVinson65@gsnail.com        2              6
84750    Ayana         Hodapp        AHodapp1976@coldmail.com        3              6            84750    Ayana         Hodapp        AHodapp1976@coldmail.com        3              6
34187    Francoise     Feliberty     FFeliberty1984@inlook.com       3              7            34187    Francoise     Feliberty     FFeliberty1984@inlook.com       3              7
82566    Dusty         Morrical      DMorrical1977@gsnail.com        3              7            82566    Dusty         Morrical      DMorrical1977@gsnail.com        3              7
31446    Collin        Dobos         CollinDobos57@coldmail.com      3              5            31446    Collin        Dobos         CollinDobos57@coldmail.com      3              5
23496    Fredia        Bi            Fredia.Bi@gsnail.com            4              8            23496    Fredia        Bi            Fredia.Bi@gsnail.com            4              8
34664    Troy          Underwood     Troy.Underwood@gsnail.com       4              6            34664    Troy          Underwood     Troy.Underwood@gsnail.com       4              6
58869    Cordia        Schingeck     CordiaSchingeck82@gsnail.com    4              6            58869    Cordia        Schingeck     CordiaSchingeck82@gsnail.com    4              6
96977    Peter         Haddaway      Peter.Haddaway@gsnail.com       4              8            96977    Peter         Haddaway      Peter.Haddaway@gsnail.com       4              8
17873    Vilma         Colaizzi      VColaizzi1973@gsnail.com        4              5            17873    Vilma         Colaizzi      VColaizzi1973@gsnail.com        4              5
49633    Lane          Dittman       LaneDittman80@gsnail.com        5              9            49633    Lane          Dittman       LaneDittman80@gsnail.com        5              9
37471    Sharice       Mcmindes      SM2234@gsnail.com               5              6            37471    Sharice       Mcmindes      SM2234@gsnail.com               5              6
14227    Grady         Antinore      Grady.Antinore@gsnail.com       5              7            14227    Grady         Antinore      Grady.Antinore@gsnail.com       5              7
90240    Mandy         Ferber        Mandy.Ferber@gsnail.com         5              9            90240    Mandy         Ferber        Mandy.Ferber@gsnail.com         5              9
22237    Olimpia       Padden        OP5814@inlook.com               5              6            22237    Olimpia       Padden        OP5814@inlook.com               5              6
84308    Mechelle      Mcgarrell     MM4920@gsnail.com               5              6            84308    Mechelle      Mcgarrell     MM4920@gsnail.com               5              6
46343    Cecelia       Filipponi     CFilipponi1977@gsnail.com       5              8            NULL     NULL          NULL           NULL                           NULL           NULL
17951    Latasha       Pasket        Latasha.Pasket@gsnail.com       5              6            17951    Latasha       Pasket        Latasha.Pasket@gsnail.com       5              6
32353    Nichole       Vogenthaler   NicholeVogenthaler58@gsnail.com 5              6            32353    Nichole       Vogenthaler   NicholeVogenthaler58@gsnail.com 5              6
59400    Hiedi         Dwight        Hiedi.Dwight@gsnail.com         5              6            59400    Hiedi         Dwight        Hiedi.Dwight@gsnail.com         5              6
12575    Loni          Manchester    LoniManchester25@gsnail.com     5              8            12575    Loni          Manchester     LoniManchester25@gsnail.com    5              8
56665    Maple         Yonts         MY2659@coldmail.com             6              8            56665    Maple         Yonts         MY2659@coldmail.com             6              8
58002    Brooke        Tandetzke     BT7427@gsnail.com               6              7            NULL     NULL          NULL           NULL                           NULL           NULL    |

id_1     first_name_1  last_name_1   email_1                        start_month_1  end_month_1   id_2  first_name_2  last_name_2   email_2 start_month_2  end_month_2
71778    Ouida         Pardini       Ouida.Pardini@gsnail.com        2              6            NULL   NULL          NULL          NULL     NULL           NULL
79652    Esteban       Pitner        Esteban.Pitner@gsnail.com       2              4            NULL   NULL          NULL          NULL     NULL           NULL
46343    Cecelia       Filipponi     CFilipponi1977@gsnail.com       5              8            NULL   NULL          NULL          NULL     NULL           NULL
58002    Brooke        Tandetzke     BT7427@gsnail.com               6              7            NULL   NULL          NULL          NULL     NULL           NULL
71091    Michael       Saffer        MSaffer1989@inlook.com          6              7            NULL   NULL          NULL          NULL     NULL           NULL
86812    Dong          Mckendree     Dong.Mckendree@inlook.com       8              10           NULL   NULL          NULL          NULL     NULL           NULL
44022    Adeline       Hazinski      AHazinski1991@inlook.com        8              12           NULL   NULL          NULL          NULL     NULL           NULL
19136    Vernetta      Manda         VernettaManda60@coldmail.com    8              10           NULL   NULL          NULL          NULL     NULL           NULL
48666    Shona         Lyssy         Shona.Lyssy@gsnail.com          9              12           NULL   NULL          NULL          NULL     NULL           NULL
85799    Vicenta       Bousley       Vicenta.Bousley@gsnail.com      11             12           NULL   NULL          NULL          NULL     NULL           NULL

```
# Primary Key vs Foreign Key
Let’s return to our example of the magazine subscriptions. Recall that we had three tables: `orders`, `subscriptions`, and `customers`.

Each of these tables has a column that uniquely identifies each row of that table:                  
* `order_id` for `orders`
* `subscription_id` for `subscriptions`
* `customer_id` for `customers`

These special columns are called **primary keys**.

# PRIMARY KEYS
The `PRIMARY KEY` constraint is a fundamental database constraint that uniquely identifies each record in a table. It serves as the main identifier for rows and ensures data integrity by preventing duplicate records and null values in the specified column or columns. It combines the functionality of both `NOT NULL` and `UNIQUE` constraints, making it essential for maintaining data consistency and establishing relationships between tables.

`PRIMARY KEY` constraints are used extensively in database design for creating unique identifiers, establishing table relationships through foreign keys, enabling efficient data retrieval through automatic indexing, and maintaining referential integrity across related tables. They are commonly implemented in user management systems for unique user IDs, inventory systems for product identification, order processing systems for transaction tracking, and any scenario where each record must be uniquely identifiable and accessible.

Primary keys have a few requirements:

* None of the values can be `NULL`.                                                      
* Each value must be unique (i.e., you can’t have two customers with the same `customer_id` in the `customers` table).    
* A table can not have more than one primary key column.

Let’s reexamine the orders table:
![Screenshot 2025-06-29 222912](https://github.com/user-attachments/assets/4061dbb4-43f2-4f25-a0d5-3e0797625da2)

Note that `customer_id` (the primary key for `customers`) and `subscription_id` (the primary key for `subscriptions`) both appear in this.

When the primary key for one table appears in a different table, it is called a **foreign key**.

So `customer_id` is a primary key when it appears in `customers`, but a `foreign key` when it appears in `orders`.

In this example, our primary keys all had somewhat descriptive names. Generally, the primary key will just be called `id`. Foreign keys will have more descriptive names.

Why is this important? The most common types of joins will be joining a foreign key from one table with the primary key from another table. For instance, when we join `orders` and `customers`, we join on `customer_id`, which is a foreign key in `orders` and the primary key in `customers`.

**(1.)** Suppose Columbia University has two tables in their database:

* The `classes` table contains information on the classes that the school offers. Its primary key is `id`.
* The `students` table contains information on all students in the school. Its primary key is `id`. It contains the foreign key `class_id`, which corresponds to the primary key of `classes`.
* Perform an inner join of `classes` and `students` using the primary and foreign keys described above, and select all the columns.
```SQL
SELECT *
FROM classes
JOIN students
  ON classes.id = students.class_id;
```
### 🟩Output
```sql
class_id  description              weeks  enrollment_cap  student_id  first_name  last_name     email
1         Intro to Javascript      10     30              11752       Arnita      Castera       AC2289@gsnail.com
1         Intro to Javascript      10     30              21361       Flor        Rittie        FlorRittie1@gsnail.com
1         Intro to Javascript      10     30              24749       Aura        Longin        Aura.Longin@gsnail.com
1         Intro to Javascript      10     30              35699       Kazuko      Buddemeyer    Kazuko.Buddemeyer@gsnail.com
1         Intro to Javascript      10     30              38832       Minda       Oberlander    MindaOberlander44@inlook.com
1         Intro to Javascript      10     30              45985       Emelia      Shum          EShum1988@gsnail.com
1         Intro to Javascript      10     30              48447       Edwin       Voigtlander   EdwinVoigtlander24@gsnail.com
1         Intro to Javascript      10     30              53042       Lidia       Ashfield      LidiaAshfield31@gsnail.com
1         Intro to Javascript      10     30              54061       Eric        Ximenez       EXimenez1990@inlook.com
1         Intro to Javascript      10     30              68193       Marci       Jenness       MJenness1999@gsnail.com
1         Intro to Javascript      10     30              70627       Jack        Haney         Jack.Haney@coldmail.com
1         Intro to Javascript      10     30              82898       Patrick     Barbella      PB9978@gsnail.com
1         Intro to Javascript      10     30              86095       Kelly       Dabadie       Kelly.Dabadie@inlook.com
2         Intro to Python          12     35              33442       Malika      Giannetti     Malika.Giannetti@gsnail.com
2         Intro to Python          12     35              47189       Cammy       Aden          CA4745@gsnail.com
2         Intro to Python          12     35              52156       Arcelia     Rendler       ArceliaRendler75@gsnail.com
2         Intro to Python          12     35              82591       Collen      Margis        CMargis1980@gsnail.com
2         Intro to Python          12     35              92215       Aurora      Flavors       AuroraFlavors39@gsnail.com
3         Intermediate SQL         8      32              10442       Fern        Buchbinder    FBuchbinder1982@gsnail.com
3         Intermediate SQL         8      32              17547       Angela      Kimber        Angela.Kimber@gsnail.com
3         Intermediate SQL         8      32              30226       Meghann     Mortland      MeghannMortland40@gsnail.com
3         Intermediate SQL         8      32              48361       Maricela    Haith         MHaith1990@gsnail.com
3         Intermediate SQL         8      32              51370       Penelope    Skemp         Penelope.Skemp@gsnail.com
3         Intermediate SQL         8      32              53818       Breana      Pree          Breana.Pree@coldmail.com
3         Intermediate SQL         8      32              74262       Berry       Bartelson     Berry.Bartelson@gsnail.com
3         Intermediate SQL         8      32              76849       Faustina    Marchello     FM9997@gsnail.com
3         Intermediate SQL         8      32              76884       Clare       Lauretta      CL9794@gsnail.com
3         Intermediate SQL         8      32              78983       Maura       Bynoe         MauraBynoe51@gsnail.com
3         Intermediate SQL         8      32              91373       Freddie     Cherwinski    Freddie.Cherwinski@gsnail.com
3         Intermediate SQL         8      32              95241       Gisele      Bethea        Gisele.Bethea@gsnail.com
4         D3-js for Beginners      6      35              12572       Maynard     Gunia         MG8854@gsnail.com
4         D3-js for Beginners      6      35              14847       Tangela     Sadorra       TSadorra1974@gsnail.com
4         D3-js for Beginners      6      35              19006       Cristi      Funderburk    CFunderburk1988@coldmail.com
4         D3-js for Beginners      6      35              22097       Loria       Bordon        LBordon1990@gsnail.com
4         D3-js for Beginners      6      35              25862       Larita      Wadden        LW6686@gsnail.com
4         D3-js for Beginners      6      35              26320       Lucille     Delongis      Lucille.Delongis@gsnail.com
4         D3-js for Beginners      6      35              42490       Tillie      Brinlee       TillieBrinlee10@gsnail.com
4         D3-js for Beginners      6      35              52074       Lanny       Doop          Lanny.Doop@gsnail.com
4         D3-js for Beginners      6      35              55867       Adrien      Siggins       ASiggins1999@gsnail.com
4         D3-js for Beginners      6      35              57470       Jefferey    Gribbins      JeffereyGribbins97@gsnail.com
4         D3-js for Beginners      6      35              60546       Dorthea     Breeding      DBreeding1990@gsnail.com
4         D3-js for Beginners      6      35              61559       Leigha      Mani          LM1846@gsnail.com
4         D3-js for Beginners      6      35              67047       Pearlie     Palomar       PP7361@gsnail.com
4         D3-js for Beginners      6      35              71067       Celinda     Lummis        CLummis1990@gsnail.com
4         D3-js for Beginners      6      35              86455       Delmer      Knightly      DKnightly1972@yoohoo.com
4         D3-js for Beginners      6      35              87158       Kala        Hathorne      KalaHathorne20@gsnail.com
4         D3-js for Beginners      6      35              88153       Cleo        Delaurie      CD5205@gsnail.com
4         D3-js for Beginners      6      35              91494       Ali         Roskop        AR5364@gsnail.com
4         D3-js for Beginners      6      35              96009       Kirstin     Kahre         KKahre1981@gsnail.com
4         D3-js for Beginners      6      35              99176       Heike       Granado       HGranado1971@gsnail.com
```
* `classes.id` (a primary key)
* `students.class_id` (a foreign key)
* You should already know how to do this join. But in this exercise, you learned that the matching column is usually a primary key of a table and foreign key of another!

# Cross Join
So far, we’ve focused on matching rows that have some information in common.

Sometimes, we just want to combine all rows of one table with all rows of another table.

For instance, if we had a table of `shirts` and a table of `pants`, we might want to know all the possible combinations to create different outfits.

Our code might look like this:
```sql
SELECT shirts.shirt_color,
   pants.pants_color
FROM shirts
CROSS JOIN pants;
```
* The first two lines select the columns `shirt_color` and `pants_color`.
* The third line pulls data from the table `shirts`.
* The fourth line performs a `CROSS JOIN` with `pants`.

Notice that cross joins don’t require an ON statement. You’re not really joining on any columns!

If we have 3 different shirts (white, grey, and olive) and 2 different pants (light denim and black), the results might look like this:

<img width="269" alt="image" src="https://github.com/user-attachments/assets/22934ae7-808d-4656-8193-12935ace2c1b" />

3 shirts × 2 pants = 6 combinations!

This clothing example is fun, but it’s not very practically useful.

A more common usage of `CROSS JOIN` is when we need to compare each row of a table to a list of values.

Let’s return to our `newspaper` subscriptions. This table contains two columns that we haven’t discussed yet:

* `start_month`: the first month where the customer subscribed to the print newspaper (e.g., `2` for February)
* `end_month`: the final month where the customer subscribed to the print newspaper.

Suppose we wanted to know how many users were subscribed during each month of the year. For each month (`1`, `2`, `3`) we would need to know if a user was subscribed. Follow the steps below to see how we can use a `CROSS JOIN` to solve this problem.

**(1.)** Eventually, we’ll use a cross join to help us, but first, let’s try a simpler problem.             
Let’s start by counting the number of customers who were subscribed to the `newspaper` during March.           
Use `COUNT(*)` to count the number of rows and a `WHERE` clause to restrict to two conditions:                     
* `start_month <= 3`
* `end_month >= 3`
```sql
SELECT COUNT(*)
FROM newspaper
WHERE start_month <= 3 
  AND end_month >= 3;
```
📝 “During March” means that the customer’s starting month was in or before March and final month was in or after March:

### 🟩Output
```sql
 COUNT(*)
------------
    13
```
**(2.)** Don’t remove the previous query.                                       
The previous query lets us investigate one month at a time. In order to check across all months, we’re going to need to use a cross join.                                              
Our database contains another table called `months` which contains the numbers between 1 and 12.                
Select all columns from the cross join of `newspaper` and `months`.
```sql
SELECT COUNT(*) FROM newspaper
WHERE start_month <= 3 AND end_month >= 3;

select * FROM newspaper
CROSS JOIN months;
```
### 🟩Output
```sql
 COUNT(*)
------------
    13

id     | first_name | last_name      | email                          | start_month | end_month | month
-------|------------|----------------|--------------------------------|--------------|-----------|-------
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 1
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 2
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 3
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 4
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 5
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 6
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 7
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 8
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 9
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 10
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 11
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 12
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 1
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 2
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 3
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 4
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 5
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 6
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 7
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 8
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 9
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 10
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 11
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 12
30648  | Hellen     | Broadwater     | HBroadwater1992@gsnail.com     | 2            | 3         | 1
30648  | Hellen     | Broadwater     | HBroadwater1992@gsnail.com     | 2            | 3         | 2
30648  | Hellen     | Broadwater     | HBroadwater1992@gsnail.com     | 2            | 3         | 3
...
```
**(3.)** Don’t remove your previous queries.                                         
Create a third query where you add a `WHERE` statement to your cross join to restrict to two conditions:     
* `start_month <= month`                                                           
* `end_month >= month`
This will select all months where a user was subscribed.
```sql
SELECT COUNT(*) FROM newspaper
WHERE start_month <= 3 AND end_month >= 3;

select * FROM newspaper
CROSS JOIN months;

select * FROM newspaper
CROSS JOIN months
WHERE start_month <= month AND end_month >= month;
```
### 🟩Output
```sql
 COUNT(*)
------------
    13

id     | first_name | last_name      | email                          | start_month | end_month | month
-------|------------|----------------|--------------------------------|--------------|-----------|-------
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 1
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 2
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 3
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 4
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 5
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 6
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 7
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 8
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 9
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 10
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 11
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 12
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 1
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 2
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 3
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 4
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 5
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 6
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 7
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 8
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 9
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 10
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 11
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 12
30648  | Hellen     | Broadwater     | HBroadwater1992@gsnail.com     | 2            | 3         | 1
30648  | Hellen     | Broadwater     | HBroadwater1992@gsnail.com     | 2            | 3         | 2
30648  | Hellen     | Broadwater     | HBroadwater1992@gsnail.com     | 2            | 3         | 3
...

id     | first_name | last_name     | email                          | start_month | end_month | month
-------|------------|---------------|--------------------------------|-------------|-----------|-------
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 1
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 2
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 3
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 4
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 5
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 1
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 2
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 3
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 4
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 5
30648  | Hellen     | Broadwater    | HBroadwater1992@gsnail.com     | 2           | 3         | 2
30648  | Hellen     | Broadwater    | HBroadwater1992@gsnail.com     | 2           | 3         | 3
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 2
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 3
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 4
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 5
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 6
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 2
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 3
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 4
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 5
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 6
55580  | Clora      | Werking       | CWerking1996@gsnail.com        | 2           | 5         | 2
55580  | Clora      | Werking       | CWerking1996@gsnail.com        | 2           | 5         | 3
55580  | Clora      | Werking       | CWerking1996@gsnail.com        | 2           | 5         | 4
55580  | Clora      | Werking       | CWerking1996@gsnail.com        | 2           | 5         | 5
79652  | Esteban    | Pitner        | Esteban.Pitner@gsnail.com      | 2           | 4         | 2
79652  | Esteban    | Pitner        | Esteban.Pitner@gsnail.com      | 2           | 4         | 3
79652  | Esteban    | Pitner        | Esteban.Pitner@gsnail.com      | 2           | 4         | 4
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 2
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 3
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 4
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 5
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 6
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 2
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 3
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 4
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 5
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 6
84750  | Ayana      | Hodapp        | AHodapp1976@coldmail.com       | 3           | 6         | 3
84750  | Ayana      | Hodapp        | AHodapp1976@coldmail.com       | 3           | 6         | 4
84750  | Ayana      | Hodapp        | AHodapp1976@coldmail.com       | 3           | 6         | 5
84750  | Ayana      | Hodapp        | AHodapp1976@coldmail.com       | 3           | 6         | 6
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 3
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 4
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 5
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 6
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 7
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 3
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 4
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 5
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 6
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 7
31446  | Collin     | Dobos         | CollinDobos57@coldmail.com     | 3           | 5         | 3
31446  | Collin     | Dobos         | CollinDobos57@coldmail.com     | 3           | 5         | 4
31446  | Collin     | Dobos         | CollinDobos57@coldmail.com     | 3           | 5         | 5
```
**(4.)** Don’t remove your previous queries.                                   
Create a final query where you aggregate over each month to count the number of subscribers.                    
Fill in the blanks in the following query:
```sql
SELECT month,
  COUNT(*)
FROM ________
CROSS JOIN ________
WHERE ________ AND ________
GROUP BY ________;
```
```sql
SELECT COUNT(*) FROM newspaper
WHERE start_month <= 3 AND end_month >= 3;

select * FROM newspaper
CROSS JOIN months;

select * FROM newspaper
CROSS JOIN months
WHERE start_month <= month AND end_month >= month;

SELECT month,
   COUNT(*) AS 'subscribers'
FROM newspaper
CROSS JOIN months
WHERE start_month <= month 
   AND end_month >= month
GROUP BY month;
```
### 🟩Output
```sql
 COUNT(*)
------------
    13

id     | first_name | last_name      | email                          | start_month | end_month | month
-------|------------|----------------|--------------------------------|--------------|-----------|-------
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 1
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 2
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 3
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 4
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 5
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 6
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 7
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 8
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 9
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 10
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 11
21253  | Vinnie     | Sagaser        | Vinnie.Sagaser@yoohoo.com      | 1            | 5         | 12
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 1
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 2
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 3
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 4
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 5
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 6
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 7
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 8
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 9
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 10
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 11
39075  | Francesco  | Maddron        | FrancescoMaddron81@gsnail.com  | 1            | 5         | 12
30648  | Hellen     | Broadwater     | HBroadwater1992@gsnail.com     | 2            | 3         | 1
30648  | Hellen     | Broadwater     | HBroadwater1992@gsnail.com     | 2            | 3         | 2
30648  | Hellen     | Broadwater     | HBroadwater1992@gsnail.com     | 2            | 3         | 3
...

id     | first_name | last_name     | email                          | start_month | end_month | month
-------|------------|---------------|--------------------------------|-------------|-----------|-------
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 1
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 2
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 3
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 4
21253  | Vinnie     | Sagaser       | Vinnie.Sagaser@yoohoo.com      | 1           | 5         | 5
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 1
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 2
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 3
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 4
39075  | Francesco  | Maddron       | FrancescoMaddron81@gsnail.com  | 1           | 5         | 5
30648  | Hellen     | Broadwater    | HBroadwater1992@gsnail.com     | 2           | 3         | 2
30648  | Hellen     | Broadwater    | HBroadwater1992@gsnail.com     | 2           | 3         | 3
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 2
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 3
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 4
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 5
71778  | Ouida      | Pardini       | Ouida.Pardini@gsnail.com       | 2           | 6         | 6
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 2
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 3
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 4
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 5
32436  | Wenona     | Tankson       | WTankson1989@gsnail.com        | 2           | 6         | 6
55580  | Clora      | Werking       | CWerking1996@gsnail.com        | 2           | 5         | 2
55580  | Clora      | Werking       | CWerking1996@gsnail.com        | 2           | 5         | 3
55580  | Clora      | Werking       | CWerking1996@gsnail.com        | 2           | 5         | 4
55580  | Clora      | Werking       | CWerking1996@gsnail.com        | 2           | 5         | 5
79652  | Esteban    | Pitner        | Esteban.Pitner@gsnail.com      | 2           | 4         | 2
79652  | Esteban    | Pitner        | Esteban.Pitner@gsnail.com      | 2           | 4         | 3
79652  | Esteban    | Pitner        | Esteban.Pitner@gsnail.com      | 2           | 4         | 4
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 2
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 3
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 4
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 5
11322  | Carmel     | Deasis        | CD3012@gsnail.com              | 2           | 6         | 6
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 2
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 3
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 4
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 5
73893  | Jessi      | Vinson        | JessiVinson65@gsnail.com       | 2           | 6         | 6
84750  | Ayana      | Hodapp        | AHodapp1976@coldmail.com       | 3           | 6         | 3
84750  | Ayana      | Hodapp        | AHodapp1976@coldmail.com       | 3           | 6         | 4
84750  | Ayana      | Hodapp        | AHodapp1976@coldmail.com       | 3           | 6         | 5
84750  | Ayana      | Hodapp        | AHodapp1976@coldmail.com       | 3           | 6         | 6
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 3
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 4
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 5
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 6
34187  | Francoise  | Feliberty     | FFeliberty1984@inlook.com      | 3           | 7         | 7
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 3
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 4
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 5
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 6
82566  | Dusty      | Morrical      | DMorrical1977@gsnail.com       | 3           | 7         | 7
31446  | Collin     | Dobos         | CollinDobos57@coldmail.com     | 3           | 5         | 3
31446  | Collin     | Dobos         | CollinDobos57@coldmail.com     | 3           | 5         | 4
31446  | Collin     | Dobos         | CollinDobos57@coldmail.com     | 3           | 5         | 5

month | subscribers
-------------------
1     | 2
2     | 9
3     | 13
4     | 17
5     | 27
6     | 30
7     | 20
8     | 22
9     | 21
10    | 19
11    | 15
12    | 10
```
# Union
Sometimes we just want to stack one dataset on top of the other. Well, the `UNION` operator allows us to do that.

Suppose we have two tables and they have the same columns.

`table1:`
<img width="269" alt="image" src="https://github.com/user-attachments/assets/48c28bd2-f44a-4c6f-a1fc-52a140e8285a" />

`table2:`
<img width="271" alt="image" src="https://github.com/user-attachments/assets/d938b500-4c0d-4796-92fd-b70ddc22ab97" />

If we combine these two with `UNION`:
```sql
SELECT *
FROM table1
UNION
SELECT *
FROM table2;
```
The result would be:
<img width="269" alt="image" src="https://github.com/user-attachments/assets/693cac38-7f47-4345-acf5-28cdf1aa8ed8" />

SQL has strict rules for appending data:

* Tables must have the same number of columns.
* The columns must have the same data types in the same order as the first table.

**(1.)** Let’s return to our `newspaper` and `online` subscriptions. We’d like to create one big table with both sets of data.Use `UNION` to stack the `newspaper` table on top of the `online` table.
```sql
SELECT * 
FROM newspaper 
UNION 
SELECT * 
FROM online;
```
### 🟩Output
```sql
id      first_name  last_name   email                           start_month  end_month  month
11322   Carmel      Deasis      CD3012@gsnail.com               2            6          2
11322   Carmel      Deasis      CD3012@gsnail.com               2            6          3
11322   Carmel      Deasis      CD3012@gsnail.com               2            6          4
11322   Carmel      Deasis      CD3012@gsnail.com               2            6          5
11322   Carmel      Deasis      CD3012@gsnail.com               2            6          6
11660   Layne       Tavella     LayneTavella12@coldmail.com     8            9          8
11660   Layne       Tavella     LayneTavella12@coldmail.com     8            9          9
12575   Loni        Manchester  LoniManchester25@gsnail.com     5            8          5
12575   Loni        Manchester  LoniManchester25@gsnail.com     5            8          6
12575   Loni        Manchester  LoniManchester25@gsnail.com     5            8          7
12575   Loni        Manchester  LoniManchester25@gsnail.com     5            8          8
12770   Yer         Carpio      YerCarpio49@coldmail.com        1            4          1
12770   Yer         Carpio      YerCarpio49@coldmail.com        1            4          2
12770   Yer         Carpio      YerCarpio49@coldmail.com        1            4          3
12770   Yer         Carpio      YerCarpio49@coldmail.com        1            4          4
14022   Elisabeth   Fredeen     EF3903@gsnail.com               10           11         10
14022   Elisabeth   Fredeen     EF3903@gsnail.com               10           11         11
14227   Grady       Antinore    Grady.Antinore@gsnail.com       5            7          5
14227   Grady       Antinore    Grady.Antinore@gsnail.com       5            7          6
14227   Grady       Antinore    Grady.Antinore@gsnail.com       5            7          7
```
# With
Often times, we want to combine two tables, but one of the tables is the result of another calculation.

Let’s return to our magazine order example. Our marketing department might want to know a bit more about our customers. For instance, they might want to know how many magazines each customer subscribes to. We can easily calculate this using our `orders` table:
```sql
SELECT customer_id,
   COUNT(subscription_id) AS 'subscriptions'
FROM orders
GROUP BY customer_id;
```
This query is good, but a `customer_id` isn’t terribly useful for our marketing department, they probably want to know the customer’s name.

We want to be able to join the results of this query with our `customers` table, which will tell us the name of each customer. We can do this by using a `WITH` clause.
```sql
WITH previous_results AS (
   SELECT ...
   ...
   ...
   ...
)
SELECT *
FROM previous_results
JOIN customers
  ON _____ = _____;
```
* The `WITH` statement allows us to perform a separate query (such as aggregating customer’s subscriptions)
* `previous_results` is the alias that we will use to reference any columns from the query inside of the `WITH` clause
* We can then go on to do whatever we want with this temporary table (such as join the temporary table with another table)

Essentially, we are putting a whole first query inside the parentheses `()` and giving it a name. After that, we can use this name as if it’s a table and write a new query using the first query.

**(1.)** Place the whole query below into a `WITH` statement, inside parentheses `()`, and give it name `previous_query`:
```sql
SELECT customer_id,
   COUNT(subscription_id) AS 'subscriptions'
FROM orders
GROUP BY customer_id
```
Join the temporary table `previous_query` with `customers` table and select the following columns:

* `customers.customer_name`
* `previous_query.subscriptions`

Check the answer in the hint below.
```sql
WITH previous_query AS (
   SELECT customer_id,
      COUNT(subscription_id) AS 'subscriptions'
   FROM orders
   GROUP BY customer_id
)
SELECT customers.customer_name, 
   previous_query.subscriptions
FROM previous_query
JOIN customers
  ON previous_query.customer_id = customers.customer_id;
```
### 🟩Output
```sql
customer_name        subscriptions
Allie Rahaim         4
Jacquline Diddle     1
Lizabeth Letsche     6
Jessia Butman        2
Inocencia Goyco      2
Bethann Schraub      1
Janay Priolo         1
Ophelia Sturdnant    1
Eryn Vilar           2
```
* Remember to use the following `ON` statement as part of your `JOIN`.

* And for review, `AS` is how you give something an alias.

* Here, we are essentially giving everything inside the parentheses (the sub-query) the name of `previous_query` using `AS`.

* Then, `previous_query` is used as a temporary table that we will query from and also join with the `customers` table.

📝 Do not include `;` inside of the `()` of your `WITH` statement.

