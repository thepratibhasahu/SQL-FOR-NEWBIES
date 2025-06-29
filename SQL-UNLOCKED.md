# Introduction

In order to efficiently store data, we often spread related information across multiple tables.

For instance, imagine that we’re running a magazine company where users can have different types of subscriptions to different products. Different subscriptions might have many different properties. Each customer would also have lots of associated information.

We could have one table with all of the following information:                                                        
* order_id
* customer_id
* customer_name
* customer_address
* subscription_id
* subscription_description
* subscription_monthly_price
* subscription_length
* purchase_date

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
