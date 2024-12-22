# README: Student Database Project (Part 2)

This README file outlines all the SQL commands and keywords used in Part 2 of the "Build a Student Database" project. The commands are described in chronological order, providing details on their purpose and usage.

---

## 1. **CREATE TABLE**
   - **Description**: Used to create a new table in the database.
   - **Syntax**:
     ```sql
     CREATE TABLE table_name (
       column_name1 data_type constraints,
       column_name2 data_type constraints,
       ...
     );
     ```
   - **Example**:
     ```sql
     CREATE TABLE students (
       student_id SERIAL PRIMARY KEY,
       first_name VARCHAR(50),
       last_name VARCHAR(50),
       major_id INT
     );
     ```

## 2. **SERIAL**
   - **Description**: Generates a unique, auto-incrementing integer value for a column.
   - **Usage**: Typically used for primary key columns.

## 3. **PRIMARY KEY**
   - **Description**: Defines a unique identifier for each row in a table.
   - **Usage**: Ensures that no duplicate values exist in the specified column(s).

## 4. **FOREIGN KEY**
   - **Description**: Establishes a relationship between two tables by referencing a column in another table.
   - **Syntax**:
     ```sql
     FOREIGN KEY (column_name) REFERENCES other_table(column_name)
     ```
   - **Example**:
     ```sql
     CREATE TABLE majors (
       major_id SERIAL PRIMARY KEY,
       major_name VARCHAR(100)
     );

     ALTER TABLE students
     ADD CONSTRAINT fk_major
     FOREIGN KEY (major_id) REFERENCES majors(major_id);
     ```

## 5. **INSERT INTO**
   - **Description**: Adds new rows of data to a table.
   - **Syntax**:
     ```sql
     INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
     ```
   - **Example**:
     ```sql
     INSERT INTO majors (major_name) VALUES ('Computer Science');
     INSERT INTO students (first_name, last_name, major_id) VALUES ('John', 'Doe', 1);
     ```

## 6. **SELECT**
   - **Description**: Retrieves data from a table.
   - **Syntax**:
     ```sql
     SELECT column1, column2 FROM table_name;
     ```
   - **Example**:
     ```sql
     SELECT * FROM students;
     SELECT first_name, major_id FROM students;
     ```

## 7. **INNER JOIN**
   - **Description**: Combines rows from two or more tables based on a related column.
   - **Syntax**:
     ```sql
     SELECT columns
     FROM table1
     INNER JOIN table2 ON table1.column_name = table2.column_name;
     ```
   - **Example**:
     ```sql
     SELECT students.first_name, majors.major_name
     FROM students
     INNER JOIN majors ON students.major_id = majors.major_id;
     ```

## 8. **LEFT JOIN**
   - **Description**: Returns all rows from the left table and the matching rows from the right table. Rows with no match will contain `NULL`.
   - **Syntax**:
     ```sql
     SELECT columns
     FROM table1
     LEFT JOIN table2 ON table1.column_name = table2.column_name;
     ```
   - **Example**:
     ```sql
     SELECT students.first_name, majors.major_name
     FROM students
     LEFT JOIN majors ON students.major_id = majors.major_id;
     ```

## 9. **FULL JOIN**
   - **Description**: Combines rows from two tables, returning all rows from both tables. Rows with no match will contain `NULL`.
   - **Syntax**:
     ```sql
     SELECT columns
     FROM table1
     FULL JOIN table2 ON table1.column_name = table2.column_name;
     ```

## 10. **WHERE**
   - **Description**: Filters rows based on a condition.
   - **Syntax**:
     ```sql
     SELECT columns FROM table_name WHERE condition;
     ```
   - **Example**:
     ```sql
     SELECT * FROM students WHERE major_id = 1;
     ```

## 11. **GROUP BY**
   - **Description**: Groups rows that have the same values in specified columns.
   - **Syntax**:
     ```sql
     SELECT column, aggregate_function(column)
     FROM table_name
     GROUP BY column;
     ```
   - **Example**:
     ```sql
     SELECT major_id, COUNT(*)
     FROM students
     GROUP BY major_id;
     ```

## 12. **HAVING**
   - **Description**: Filters grouped rows based on a condition.
   - **Syntax**:
     ```sql
     SELECT column, aggregate_function(column)
     FROM table_name
     GROUP BY column
     HAVING condition;
     ```
   - **Example**:
     ```sql
     SELECT major_id, COUNT(*)
     FROM students
     GROUP BY major_id
     HAVING COUNT(*) > 5;
     ```

## 13. **ORDER BY**
   - **Description**: Sorts the result set in ascending or descending order.
   - **Syntax**:
     ```sql
     SELECT columns
     FROM table_name
     ORDER BY column [ASC|DESC];
     ```
   - **Example**:
     ```sql
     SELECT * FROM students ORDER BY last_name ASC;
     ```

## 14. **DISTINCT**
   - **Description**: Ensures unique rows are returned in the result set.
   - **Syntax**:
     ```sql
     SELECT DISTINCT column FROM table_name;
     ```
   - **Example**:
     ```sql
     SELECT DISTINCT major_id FROM students;
     ```

---

This document provides a detailed explanation of all the commands and keywords used in Part 2 of the project.
