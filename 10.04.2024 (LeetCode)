SQL
## 175
### Write a solution to report the first name, last name, city, and state of each person in the Person table. If the address of a personId is not present in the Address table, report null instead. Return the result table in any order. The result format is in the following example.
```
SELECT p.firstName, p.lastName, a.city, a.state
FROM Person p 
LEFT JOIN Address a ON p.personId = a.personId
```

## 176
### Write a solution to find the second highest salary from the Employee table. If there is no second highest salary, return null (return None in Pandas).
```
SELECT MAX(salary) AS SecondHighestSalary
FROM Employee
WHERE salary < (SELECT MAX(salary) FROM Employee);
```

## 177
### Write a solution to find the nth highest salary from the Employee table. If there is no nth highest salary, return null.
```
CREATE OR REPLACE FUNCTION NthHighestSalary(N INT) RETURNS TABLE (Salary INT) AS $$
BEGIN
  RETURN QUERY (
  SELECT DISTINCT tab.salary FROM (
	    SELECT DENSE_RANK() OVER(ORDER BY e.salary desc) AS getNthHighestSalary, e.* FROM Employee e
    ) as tab
    WHERE getNthHighestSalary = N
  );
END;
$$ LANGUAGE plpgsql;
```

## 178
### Write a solution to find the rank of the scores. The ranking should be calculated according to the following rules:
The scores should be ranked from the highest to the lowest.
If there is a tie between two scores, both should have the same ranking.
After a tie, the next ranking number should be the next consecutive integer value. In other words, there should be no holes between ranks.
Return the result table ordered by score in descending order.
```
SELECT s.score, DENSE_RANK() OVER(ORDER BY score desc) AS rank FROM Scores s
```

## 181
### Write a solution to find the employees who earn more than their managers. Return the result table in any order.
```
SELECT a.Name AS Employee
FROM Employee a JOIN Employee b on a.ManagerId = b.Id
WHERE a.Salary > b.Salary
```

## 182
### Write a solution to report all the duplicate emails. Note that it's guaranteed that the email field is not NULL. Return the result table in any order.
```
SELECT email FROM person
GROUP BY email
HAVING COUNT(email) > 1
```

## 262
### The cancellation rate is computed by dividing the number of canceled (by client or driver) requests with unbanned users by the total number of requests with unbanned users on that day. Write a solution to find the cancellation rate of requests with unbanned users (both client and driver must not be banned) each day between "2013-10-01" and "2013-10-03". Round Cancellation Rate to two decimal points. Return the result table in any order.
```
WITH twb AS(
    SELECT request_at::date as day, status FROM trips
    WHERE client_id NOT IN (
        SELECT users_id FROM users WHERE banned = 'Yes'
    )
    AND driver_id NOT IN (
        SELECT users_id FROm users WHERE banned = 'Yes'
    )
)

SELECT
    day AS "Day",
    ROUND (CAST(COUNT(*)FILTER (WHERE status LIKE 'cancelled%') AS NUMERIC)
    /
    CAST (COUNT(*) AS NUMERIC), 2) AS "Cancellation Rate"
FROM twb
WHERE day BETWEEN '2013-10-01' AND '2013-10-03'
GROUP BY day
ORDER BY 1
```

## Game Play Analysis I
### Write a solution to find the first login date for each player. Return the result table in any order.
```
SELECT player_id, min(event_date) AS first_login FROM activity
GROUP BY player_id
```
