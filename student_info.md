# README: student_info.sh Script

This README provides a detailed explanation of the `student_info.sh` script. The script fetches information about computer science students from the `students` database using SQL queries executed via `psql`.

---

## Script Overview

The script retrieves various pieces of information about students and their associated data, including:
1. Students with a 4.0 GPA.
2. Courses with names starting before 'D' in the alphabet.
3. Students meeting specific GPA and last name conditions.
4. Last names matching certain patterns.
5. Students without a major meeting other conditions.
6. Courses matching letter-based criteria.
7. Average GPA.
8. Grouped data based on major IDs.
9. Majors meeting specific criteria.
10. Unique courses not taken by any student or a specific student.
11. Courses with exactly one student enrolled.

---

## Script Sections

### 1. **Retrieve Students with a 4.0 GPA**
```bash
echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE gpa = 4.0")"
```
- **Description**: Displays the first name, last name, and GPA of students with a perfect 4.0 GPA.
- **SQL Query**:
  ```sql
  SELECT first_name, last_name, gpa FROM students WHERE gpa = 4.0;
  ```

### 2. **Courses Starting Before 'D'**
```bash
echo "$($PSQL "SELECT course FROM courses WHERE course < 'D'")"
```
- **Description**: Lists course names alphabetically whose names start before 'D'.
- **SQL Query**:
  ```sql
  SELECT course FROM courses WHERE course < 'D';
  ```

### 3. **Students with Specific Last Names and GPAs**
```bash
echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE last_name >= 'R' AND (gpa > 3.8 OR gpa < 2.0)")"
```
- **Description**: Displays students whose last name starts with 'R' or later, and have a GPA > 3.8 or < 2.0.
- **SQL Query**:
  ```sql
  SELECT first_name, last_name, gpa FROM students WHERE last_name >= 'R' AND (gpa > 3.8 OR gpa < 2.0);
  ```

### 4. **Students with Specific Last Names**
```bash
echo "$($PSQL "SELECT last_name FROM students WHERE last_name ILIKE '%sa%' OR last_name ILIKE '%r_'")"
```
- **Description**: Displays the last names of students where:
  - The last name contains 'sa' (case-insensitive).
  - The second-to-last letter in the last name is 'r'.
- **SQL Query**:
  ```sql
  SELECT last_name FROM students WHERE last_name ILIKE '%sa%' OR last_name ILIKE '%r_';
  ```

### 5. **Students Without a Major**
```bash
echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE major_id IS NULL AND (first_name LIKE 'D%' OR gpa > 3.0)")"
```
- **Description**: Displays the first name, last name, and GPA of students who:
  - Have not selected a major.
  - Either their first name starts with 'D' or their GPA is > 3.0.
- **SQL Query**:
  ```sql
  SELECT first_name, last_name, gpa FROM students WHERE major_id IS NULL AND (first_name LIKE 'D%' OR gpa > 3.0);
  ```

### 6. **Courses Matching Letter-Based Criteria**
```bash
echo "$($PSQL "SELECT course FROM courses WHERE course LIKE '_e%' OR course LIKE '%s' ORDER BY course DESC LIMIT 5")"
```
- **Description**: Retrieves the first 5 courses (in reverse alphabetical order) that:
  - Have 'e' as the second letter.
  - End with 's'.
- **SQL Query**:
  ```sql
  SELECT course FROM courses WHERE course LIKE '_e%' OR course LIKE '%s' ORDER BY course DESC LIMIT 5;
  ```

### 7. **Average GPA**
```bash
echo "$($PSQL "SELECT ROUND(AVG(gpa), 2) FROM students")"
```
- **Description**: Calculates the average GPA of all students, rounded to two decimal places.
- **SQL Query**:
  ```sql
  SELECT ROUND(AVG(gpa), 2) FROM students;
  ```

### 8. **Grouped Data by Major ID**
```bash
echo "$($PSQL "SELECT major_id, COUNT(*) AS number_of_students, ROUND(AVG(gpa), 2) AS average_gpa FROM students GROUP BY major_id HAVING COUNT(*) > 1")"
```
- **Description**: Retrieves the major ID, total number of students, and average GPA (rounded to two decimals) for majors with more than one student.
- **SQL Query**:
  ```sql
  SELECT major_id, COUNT(*) AS number_of_students, ROUND(AVG(gpa), 2) AS average_gpa FROM students GROUP BY major_id HAVING COUNT(*) > 1;
  ```

### 9. **Majors Meeting Specific Criteria**
```bash
echo "$($PSQL "SELECT major FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE major IS NOT NULL AND (student_id IS NULL OR first_name ILIKE '%ma%') ORDER BY major")"
```
- **Description**: Lists majors (alphabetically) that:
  - Have no students.
  - Or have students whose first name contains 'ma' (case-insensitive).
- **SQL Query**:
  ```sql
  SELECT major FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE major IS NOT NULL AND (student_id IS NULL OR first_name ILIKE '%ma%') ORDER BY major;
  ```

### 10. **Unique Courses Not Taken by Any Student or a Specific Student**
```bash
echo "$($PSQL "select DISTINCT course from students FULL JOIN majors_courses using(major_id) FULL JOIN courses using(course_id) where student_id IS NULL or (first_name='Obie' AND last_name='Hilpert') order by course DESC")"
```
- **Description**: Lists unique courses (in reverse alphabetical order) that:
  - Are not taken by any student.
  - Or are not taken by 'Obie Hilpert'.
- **SQL Query**:
  ```sql
  SELECT DISTINCT course FROM students FULL JOIN majors_courses USING (major_id) FULL JOIN courses USING (course_id) WHERE student_id IS NULL OR (first_name='Obie' AND last_name='Hilpert') ORDER BY course DESC;
  ```

### 11. **Courses with Exactly One Student Enrolled**
```bash
echo "$($PSQL "SELECT course FROM students INNER JOIN majors_courses USING(major_id) INNER JOIN courses USING(course_id) GROUP BY course HAVING COUNT(student_id) = 1 ORDER BY course")"
```
- **Description**: Lists courses (alphabetically) that have exactly one student enrolled.
- **SQL Query**:
  ```sql
  SELECT course FROM students INNER JOIN majors_courses USING (major_id) INNER JOIN courses USING (course_id) GROUP BY course HAVING COUNT(student_id) = 1 ORDER BY course;
  ```

---



