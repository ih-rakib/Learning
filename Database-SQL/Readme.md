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


