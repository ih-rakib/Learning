# SQL practice problems and solution from LeetCode

1. [Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/)

```sql
SELECT product_id FROM Products WHERE low_fats = 'Y' AND recyclable = 'Y';
```
------

2. [Find Customer Referee](https://leetcode.com/problems/find-customer-referee/)

```sql
SELECT name FROM Customer WHERE referee_id != 2 OR referee_id IS NULL;
```
------

3. [Big Countries](https://leetcode.com/problems/big-countries/)

```sql
SELECT name, population, area FROM World 
WHERE population >= 25000000 OR area >= 3000000;
```
------

4. [Article Views I](https://leetcode.com/problems/article-views-i/)

```sql
SELECT DISTINCT author_id AS id 
FROM Views
WHERE author_id = viewer_id
ORDER BY id ASC;
```
------

5. [Invalid Tweets](https://leetcode.com/problems/invalid-tweets/)

```sql
SELECT tweet_id FROM Tweets
WHERE LENGTH(content) > 15;
```
------

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
------

7. [Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/)

```sql
SELECT P.product_name, S.year, S.price
FROM Product AS P
JOIN SALES AS S
ON P.product_id = S.product_id;
```
------


8. [Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/)

```sql
SELECT V.customer_id, COUNT(*) AS count_no_trans
FROM Visits AS V
LEFT JOIN Transactions AS T
ON V.visit_id = T.visit_id
WHERE T.visit_id IS NULL
GROUP BY V.customer_id;
```
------

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

------


10. [Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/)

```sql
SEL machine_id,
    ROUND(AVG(end_time - start_time), 3)ECT AS processing_time
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
------

11. [Employee Bonus](https://leetcode.com/problems/employee-bonus/)

```sql
SELECT E.name, B.bonus
FROM Employee E
LEFT JOIN Bonus B
ON E.empId = B.empId
WHERE B.bonus < 1000 OR B.empId IS NULL;
```

------

12. [Students and Examinations](https://leetcode.com/problems/students-and-examinations/)

```sql
SELECT S.student_id, S.student_name, Sub.subject_name, COALESCE(COUNT(E.student_id), 0) AS attended_exams
FROM Students S
CROSS JOIN Subjects Sub
LEFT JOIN Examinations E ON E.student_id = S.student_id AND E.subject_name = Sub.subject_name
GROUP BY S.student_id, S.student_name, Sub.subject_name
ORDER BY S.student_id, Sub.subject_name;
```

**Explanation:**

```sql
SELECT *
FROM Students;
```

| student_id | student_name |
|------------|--------------|
| 1          | Alice        |
| 2          | Bob          |
| 6          | Alex         |
| 13         | John         |


```sql
SELECT *
FROM Subjects;
```

| subject_name |
|--------------|
| Math         |
| Physics      |
| Programming  |


```sql
SELECT S.student_id, S.student_name, SUB.subject_name
FROM Students S
CROSS JOIN Subjects SUB;
```

The CROSS JOIN generates all possible combinations of students and subjects, meaning each student will be listed for each subject.

| student_id | student_name | subject_name |
|------------|--------------|--------------|
| 1          | Alice        | Math         |
| 1          | Alice        | Physics      |
| 1          | Alice        | Programming  |
| 2          | Bob          | Math         |
| 2          | Bob          | Physics      |
| 2          | Bob          | Programming  |
| 6          | Alex         | Math         |
| 6          | Alex         | Physics      |
| 6          | Alex         | Programming  |
| 13         | John         | Math         |
| 13         | John         | Physics      |
| 13         | John         | Programming  |



Next, we will use a LEFT JOIN to combine the above results with the Examinations table. This will allow us to see how many times each student attended each subject.

```sql
SELECT S.student_id, S.student_name, SUB.subject_name, E.student_id AS exam_student_id
FROM Students S
CROSS JOIN Subjects SUB
LEFT JOIN Examinations E ON S.student_id = E.student_id AND SUB.subject_name = E.subject_name;
```

| student_id | student_name | subject_name | exam_student_id  |
|------------|--------------|--------------|------------------|
| 1          | Alice        | Math         | 1                |
| 1          | Alice        | Physics      | 1                |
| 1          | Alice        | Programming  | 1                |
| 2          | Bob          | Math         | 2                |
| 2          | Bob          | Physics      | NULL             |
| 2          | Bob          | Programming  | 2                |
| 6          | Alex         | Math         | NULL             |
| 6          | Alex         | Physics      | NULL             |
| 6          | Alex         | Programming  | NULL             |
| 13         | John         | Math         | 13               |
| 13         | John         | Physics      | 13               |
| 13         | John         | Programming  | 13               |


Counting Attendance
Now, we will count how many times each student attended each subject. We will use the COUNT function and COALESCE to handle cases where there are no exams attended.

```sql
SELECT S.student_id, 
       S.student_name, 
       SUB.subject_name, 
       COALESCE(COUNT(E.student_id), 0) AS attended_exams
FROM Students S
CROSS JOIN Subjects SUB
LEFT JOIN Examinations E ON S.student_id = E.student_id AND SUB.subject_name = E.subject_name
GROUP BY S.student_id, S.student_name, SUB.subject_name;
```

| student_id | student_name | subject_name | attended_exams |
|------------|--------------|--------------|----------------|
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |


>> The COALESCE function in SQL is used to return the first non-null value in a list of arguments. It's a very useful function when you want to ensure that a result does not end up being null, especially when dealing with outer joins, where some values may be null.

```sql
COALESCE(value1, value2, ..., valueN)
```

It evaluates the values in the order they are provided.
It returns the first value that is not NULL.
Use Case in the Given Query:
In the context of the previous query, COALESCE is used to ensure that the attended_exams column does not return a NULL value when counting the number of times a student attended a particular exam.

Here’s the relevant part of the query again:

```sql
COALESCE(COUNT(E.student_id), 0) AS attended_exams
```

What it Does:
Counting Attendance:

COUNT(E.student_id) counts how many times a student attended exams for a particular subject. If the student did not attend any exams for that subject, this count would return 0.
However, if a student has never attended any exams for any subjects (which would happen in the case of LEFT JOIN), it could return NULL for that subject.

Using COALESCE:

COALESCE(COUNT(E.student_id), 0) checks the result of the count.
If the count is NULL, it replaces it with 0.
This means that instead of showing a blank or NULL value for students who have not attended any exams, it will explicitly show 0.

13. [Not Boring Movies](https://leetcode.com/problems/not-boring-movies/)

```sql
SELECT * FROM Cinema
WHERE id % 2 != 0 AND description != "boring"
ORDER BY rating DESC;
```

------

14. [ Average Selling Price](https://leetcode.com/problems/average-selling-price/)

```sql
SELECT 
    p.product_id,
    ROUND(COALESCE(SUM(u.units * p.price) / NULLIF(SUM(u.units), 0), 0), 2) AS average_price
FROM 
    Prices p
LEFT JOIN 
    UnitsSold u ON p.product_id = u.product_id 
                AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY 
    p.product_id;
```

1. **`SELECT`**: This keyword initiates the selection of data from the database.
   
   - **`p.product_id`**: This selects the `product_id` from the `Prices` table (aliased as `p`). It ensures that each product ID is included in the final result.

   - **`ROUND(COALESCE(SUM(u.units * p.price) / NULLIF(SUM(u.units), 0), 0), 2) AS average_price`**: This calculates the average price and assigns it an alias `average_price`. Let's break this down further:
     - **`SUM(u.units * p.price)`**: This computes the total revenue for each product by multiplying the number of units sold (`u.units`) by the price at which those units were sold (`p.price`). The result is summed to get the total revenue across all transactions for each product.
     - **`SUM(u.units)`**: This sums up all the units sold for each product. This is used as the denominator to calculate the average price.
     - **`NULLIF(SUM(u.units), 0)`**: This function returns `NULL` if the sum of units sold is `0`. This is important to avoid division by zero when calculating the average price. If there are no units sold, this will prevent an error and allow us to handle the average price calculation gracefully.
     - **`SUM(u.units * p.price) / NULLIF(SUM(u.units), 0)`**: This expression divides the total revenue by the total units sold. If no units are sold, it will return `NULL` (thanks to the `NULLIF` function).
     - **`COALESCE(..., 0)`**: This function checks if the result of the division is `NULL`. If it is `NULL`, it returns `0`, indicating that the average price should be considered `0` when there are no sales.
     - **`ROUND(..., 2)`**: Finally, this function rounds the average price to two decimal places for better presentation.

2. **`FROM Prices p`**: This specifies the main table we are querying from. `Prices` is aliased as `p` for easier reference throughout the query.

3. **`LEFT JOIN UnitsSold u ON p.product_id = u.product_id`**: 
   
   - **`LEFT JOIN`**: This type of join returns all records from the `Prices` table (`p`) and the matched records from the `UnitsSold` table (`u`). If there is no match, it will still return the records from `Prices` but with `NULL` values for the columns from `UnitsSold`. This is crucial because we want to include products even if they have no units sold.
   
   - **`ON p.product_id = u.product_id`**: This condition specifies how the tables are linked: by matching the `product_id` from both tables. This ensures we are combining relevant data about sales with the corresponding prices.

   - **`AND u.purchase_date BETWEEN p.start_date AND p.end_date`**: This additional condition filters the joined results to only include rows where the `purchase_date` falls within the price validity period (`start_date` to `end_date`). It ensures that only applicable prices are considered when calculating revenue.

4. **`GROUP BY p.product_id`**: This groups the results by `product_id`, which allows us to perform aggregate functions (like `SUM`) for each product. Each product will have its own row in the final result, containing the total revenue and total units sold specific to that product.

------

15. [Project Employees I](https://leetcode.com/problems/project-employees-i/)

```sql
SELECT 
    p.project_id,
    ROUND(AVG(e.experience_years), 2) AS average_years
FROM 
    Project p
JOIN 
    Employee e ON p.employee_id = e.employee_id
GROUP BY 
    p.project_id;
```
------

16. [Percentage of Users Attended a Contest](https://leetcode.com/problems/percentage-of-users-attended-a-contest/)

```sql
WITH TotalUsers AS (
    SELECT COUNT(DISTINCT user_id) AS total_users
    FROM Users
),
RegisteredUsers AS (
    SELECT contest_id, COUNT(DISTINCT user_id) AS registered_users
    FROM Register
    GROUP BY contest_id
)
SELECT 
    r.contest_id,
    ROUND((r.registered_users * 100.0) / t.total_users, 2) AS percentage
FROM 
    RegisteredUsers r
CROSS JOIN 
    TotalUsers t
ORDER BY 
    percentage DESC,
    contest_id ASC;
```

Another way:

```sql
SELECT 
    contest_id,
    ROUND((COUNT(DISTINCT user_id) * 100.0) / (SELECT COUNT(*) FROM Users), 2) AS percentage
FROM 
    Register
GROUP BY 
    contest_id
ORDER BY 
    percentage DESC, contest_id ASC;
```

**Steps:**
- Find the total number of unique users from the Users table.
- Count how many unique users registered for each contest from the Register table.
- Calculate the percentage of users who registered for each contest by dividing the number of users registered for the contest by the total number of unique users.
- Round the percentage to 2 decimal places.
- Sort the results by percentage in descending order. If there's a tie, sort by contest_id in ascending order.

**Explanation:**
- *COUNT(DISTINCT user_id)*: This counts the unique users for each contest.
- *(SELECT COUNT(*) FROM Users)*: This gets the total number of users.
- *ROUND((COUNT(DISTINCT user_id) * 100.0) / (SELECT COUNT(*) FROM Users), 2)*: This calculates the percentage of users registered for the contest and rounds it to 2 decimal places.
- *GROUP BY contest_id*: Groups the results by each contest to calculate the percentage for each contest.
- *ORDER BY percentage DESC, contest_id ASC*: Sorts the results by percentage in descending order and by contest_id in ascending order if there is a tie in the percentage.

17. [Confirmation Rate](https://leetcode.com/problems/confirmation-rate/)

```sql
SELECT 
    s.user_id,
    IFNULL(ROUND(COUNT(CASE WHEN c.action = 'confirmed' THEN 1 END) / COUNT(c.action), 2), 0.00) AS confirmation_rate
FROM 
    Signups s
LEFT JOIN 
    Confirmations c
ON 
    s.user_id = c.user_id
GROUP BY 
    s.user_id;
```

**Explanation:**
- FROM Signups s LEFT JOIN Confirmations c: We perform a LEFT JOIN between the Signups table and the Confirmations table to ensure that all users from Signups are included, even if they have no confirmation records.

- COUNT(CASE WHEN c.action = 'confirmed' THEN 1 END): This counts how many times each user had a confirmation message that was 'confirmed'.

- COUNT(c.action): This counts the total number of confirmation messages (either 'confirmed' or 'timeout') for each user.

- ROUND(..., 2): This rounds the confirmation rate to two decimal places.

- IFNULL(..., 0.00): If the user did not request any confirmation messages (i.e., COUNT(c.action) is NULL), we set the confirmation rate to 0.00.

- GROUP BY s.user_id: We group the results by user_id to calculate the confirmation rate for each user.


1. User 6: Did not request any confirmation messages, so the confirmation rate is 0.00.
2. User 3: Made 2 requests, but both timed out, so the confirmation rate is 0.00.
3. User 7: Made 3 requests and all were confirmed, so the confirmation rate is 1.00.
4. User 2: Made 2 requests, with 1 confirmed and 1 timed out, so the confirmation rate is 0.50.

------

18. [Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/)

```sql
SELECT e.name FROM Employee E
JOIN (
    SELECT managerId, COUNT(*) AS report_count FROM Employee
    WHERE managerId IS NOT NULL
    GROUP BY managerId
    HAVING report_count >= 5
) AS managers
ON e.id = managers.managerId;
```


```sql
SELECT managerId, COUNT(*) AS report_count 
FROM Employee
WHERE managerId IS NOT NULL
GROUP BY managerId
HAVING report_count >= 5
```

| managerId | report_count |
|-----------|--------------|
| 101       | 5            |


```sql
SELECT e.name 
FROM Employee E
JOIN (subquery result) AS managers
ON e.id = managers.managerId;
```

| name |
|------|
| John |

------

19. [Number of Unique Subjects Taught by Each Teacher](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/)

```sql
SELECT teacher_id, COUNT(DISTINCT subject_id) AS cnt 
FROM Teacher
GROUP BY teacher_id;
```

------


20. [User Activity for the Past 30 Days I](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/)

```sql
SELECT activity_date AS day, COUNT(DISTINCT user_id) AS active_users
FROM Activity
WHERE activity_date BETWEEN '2019-06-28' AND '2019-07-27'
GROUP BY activity_date;
```

- On 2019-07-20, two users (user 1 and user 2) were active.
- On 2019-07-21, two users (user 2 and user 3) were active.
------

21. [Queries Quality and Percentage](https://leetcode.com/problems/queries-quality-and-percentage/)

```sql
SELECT query_name,
       ROUND(AVG(rating / position), 2) AS quality,
       ROUND((SUM(rating < 3) * 100) / COUNT(*), 2) AS poor_query_percentage
FROM Queries
WHERE query_name IS NOT NULL
GROUP BY query_name;
```

------


22. [Monthly Transactions I](https://leetcode.com/problems/monthly-transactions-i/)

```sql
SELECT 
    DATE_FORMAT(trans_date, '%Y-%m') AS month,    -- Extract year and month from trans_date
    country,
    COUNT(*) AS trans_count,                      -- Total number of transactions
    SUM(state = 'approved') AS approved_count,     -- Count of approved transactions
    SUM(amount) AS trans_total_amount,            -- Total amount of all transactions
    SUM(amount * (state = 'approved')) AS approved_total_amount  -- Sum of approved transaction amounts
FROM Transactions
GROUP BY month, country;
```

------

23. [Product Sales Analysis III](https://leetcode.com/problems/product-sales-analysis-iii/)

```sql
SELECT s.product_id, s.year AS first_year, s.quantity, s.price
FROM Sales s
INNER JOIN (
    SELECT product_id, MIN(year) AS first_year
    FROM Sales
    GROUP BY product_id
) AS first_sales
ON s.product_id = first_sales.product_id AND s.year = first_sales.first_year;
```

```sql
SELECT p.product_name, s.product_id, s.year AS first_year, s.quantity, s.price
FROM Sales s
INNER JOIN (
    SELECT product_id, MIN(year) AS first_year
    FROM Sales
    GROUP BY product_id
) AS first_sales
ON s.product_id = first_sales.product_id AND s.year = first_sales.first_year
JOIN Product p
ON s.product_id = p.product_id;
```

------


24. [Classes More Than 5 Students](https://leetcode.com/problems/classes-more-than-5-students/)

```sql
SELECT class FROM Courses
GROUP BY class
HAVING COUNT(student) >= 5;
```

------

25. [Immediate Food Delivery II](https://leetcode.com/problems/immediate-food-delivery-ii/)

```sql
WITH FirstOrders AS (
    -- Create a CTE (Common Table Expression) to identify each customer's first order
    SELECT 
        customer_id,
        MIN(order_date) AS first_order_date  -- Get the earliest order date per customer
    FROM Delivery
    GROUP BY customer_id
)

SELECT 
    ROUND(
        100.0 * SUM(d.order_date = d.customer_pref_delivery_date) 
        / COUNT(*), 2  -- Calculate and round the percentage of immediate first orders to 2 decimal places
    ) AS immediate_percentage
FROM Delivery d
JOIN FirstOrders f 
ON d.customer_id = f.customer_id AND d.order_date = f.first_order_date;  
-- Join Delivery table with FirstOrders to only look at each customer’s first order
-- Count orders where order_date equals customer_pref_delivery_date (immediate orders)
```

------


26. [Game Play Analysis IV](https://leetcode.com/problems/game-play-analysis-iv/)

[1]

```sql
SELECT 
    -- Calculate the fraction of players that logged in the day after their first login
    ROUND(
        -- Count distinct players who logged in the day after their first login
        COUNT(DISTINCT CASE WHEN a.event_date = DATE_ADD(f.first_login_date, INTERVAL 1 DAY) 
                            THEN f.player_id END) * 1.0 / 
        -- Count total distinct players
        COUNT(DISTINCT f.player_id), 
        2 -- Round the result to 2 decimal places
    ) AS fraction
FROM 
    -- Subquery to get each player's first login date
    (SELECT 
        player_id, 
        MIN(event_date) AS first_login_date -- Get the earliest login date for each player
     FROM Activity
     GROUP BY player_id) f -- Group by player_id to aggregate
LEFT JOIN Activity a 
    ON f.player_id = a.player_id; -- Join the Activity table to check for logins
```

[2]

```sql
WITH FirstLogin AS (
    -- Get each player's first login date
    SELECT 
        player_id, 
        MIN(event_date) AS first_login_date
    FROM Activity
    GROUP BY player_id
),

NextDayLogin AS (
    -- Check if there’s a login the day after the first login
    SELECT 
        f.player_id,
        (a.event_date = DATE_ADD(f.first_login_date, INTERVAL 1 DAY)) AS logged_next_day
    FROM FirstLogin f
    JOIN Activity a 
    ON f.player_id = a.player_id
    WHERE a.event_date = DATE_ADD(f.first_login_date, INTERVAL 1 DAY)
)

SELECT 
    ROUND(
        1.0 * COUNT(DISTINCT player_id) / (SELECT COUNT(DISTINCT player_id) FROM Activity), 
        2
    ) AS fraction
FROM NextDayLogin
WHERE logged_next_day = 1;
```

| player_id | device_id | event_date | games_played |
|-----------|-----------|------------|--------------|
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-03-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |


```sql
WITH FirstLogin AS (
    SELECT 
        player_id, 
        MIN(event_date) AS first_login_date
    FROM Activity
    GROUP BY player_id
)
```

| player_id | first_login_date |
|-----------|------------------|
| 1         | 2016-03-01       |
| 2         | 2017-06-25       |
| 3         | 2016-03-02       |

```sql
NextDayLogin AS (
    SELECT 
        f.player_id,
        (a.event_date = DATE_ADD(f.first_login_date, INTERVAL 1 DAY)) AS logged_next_day
    FROM FirstLogin f
    JOIN Activity a 
    ON f.player_id = a.player_id
    WHERE a.event_date = DATE_ADD(f.first_login_date, INTERVAL 1 DAY)
)
```

| player_id | logged_next_day |
|-----------|-----------------|
| 1         | 1               |


```sql
SELECT 
    ROUND(
        1.0 * COUNT(DISTINCT player_id) / (SELECT COUNT(DISTINCT player_id) FROM Activity), 
        2
    ) AS fraction
FROM NextDayLogin
WHERE logged_next_day = 1
```

| fraction |
|----------|
| 0.33     |

------

27. []()

```sql

```

------


28. []()

```sql

```

------
