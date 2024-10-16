# Database - SQL

## Introduction to Databases and SQL

### What is a Database?
- A database is a structured collection of data. It helps store, retrieve, and manage data efficiently.

### What is SQL?
- SQL is a programming language used to communicate with databases. It allows you to perform various operations like querying data, updating records, and managing database structures.

### Environment To practice
- **SQLite** (lightweight and easy to set up)
- **MySQL** (popular for web applications)
- **PostgreSQL** (powerful open-source database)

### Online Environment
- [SQLzoo](https://sqlzoo.net/wiki/SQL_Tutorial)
- [SQLite Online](https://sqliteonline.com/)
- [DB Fiddle](https://www.db-fiddle.com/)


### Data Types 

| Data Type   | Description                                                | Example              |
|-------------|------------------------------------------------------------|----------------------|
| INTEGER     | A whole number.                                           | `1`, `42`, `-100`    |
| SMALLINT    | A smaller integer range.                                   | `100`, `-20`         |
| FLOAT       | Approximate numeric values with decimal points.           | `3.14`, `-0.001`     |
| DOUBLE      | Double-precision floating-point number.                   | `3.14159265359`      |
| TEXT        | A string of text, variable length.                        | `'John Doe'`        |
| CHAR(n)     | Fixed-length character string, where `n` is the length.  | `'A'`, `'Hello'`     |
| VARCHAR(n)  | Variable-length string, with `n` as the maximum length.  | `'Alice'`, `'Bob'`   |
| DATE        | Stores dates.                                             | `2024-10-14`         |
| TIME        | Stores time.                                             | `14:30:00`           |
| DATETIME    | Stores both date and time.                                | `2024-10-14 14:30:00`|
| BOOLEAN     | Represents truth values (`TRUE` or `FALSE`).             | `TRUE`, `FALSE`      |


## Basic SQL Commands

### a. Creating a Database

```sql
CREATE DATABASE School;
```

### Creating a Books Table

| BookID | Title                    | Author                | PublishedYear |
|--------|--------------------------|-----------------------|----------------|
| INTEGER (Primary Key) | TEXT (Not Null) | TEXT (Not Null) | INTEGER |

**Command to Create this Table:**

```sql
CREATE TABLE Books (
    BookID INTEGER PRIMARY KEY,
    Title TEXT NOT NULL,
    Author TEXT NOT NULL,
    PublishedYear INTEGER
);
```

### Inserting Data

| BookID | Title                    | Author                | PublishedYear |
|--------|--------------------------|-----------------------|----------------|
| 1      | The Great Gatsby         | F. Scott Fitzgerald    | 1925           |
| 2      | To Kill a Mockingbird    | Harper Lee            | 1960           |
| 3      | 1984                     | George Orwell         | 1949           |

**Command to Insert Data:**

```sql
INSERT INTO Books (BookID, Title, Author, PublishedYear) VALUES
(1, 'The Great Gatsby', 'F. Scott Fitzgerald', 1925),
(2, 'To Kill a Mockingbird', 'Harper Lee', 1960),
(3, '1984', 'George Orwell', 1949);
```

### Querying Data

```sql
SELECT * FROM Books;
```

# Examples

## Example 1:

## Create this Table

| StudentID | FirstName | LastName | Age | Grade |
|-----------|-----------|----------|-----|-------|
| INTEGER   | TEXT      | TEXT     | INTEGER | TEXT |

**Command to Create this Table with Data Types:**

```sql
CREATE TABLE Students (
    StudentID INTEGER PRIMARY KEY,  -- Unique ID for each student
    FirstName TEXT NOT NULL,        -- Student's first name
    LastName TEXT NOT NULL,         -- Student's last name
    Age INTEGER,                    -- Student's age
    Grade TEXT                      -- Student's grade (e.g., 10th, 11th)
);
```

- Inserting Data in a Table
- Updating Data in a Table
- Deleting Data from a Table
- Filtering Data with WHERE Clause

1. Inserting Data in a Table

```sql
INSERT INTO Students (StudentID, FirstName, LastName, Age, Grade) VALUES
(1, 'John', 'Doe', 15, '10th'),
(2, 'Jane', 'Smith', 14, '9th'),
(3, 'Emily', 'Davis', 16, '11th');
```

| StudentID | FirstName | LastName | Age | Grade |
|-----------|-----------|----------|-----|-------|
| 1         | John      | Doe      | 15  | 10th  |
| 2         | Jane      | Smith    | 14  | 9th   |
| 3         | Emily     | Davis    | 16  | 11th  |


2. Updating Data in a Table

```sql
UPDATE Students
SET Age = 77
WHERE FirstName = 'Jane' AND LastName = 'Smith';
```

| StudentID | FirstName | LastName | Age | Grade |
|-----------|-----------|----------|-----|-------|
| 1         | John      | Doe      | 15  | 10th  |
| 2         | Jane      | Smith    | 77  | 9th   |
| 3         | Emily     | Davis    | 16  | 11th  |


3. Deleting Data from a Table
```sql
DELETE FROM Students
WHERE FirstName = 'Emily' AND LastName = 'Davis';
```

| StudentID | FirstName | LastName | Age | Grade |
|-----------|-----------|----------|-----|-------|
| 1         | John      | Doe      | 15  | 10th  |
| 2         | Jane      | Smith    | 15  | 9th   |

4. Filtering Data with WHERE Clause

```sql
SELECT * FROM Students
WHERE Grade = '10th';
```

| StudentID | FirstName | LastName | Age | Grade |
|-----------|-----------|----------|-----|-------|
| 1         | John      | Doe      | 15  | 10th  |


## Example 2:

1. Creating a Database

```sql
CREATE DATABASE UniversityDB;
```

2. Using the Database

```sql
USE UniversityDB;
```

3. Creating a Courses Table

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| INTEGER  | TEXT                 | TEXT           | INTEGER |

```sql
CREATE TABLE Courses (
    CourseID INTEGER PRIMARY KEY,
    CourseName TEXT NOT NULL,
    Instructor TEXT NOT NULL,
    Credits INTEGER
);
```

4. Inserting Data into the Courses Table

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 3       |
| 3        | Web Development      | Dr. Smith      | 5       |

```sql
INSERT INTO Courses (CourseID, CourseName, Instructor, Credits) VALUES
(1, 'Introduction to SQL', 'Dr. Brown', 4),
(2, 'Data Structures', 'Dr. Lee', 3),
(3, 'Web Development', 'Dr. Smith', 5);
```

5. Querying Data

```sql
SELECT * FROM Courses;
```

this will return:

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 3       |
| 3        | Web Development      | Dr. Smith      | 5       |


6. Updating Data in the Courses Table

```sql
UPDATE Courses
SET Credits = 4
WHERE CourseName = 'Data Structures';
```

After updating the table it will look like: 

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 4       |
| 3        | Web Development      | Dr. Smith      | 5       |


7. Deleting Data from the Courses Table

```sql
DELETE FROM Courses
WHERE CourseName = 'Web Development';
```

After deletion: 

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 4       |

Great! 😄
> create, insert, update, filtering, delete done!

Now -->

- Insert more Data
- Filtering Data with WHERE Clause
- Sorting Data with ORDER BY
- Using Aggregate Functions
- Grouping Data with GROUP BY
- Joining Tables

1. Insert More Data
```
INSERT INTO Courses(CourseId, CourseName, Instructor, Credits) VALUES
(3, 'Web Development', 'Dr Han', 2),
(4, 'Machine Learning', 'Dr Bota', 1),
(5, 'AI', 'Dr Matata', 3),
(6, 'Software Engineering', 'Lun Do', 4),
(7, 'UI/UX Development', 'Kevin Chik', 2);

SELECT * FROM Courses;
```

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 4       |
| 3        | Web Development	  | Dr Han	       | 2       |
| 4        | Machine Learning	  | Dr Bota	       | 1       |
| 5        | AI                	  | Dr Matata	   | 3       |
| 6        | Software Engineering | Lun Do	       | 4       |
| 7        | UI/UX Development	  | Kevin Chik	   | 2       |

2. Filtering Data with WHERE Clause

```sql
SELECT * FROM Courses
WHERE Credits > 2;
```

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 4       |
| 6        | Software Engineering | Lun Do	       | 4       |
| 5        | AI                	  | Dr Matata	   | 3       |


3. Sorting Data with ORDER BY

```sql
SELECT * FROM Courses
ORDER BY Credits DESC;
```

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 4       |
| 6        | Software Engineering  | Lun Do        | 4       |
| 5        | AI                   | Dr Matata      | 3       |
| 3        | Web Development      | Dr Han         | 2       |
| 7        | UI/UX Development    | Kevin Chik     | 2       |
| 4        | Machine Learning     | Dr Bota        | 1       |


4. Using Aggregate Functions

Aggregate functions perform calculations on a set of values and return a single value.

**Example: Count the Number of Courses**

```sql
SELECT COUNT(*) AS NumberOfCourses FROM Courses;
```

| NumberOfCourses |
|------------------|
| 7                |


**Example: Find the Average Credits of Courses**

```sql
SELECT AVG(Credits) AS AverageCredits FROM Courses;
```

| AverageCredits |
|-----------------|
| 3.14            |


5. Grouping Data with GROUP BY

```sql
SELECT Credits, COUNT(*) AS NumberOfCourses 
FROM Courses 
GROUP BY Credits;
```

| Credits | NumberOfCourses |
|---------|-----------------|
| 1       | 1               |
| 2       | 3               |
| 3       | 1               |
| 4       | 3               |


6. Joining Tables

Joining tables allows you to combine rows from two or more tables based on a related column.

a. Creating Another Table
Let's create an Instructors table for demonstration.

Command to Create Instructors Table:

```sql
CREATE TABLE Instructors (
    InstructorID INTEGER PRIMARY KEY,
    InstructorName TEXT NOT NULL,
    ExperienceYears INTEGER
);
```

Insert Data into Instructors Table:

```sql
INSERT INTO Instructors (InstructorID, InstructorName, ExperienceYears) VALUES
(1, 'Dr. Brown', 10),
(2, 'Dr. Lee', 8),
(3, 'Dr Han', 5),
(4, 'Dr Bota', 6),
(5, 'Dr Matata', 7),
(6, 'Lun Do', 4),
(7, 'Kevin Chik', 3);
```

```sql
SELECT * FROM Instructors;
```

| InstructorID | InstructorName | ExperienceYears |
|--------------|----------------|------------------|
| 1            | Dr. Brown      | 10               |
| 2            | Dr. Lee        | 8                |
| 3            | Dr Han         | 5                |
| 4            | Dr Bota        | 6                |
| 5            | Dr Matata      | 7                |
| 6            | Lun Do         | 4                |
| 7            | Kevin Chik     | 3                |

```sql
SELECT * FROM Courses;
```

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 4       |
| 3        | Web Development      | Dr Han         | 2       |
| 4        | Machine Learning     | Dr Bota        | 1       |
| 5        | AI                   | Dr Matata      | 3       |
| 6        | Software Engineering  | Lun Do         | 4       |
| 7        | UI/UX Development    | Kevin Chik     | 2       |
``


**Joining Courses and Instructors Tables**

Now that we have data in both Courses and Instructors, we can perform a join operation to combine relevant information.

```sql
SELECT C.CourseName, I.InstructorName, I.ExperienceYears
FROM Courses C
JOIN Instructors I ON C.Instructor = I.InstructorName;
```

| CourseName           | InstructorName | ExperienceYears |
|----------------------|----------------|------------------|
| Introduction to SQL  | Dr. Brown      | 10               |
| Data Structures      | Dr. Lee        | 8                |
| Web Development      | Dr Han         | 5                |
| Machine Learning     | Dr Bota       | 6                |
| AI                   | Dr Matata      | 7                |
| Software Engineering  | Lun Do        | 4                |
| UI/UX Development    | Kevin Chik    | 3                |


### SQL Query and Explanation

```sql
SELECT C.CourseName, I.InstructorName, I.ExperienceYears
FROM Courses C
JOIN Instructors I ON C.Instructor = I.InstructorName;
```

**1. Column Selection:**

- This part specifies the columns to retrieve:
  - `C.CourseName` refers to the course name from the `Courses` table (aliased as `C`).
  - `I.InstructorName` and `I.ExperienceYears` refer to the instructor's name and their years of experience from the `Instructors` table (aliased as `I`).

---

**2. Primary Table:**

- This indicates that the query is primarily selecting data from the `Courses` table, which is aliased as `C` for easier reference in the query.

---

**3. Joining Tables:**

- This part joins the `Instructors` table, which is aliased as `I`, with the `Courses` table.
- The `JOIN` operation is used to combine rows from both tables based on a related column between them.

---

**4. Join Condition:**

- This specifies the condition for the join.
- It indicates that the `Instructor` column from the `Courses` table must match the `InstructorName` column from the `Instructors` table.
- This allows the query to pull the corresponding instructor's details for each course.

-------

so far : 

### Courses Table

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 4       |
| 3        | Web Development      | Dr Han         | 2       |
| 4        | Machine Learning     | Dr. Bota       | 1       |
| 5        | AI                   | Dr Matata      | 3       |
| 6        | Software Engineering  | Lun Do         | 4       |
| 7        | UI/UX Development    | Kevin Chik     | 2       |


### Instructors Table

| InstructorID | InstructorName | ExperienceYears |
|--------------|----------------|------------------|
| 1            | Dr. Brown      | 10               |
| 2            | Dr. Lee        | 8                |
| 3            | Dr Han         | 5                |
| 4            | Dr. Bota       | 6                |
| 5            | Dr. Matata     | 7                |
| 6            | Lun Do         | 4                |
| 7            | Kevin Chik     | 3                |


7. LEFT JOIN

A LEFT JOIN returns all records from the left table (Courses) and the matched records from the right table (Instructors). If there is no match, the result is NULL on the right side.

**Example: Left Join on Courses and Instructors**

```sql
SELECT C.CourseName, I.InstructorName
FROM Courses C
LEFT JOIN Instructors I ON C.Instructor = I.InstructorName;
```

| CourseName           | InstructorName |
|----------------------|----------------|
| Introduction to SQL  | Dr. Brown      |
| Data Structures      | Dr. Lee        |
| Web Development      | Dr Han         |
| Machine Learning     | Dr. Bota      |
| AI                   | Dr. Matata     |
| Software Engineering  | Lun Do         |
| UI/UX Development    | Kevin Chik    |


8. RIGHT JOIN

A RIGHT JOIN returns all records from the right table (Instructors) and the matched records from the left table (Courses). If there is no match, the result is NULL on the left side.

```sql
SELECT C.CourseName, I.InstructorName
FROM Courses C
RIGHT JOIN Instructors I ON C.Instructor = I.InstructorName;
```

| CourseName           | InstructorName |
|----------------------|----------------|
| Introduction to SQL  | Dr. Brown      |
| Data Structures      | Dr. Lee        |
| Web Development      | Dr Han         |
| Machine Learning     | Dr. Bota      |
| AI                   | Dr. Matata     |
| Software Engineering  | Lun Do         |
| UI/UX Development    | Kevin Chik     |


### Key Differences

Returned Records:

LEFT JOIN: Returns all rows from the left table, regardless of matches in the right table.
RIGHT JOIN: Returns all rows from the right table, regardless of matches in the left table.
Handling Non-Matches:

In a LEFT JOIN, if there are no matches for a left table row, the right side shows NULL.
In a RIGHT JOIN, if there are no matches for a right table row, the left side shows NULL.


😕 Can't find any difference???

1. Insert a New Course Without an Instructor

Let’s add a course named "Cloud Computing" that has no instructor assigned.

```sql
INSERT INTO Courses (CourseID, CourseName, Instructor, Credits) VALUES 
(8, 'Cloud Computing', 'Dr. Taylor', 3);
```

***Updated Courses Table:***

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 4       |
| 3        | Web Development      | Dr Han         | 2       |
| 4        | Machine Learning     | Dr. Bota      | 1       |
| 5        | AI                   | Dr. Matata     | 3       |
| 6        | Software Engineering  | Lun Do         | 4       |
| 7        | UI/UX Development    | Kevin Chik     | 2       |
| 8        | Cloud Computing      | Dr. Taylor     | 3       |


2. Insert a New Instructor Without a Course

Let’s add an instructor named "Dr. Smith" who has no courses assigned.

```sql
INSERT INTO Instructors (InstructorID, InstructorName, ExperienceYears) VALUES 
(8, 'Dr. Smith', 2);
```

***Updated Instructors Table:***

| InstructorID | InstructorName | ExperienceYears |
|--------------|----------------|------------------|
| 1            | Dr. Brown      | 10               |
| 2            | Dr. Lee        | 8                |
| 3            | Dr Han         | 5                |
| 4            | Dr. Bota      | 6                |
| 5            | Dr. Matata     | 7                |
| 6            | Lun Do         | 4                |
| 7            | Kevin Chik     | 3                |
| 8            | Dr. Smith      | 2                |


```sql
UPDATE Courses
SET Instructor = NULL
WHERE CourseID = 8;  
```

| CourseID | CourseName           | Instructor     | Credits |
|----------|----------------------|----------------|---------|
| 1        | Introduction to SQL  | Dr. Brown      | 4       |
| 2        | Data Structures      | Dr. Lee        | 4       |
| 3        | Web Development      | Dr Han         | 2       |
| 4        | Machine Learning     | Dr. Bota       | 1       |
| 5        | AI                   | Dr. Matata     | 3       |
| 6        | Software Engineering  | Lun Do         | 4       |
| 7        | UI/UX Development    | Kevin Chik     | 2       |
| 8        | Cloud Computing      | NULL           | 3       |



### LEFT JOIN Example

Now, if we perform a LEFT JOIN to see all courses and their corresponding instructors:

```sql
SELECT C.CourseName, I.InstructorName
FROM Courses C
LEFT JOIN Instructors I ON C.Instructor = I.InstructorName;
```

| CourseName           | InstructorName |
|----------------------|----------------|
| Introduction to SQL  | Dr. Brown      |
| Data Structures      | Dr. Lee        |
| Web Development      | Dr Han         |
| Machine Learning     | Dr. Bota      |
| AI                   | Dr. Matata     |
| Software Engineering  | Lun Do         |
| UI/UX Development    | Kevin Chik     |
| Cloud Computing      | NULL           |


### RIGHT JOIN Example

```sql
SELECT C.CourseName, I.InstructorName
FROM Courses C
RIGHT JOIN Instructors I ON C.Instructor = I.InstructorName;
```

| CourseName           | InstructorName |
|----------------------|----------------|
| Introduction to SQL  | Dr. Brown      |
| Data Structures      | Dr. Lee        |
| Web Development      | Dr Han         |
| Machine Learning     | Dr. Bota      |
| AI                   | Dr. Matata     |
| Software Engineering  | Lun Do         |
| UI/UX Development    | Kevin Chik     |
| NULL                 | Dr. Smith      |


9. FULL OUTER JOIN
A FULL OUTER JOIN returns all records from both tables, with matching records from both sides when available. If there is no match, NULL values will appear in the result for non-matching records.

```sql
SELECT C.CourseName, I.InstructorName
FROM Courses C
FULL OUTER JOIN Instructors I ON C.Instructor = I.InstructorName;
```

| CourseName           | InstructorName |
|----------------------|----------------|
| Introduction to SQL  | Dr. Brown      |
| Data Structures      | Dr. Lee        |
| Web Development      | Dr Han         |
| Machine Learning     | Dr. Bota      |
| AI                   | Dr. Matata     |
| Software Engineering  | Lun Do         |
| UI/UX Development    | Kevin Chik     |
| Cloud Computing      | NULL           |
| NULL                 | Dr. Smith      |


10. CROSS JOIN
A CROSS JOIN produces a Cartesian product of two tables, which means each row from the first table is combined with all rows from the second table.

```sql
SELECT C.CourseName, I.InstructorName
FROM Courses C
CROSS JOIN Instructors I;
```

| CourseName           | InstructorName |
|----------------------|----------------|
| Introduction to SQL  | Dr. Brown      |
| Introduction to SQL  | Dr. Lee        |
| Introduction to SQL  | Dr Han         |
| Introduction to SQL  | Dr. Bota      |
| Introduction to SQL  | Dr. Matata     |
| Introduction to SQL  | Lun Do         |
| Introduction to SQL  | Kevin Chik     |
| Introduction to SQL  | Dr. Smith      |
| Data Structures      | Dr. Brown      |
| Data Structures      | Dr. Lee        |
| Data Structures      | Dr Han         |
| Data Structures      | Dr. Bota      |
| Data Structures      | Dr. Matata     |
| Data Structures      | Lun Do         |
| Data Structures      | Kevin Chik     |
| Data Structures      | Dr. Smith      |
| Web Development      | Dr. Brown      |
| Web Development      | Dr. Lee        |
| Web Development      | Dr Han         |
| Web Development      | Dr. Bota      |
| Web Development      | Dr. Matata     |
| Web Development      | Lun Do         |
| Web Development      | Kevin Chik     |
| Web Development      | Dr. Smith      |
| Machine Learning     | Dr. Brown      |
| Machine Learning     | Dr. Lee        |
| Machine Learning     | Dr Han         |
| Machine Learning     | Dr. Bota      |
| Machine Learning     | Dr. Matata     |
| Machine Learning     | Lun Do         |
| Machine Learning     | Kevin Chik     |
| Machine Learning     | Dr. Smith      |
| AI                   | Dr. Brown      |
| AI                   | Dr. Lee        |
| AI                   | Dr Han         |
| AI                   | Dr. Bota      |
| AI                   | Dr. Matata     |
| AI                   | Lun Do         |
| AI                   | Kevin Chik     |
| AI                   | Dr. Smith      |
| Software Engineering  | Dr. Brown      |
| Software Engineering  | Dr. Lee        |
| Software Engineering  | Dr Han         |
| Software Engineering  | Dr. Bota      |
| Software Engineering  | Dr. Matata     |
| Software Engineering  | Lun Do         |
| Software Engineering  | Kevin Chik     |
| Software Engineering  | Dr. Smith      |
| UI/UX Development    | Dr. Brown      |
| UI/UX Development    | Dr. Lee        |
| UI/UX Development    | Dr Han         |
| UI/UX Development    | Dr. Bota      |
| UI/UX Development    | Dr. Matata     |
| UI/UX Development    | Lun Do         |
| UI/UX Development    | Kevin Chik     |
| UI/UX Development    | Dr. Smith      |
| Cloud Computing      | Dr. Brown      |
| Cloud Computing      | Dr. Lee        |
| Cloud Computing      | Dr Han         |
| Cloud Computing      | Dr. Bota      |
| Cloud Computing      | Dr. Matata     |
| Cloud Computing      | Lun Do         |
| Cloud Computing      | Kevin Chik     |
| Cloud Computing      | Dr. Smith      |


11. SELF JOIN
A SELF JOIN is a regular join but the table is joined with itself. This is useful for comparing rows within the same table.

Example: Self Join on Instructors
In this case, we can use a self-join to find pairs of instructors where one has more experience than the other

existing table: 

### Instructors Table

| InstructorID | InstructorName | ExperienceYears |
|--------------|----------------|------------------|
| 1            | Dr. Brown      | 10               |
| 2            | Dr. Lee        | 8                |
| 3            | Dr Han         | 5                |
| 4            | Dr. Bota       | 6                |
| 5            | Dr. Matata     | 7                |
| 6            | Lun Do         | 4                |
| 7            | Kevin Chik     | 3                |

```sql
SELECT A.InstructorName AS MoreExperienced, B.InstructorName AS LessExperienced
FROM Instructors A
JOIN Instructors B ON A.ExperienceYears > B.ExperienceYears;
```

| MoreExperienced | LessExperienced |
|------------------|-----------------|
| Dr. Brown        | Dr. Lee         |
| Dr. Brown        | Dr. Han         |
| Dr. Brown        | Dr. Bota        |
| Dr. Brown        | Dr. Matata     |
| Dr. Brown        | Lun Do          |
| Dr. Brown        | Kevin Chik      |
| Dr. Brown        | Dr. Smith       |
| Dr. Lee          | Dr. Han         |
| Dr. Lee          | Dr. Bota        |
| Dr. Lee          | Dr. Matata      |
| Dr. Lee          | Lun Do          |
| Dr. Lee          | Kevin Chik      |
| Dr. Lee          | Dr. Smith       |
| Dr. Han          | Dr. Bota        |
| Dr. Han          | Dr. Matata      |
| Dr. Han          | Lun Do          |
| Dr. Han          | Kevin Chik      |
| Dr. Han          | Dr. Smith       |
| Dr. Bota         | Dr. Matata      |
| Dr. Bota         | Lun Do          |
| Dr. Bota         | Kevin Chik      |
| Dr. Bota         | Dr. Smith       |
| Dr. Matata      | Lun Do          |
| Dr. Matata      | Kevin Chik      |
| Dr. Matata      | Dr. Smith       |
| Lun Do          | Kevin Chik      |
| Lun Do          | Dr. Smith       |
| Kevin Chik      | Dr. Smith       |

----------


# Next Topic: Subquery

Example: Subquery in the WHERE Clause
Finding all courses taught by instructors with more than 5 years of experience:

```sql
SELECT CourseName
FROM Courses
WHERE Instructor IN (
    SELECT InstructorName
    FROM Instructors
    WHERE ExperienceYears > 5
);
```

| CourseName           |
|----------------------|
| Introduction to SQL  |
| Data Structures      |
| Machine Learning     |
| AI                   |
| Software Engineering  |
| UI/UX Development    |


Example: Subquery in the SELECT Clause
Listing each instructor with the number of courses they teach:

```sql
SELECT I.InstructorName,
       (SELECT COUNT(*)
        FROM Courses C
        WHERE C.Instructor = I.InstructorName) AS CourseCount
FROM Instructors I;
```

| InstructorName | CourseCount |
|----------------|-------------|
| Dr. Brown      | 1           |
| Dr. Lee        | 1           |
| Dr Han         | 1           |
| Dr. Bota       | 1           |
| Dr. Matata     | 1           |
| Lun Do         | 1           |
| Kevin Chik     | 1           |
| Dr. Smith      | 0           |


Example: Subquery in the FROM Clause
Creating a temporary table to select experienced instructors:

```sql
SELECT InstructorName, ExperienceYears
FROM (SELECT InstructorName, ExperienceYears
      FROM Instructors
      WHERE ExperienceYears > 5) AS ExperiencedInstructors;
```

| InstructorName | ExperienceYears |
|----------------|------------------|
| Dr. Brown      | 10               |
| Dr. Lee        | 8                |
| Dr. Bota       | 6                |
| Dr. Matata     | 7                |

you can't see the name ExperiencedInstructors in the output, as it serves as an internal structure for the query processing rather than a part of the final result set.

:))))))

