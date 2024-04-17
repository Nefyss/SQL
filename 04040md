SQL
## Task 00
### Let’s make a simple aggregation, please write a SQL statement that returns person identifiers and corresponding number of visits in any pizzerias and sorting by count of visits in descending mode and sorting in person_id in ascending mode. Please take a look at the sample of data below.
```
SELECT pv.person_id, COUNT(pv.id) as visit_count
FROM person_visits pv
GROUP BY pv.person_id
ORDER BY visit_count DESC, pv.person_id ASC;
```
![image](https://github.com/Nefyss/SQL/assets/113514047/aaac1438-48cd-4303-979e-576f5e4741ac)

## Task 01
### Please change a SQL statement from Exercise 00 and return a person name (not identifier). Additional clause is we need to see only top-4 persons with maximal visits in any pizzerias and sorted by a person name. Please take a look at the example of output data below.
```
SELECT p.name as user_name, COUNT(pv.id) as visit_count
FROM person_visits pv
JOIN person p ON pv.person_id = p.id
GROUP BY pv.person_id, p.name
ORDER BY visit_count DESC, p.name ASC
LIMIT 4;
```
![image](https://github.com/Nefyss/SQL/assets/113514047/ef1b7fc3-eae3-4c8a-bd13-87b86ae5a306)

## Task 02
### Please write a SQL statement to see 3 favorite restaurants by visits and by orders in one list (please add an action_type column with values ‘order’ or ‘visit’, it depends on data from the corresponding table). Please take a look at the sample of data below. The result should be sorted by action_type column in ascending mode and by count column in descending mode.
```
SELECT p.id as count, pz.name as name, 'visit' as action_type
FROM person_visits pv
JOIN person p ON pv.person_id = p.id
JOIN pizzeria pz ON pv.pizzeria_id = pz.id
UNION 
SELECT p.id as count, pz.name as name, 'order' as action_type
FROM person_order po
JOIN person p ON po.person_id = p.id
JOIN menu m ON po.menu_id = m.id
JOIN pizzeria pz ON m.pizzeria_id = pz.id
ORDER BY count, action_type;
```
![image](https://github.com/Nefyss/SQL/assets/113514047/856f8a1f-3d6c-48df-be52-390a6468c8b7)

## Task 03
### Please write a SQL statement to see restaurants are grouping by visits and by orders and joined with each other by using restaurant name. You can use internal SQLs from Exercise 02 (restaurants by visits and by orders) without limitations of amount of rows.
```

```
## Task 04
### Please write a SQL statement that returns the person name and corresponding number of visits in any pizzerias if the person has visited more than 3 times (> 3).Please take a look at the sample of data below.
```

```
## Task 05
### Please write a simple SQL query that returns a list of unique person names who made orders in any pizzerias. The result should be sorted by person name. Please take a look at the sample below.
```

```
## Task 06
### Please write a SQL statement that returns the amount of orders, average of price, maximum and minimum prices for sold pizza by corresponding pizzeria restaurant. The result should be sorted by pizzeria name. Please take a look at the data sample below. Round your average price to 2 floating numbers.
```

```
## Task 07
### Please write a SQL statement that returns a common average rating (the output attribute name is global_rating) for all restaurants. Round your average rating to 4 floating numbers.
```

```
## Task 08 
### We know about personal addresses from our data. Let’s imagine, that particular person visits pizzerias in his/her city only. Please write a SQL statement that returns address, pizzeria name and amount of persons’ orders. The result should be sorted by address and then by restaurant name. Please take a look at the sample of output data below.
```

```
## Task 09
### Please write a SQL statement that returns aggregated information by person’s address , the result of “Maximal Age - (Minimal Age / Maximal Age)” that is presented as a formula column, next one is average age per address and the result of comparison between formula and average columns (other words, if formula is greater than average then True, otherwise False value).
```

```
