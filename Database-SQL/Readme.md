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
- [SQLite Online](https://sqliteonline.com/)
- [DB Fiddle](https://www.db-fiddle.com/)


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
