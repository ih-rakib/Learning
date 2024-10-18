# SQL practice problems and solution from LeetCode

1. [Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/)

```sql
SELECT product_id FROM Products WHERE low_fats = 'Y' AND recyclable = 'Y';
```

2. [Find Customer Referee](https://leetcode.com/problems/find-customer-referee/)

```sql
SELECT name FROM Customer WHERE referee_id != 2 OR referee_id IS NULL;
```

3. [Big Countries](https://leetcode.com/problems/big-countries/)

```sql
SELECT name, population, area FROM World 
WHERE population >= 25000000 OR area >= 3000000;
```

4. [Article Views I](https://leetcode.com/problems/article-views-i/)

```sql
SELECT DISTINCT author_id AS id 
FROM Views
WHERE author_id = viewer_id
ORDER BY id ASC;
```

5. [Invalid Tweets](https://leetcode.com/problems/invalid-tweets/)

```sql
SELECT tweet_id FROM Tweets
WHERE LENGTH(content) > 15;
```

6. [Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/)

```sql
SELECT unique_id, name
FROM Employees
LEFT JOIN EmployeeUNI
ON Employees.id = EmployeeUNI.id;
```

or

```sql
SELECT 
    E.unique_id, 
    E.name
FROM 
    Employees AS E
LEFT JOIN 
    EmployeeUNI AS EU ON E.id = EU.id;
```

7. [Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/)

```sql
SELECT P.product_name, S.year, S.price
FROM Product AS P
JOIN SALES AS S
ON P.product_id = S.product_id;
```

8. [Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/)

```sql
SELECT V.customer_id, COUNT(*) AS count_no_trans
FROM Visits AS V
LEFT JOIN Transactions AS T
ON V.visit_id = T.visit_id
WHERE T.visit_id IS NULL
GROUP BY V.customer_id;
```

9. [Rising Temperature](https://leetcode.com/problems/rising-temperature/)

```sql
SELECT W1.id FROM Weather AS W1
JOIN Weather AS W2
ON W1.recordDate = DATE_ADD(W2.recordDate, INTERVAL 1 DAY)
WHERE W1.temperature > W2.temperature;
```

another way(easier)

```sql
SELECT W1.id 
FROM Weather AS W1, Weather AS W2
WHERE W1.recordDate = W2.recordDate + INTERVAL 1 DAY
AND W1.temperature > W2.temperature;
```

10. [Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/)

```sql
SELECT machine_id,
    ROUND(AVG(end_time - start_time), 3) AS processing_time
FROM (
    SELECT machine_id, process_id,
        MIN(timestamp) AS start_time,
        MAX(timestamp) AS end_time
        FROM Activity
        WHERE activity_type IN ('start', 'end')
    GROUP BY machine_id, process_id
) AS time_data
WHERE start_time IS NOT NULL AND end_time IS NOT NULL
GROUP BY machine_id;
```
better

```sql
SELECT machine_id,
       ROUND(AVG(end_time - start_time), 3) AS processing_time
FROM (
    SELECT machine_id,
           process_id,
           MIN(timestamp) AS start_time,
           MAX(timestamp) AS end_time
    FROM Activity
    GROUP BY machine_id, process_id
) AS time_data
GROUP BY machine_id;
```

11. []()

```sql

```

12. []()

```sql

```
