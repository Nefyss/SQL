SQL
### 570 Managers with at Least 5 Direct Reports
## Write a solution to find managers with at least five direct reports. Return the result table in any order. 
```
SELECT name
FROM Employee
WHERE id IN (
    SELECT managerId
    FROM Employee
    WHERE managerId IS NOT NULL
    GROUP BY managerId
    HAVING COUNT(*) >= 5
);
```
## 1934. Confirmation Rate
### The confirmation rate of a user is the number of 'confirmed' messages divided by the total number of requested confirmation messages. The confirmation rate of a user that did not request any confirmation messages is 0. Round the confirmation rate to two decimal places. Write a solution to find the confirmation rate of each user. Return the result table in any order.
```
SELECT 
    s.user_id,
    IFNULL(SUM(CASE WHEN c.action = 'confirmed' THEN 1 ELSE 0 END) / COUNT(c.user_id), 0) AS confirmation_rate
FROM 
    Signups s
LEFT JOIN 
    Confirmations c ON s.user_id = c.user_id
GROUP BY 
    s.user_id;
```
## 1193. Monthly Transactions I
### Write an SQL query to find for each month and country, the number of transactions and their total amount, the number of approved transactions and their total amount. Return the result table in any order.
```
SELECT 
    DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,
    COUNT(id) AS trans_count,
    SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,
    SUM(amount) AS trans_total_amount,
    SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM 
    Transactions
GROUP BY 
    month, country;
```
## 1174. Immediate Food Delivery II
### If the customer's preferred delivery date is the same as the order date, then the order is called immediate; otherwise, it is called scheduled. The first order of a customer is the order with the earliest order date that the customer made. It is guaranteed that a customer has precisely one first order. Write a solution to find the percentage of immediate orders in the first orders of all customers, rounded to 2 decimal places.
```
SELECT ROUND((SUM(is_immediate) / COUNT(*)) * 100, 2) AS immediate_percentage
FROM (
    SELECT 
        customer_id,
        MIN(order_date) AS first_order_date,
        IF(MIN(order_date) = MIN(customer_pref_delivery_date), 1, 0) AS is_immediate
    FROM 
        Delivery
    GROUP BY 
        customer_id
) AS first_orders;
```
## 550. Game Play Analysis IV
### Write a solution to report the fraction of players that logged in again on the day after the day they first logged in, rounded to 2 decimal places. In other words, you need to count the number of players that logged in for at least two consecutive days starting from their first login date, then divide that number by the total number of players.
```
SELECT ROUND(SUM(consecutive_logins) / COUNT(DISTINCT player_id), 2) AS fraction
FROM (
    SELECT a1.player_id, 
           COUNT(a2.event_date) >= 1 AS consecutive_logins
    FROM Activity a1
    LEFT JOIN Activity a2 ON a1.player_id = a2.player_id 
                          AND DATEDIFF(a2.event_date, a1.event_date) = 1
    GROUP BY a1.player_id, a1.event_date
) AS subquery;
```
## 1070. Product Sales Analysis III
### Write a solution to select the product id, year, quantity, and price for the first year of every product sold. Return the resulting table in any order.
```
SELECT 
    product_id,
    MIN(year) AS first_year,
    quantity,
    price
FROM 
    Sales
GROUP BY 
    product_id;
```
## 1045. Customers Who Bought All Products
### Write a solution to report the customer ids from the Customer table that bought all the products in the Product table. Return the result table in any order.
```
SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(*) FROM Product);
```
## 180. Consecutive Numbers
### Find all numbers that appear at least three times consecutively. Return the result table in any order.
```
SELECT DISTINCT num AS ConsecutiveNums
FROM (
    SELECT num, 
           LAG(num, 1) OVER (ORDER BY id) AS prev_num,
           LEAD(num, 1) OVER (ORDER BY id) AS next_num
    FROM Logs
) AS subquery
WHERE num = prev_num AND num = next_num;
```
## 1164. Product Price at a Given Date
### Write a solution to find the prices of all products on 2019-08-16. Assume the price of all products before any change is 10. Return the result table in any order.
```
SELECT 
    product_id,
    COALESCE(MAX(CASE WHEN change_date <= '2019-08-16' THEN new_price END), 10) AS price
FROM 
    Products
GROUP BY 
    product_id;
```
## 1204. Last Person to Fit in the Bus
### There is a queue of people waiting to board a bus. However, the bus has a weight limit of 1000 kilograms, so there may be some people who cannot board. Write a solution to find the person_name of the last person that can fit on the bus without exceeding the weight limit. The test cases are generated such that the first person does not exceed the weight limit.
```
WITH SortedQueue AS (
    SELECT *
    FROM Queue
    ORDER BY turn
),
CumulativeWeights AS (
    SELECT 
        sq.person_id,
        sq.person_name,
        sq.weight,
        SUM(sq.weight) OVER (ORDER BY sq.turn) AS total_weight
    FROM SortedQueue sq
)
SELECT 
    c.person_name
FROM CumulativeWeights c
WHERE c.total_weight <= 1000
ORDER BY c.person_id DESC
LIMIT 1;
```
## 176. Second Highest Salary
### Write a solution to find the second highest salary from the Employee table. If there is no second highest salary, return null (return None in Pandas).
```
SELECT 
    (SELECT DISTINCT salary
     FROM Employee
     ORDER BY salary DESC
     LIMIT 1 OFFSET 1) AS SecondHighestSalary;
```