```sql
SELECT InstructorName, ExperienceYears
FROM Instructors
WHERE ExperienceYears > 5;
```

:))))))


# Next Topic: Common Table Expressions (CTEs)

Common Table Expressions (CTEs) provide a way to create temporary result sets that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement. They can make complex queries easier to read and maintain.

```sql
WITH ExperiencedInstructors AS (
    SELECT InstructorName, ExperienceYears
    FROM Instructors
    WHERE ExperienceYears > 5
)
SELECT InstructorName
FROM ExperiencedInstructors;
```

| InstructorName |
|----------------|
| Dr. Brown      |
| Dr. Lee        |
| Dr. Bota       |
| Dr. Matata     |



# Next Topic: Window Functions

Window functions allow you to perform calculations across a set of table rows that are somehow related to the current row. They are useful for running totals, moving averages, and ranking data.

Example: Using the ROW_NUMBER() Window Function

Let's say we want to assign a unique rank to each instructor based on their years of experience.

```sql
SELECT InstructorName, ExperienceYears,
       ROW_NUMBER() OVER (ORDER BY ExperienceYears DESC) AS Rank
FROM Instructors;
```

| InstructorName | ExperienceYears | Rank |
|----------------|------------------|------|
| Dr. Brown      | 10               | 1    |
| Dr. Lee        | 8                | 2    |
| Dr. Matata     | 7                | 3    |
| Dr. Bota       | 6                | 4    |
| Dr Han         | 5                | 5    |
| Lun Do         | 4                | 6    |
| Kevin Chik     | 3                | 7    |
| Dr. Smith      | 2                | 8    |

Explanation:
Window Function: ROW_NUMBER() assigns a unique sequential integer to rows within a partition of a result set, starting at 1 for the first row in each partition.
ORDER BY Clause: The ORDER BY ExperienceYears DESC clause specifies that the ranking should be based on the years of experience in descending order.
Window functions allow you to perform calculations across a defined range of rows while maintaining the ability to return individual row data.
