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

11. [Employee Bonus](https://leetcode.com/problems/employee-bonus/)

```sql
SELECT E.name, B.bonus
FROM Employee E
LEFT JOIN Bonus B
ON E.empId = B.empId
WHERE B.bonus < 1000 OR B.empId IS NULL;
```

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

13. []()

```sql

```

14. []()

```sql

```
