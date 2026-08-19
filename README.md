# 🎓 College Database Management System

## 📌 Overview

**College Database Management System** is a MySQL-based database project designed to store and manage information about a college.

The database contains information about:

* 🏢 Departments
* 👨‍🎓 Students
* 📚 Courses
* 📝 Student Enrollments
* 👨‍🏫 Faculty

This project demonstrates the use of **SQL databases, primary keys, foreign keys, unique constraints, NOT NULL constraints, CHECK constraints, INSERT statements, SELECT statements, and table relationships**.

---

## 🗄️ Database Name

```sql
CREATE DATABASE college_zoro;
```

> **Note:** The provided script later uses `college_demo`. For consistency, use the same database name throughout the script, for example:

```sql
CREATE DATABASE college_zoro;
USE college_zoro;
```

---

# 📊 Database Tables

The project contains five main tables:

```text
college_zoro
│
├── department
│
├── student
│
├── course
│
├── enrollment
│
└── faculty
```

---

## 🏢 1. Department Table

The `department` table stores information about different college departments.

| Column      | Data Type   | Description            |
| ----------- | ----------- | ---------------------- |
| `dept_id`   | INT         | Unique department ID   |
| `dept_name` | VARCHAR(50) | Name of the department |

### Constraints

* `dept_id` → Primary Key
* `dept_name` → UNIQUE
* `dept_name` → NOT NULL

### Sample Data

| dept_id | dept_name        |
| ------: | ---------------- |
|       1 | Computer Science |
|       2 | Mechanical       |
|       3 | Electronics      |

---

## 👨‍🎓 2. Student Table

The `student` table stores student information.

| Column      | Data Type   | Description                |
| ----------- | ----------- | -------------------------- |
| `roll_no`   | INT         | Unique student roll number |
| `name`      | VARCHAR(50) | Student name               |
| `email`     | VARCHAR(50) | Student email              |
| `aadhar_no` | VARCHAR(12) | Student Aadhaar number     |
| `dept_id`   | INT         | Student's department       |

### Constraints

* `roll_no` → Primary Key
* `name` → NOT NULL
* `email` → UNIQUE
* `aadhar_no` → UNIQUE
* `dept_id` → Foreign Key

The `dept_id` column references:

```text
department(dept_id)
```

### Sample Students

| Roll No. | Name          | Department       |
| -------: | ------------- | ---------------- |
|      101 | Laksh Kapse   | Computer Science |
|      102 | Varun Gharote | Mechanical       |
|      103 | Deep Kuswha   | Computer Science |

---

## 📚 3. Course Table

The `course` table stores courses offered by different departments.

| Column        | Data Type   | Description                    |
| ------------- | ----------- | ------------------------------ |
| `course_id`   | INT         | Unique course ID               |
| `course_name` | VARCHAR(50) | Course name                    |
| `dept_id`     | INT         | Department offering the course |

### Constraints

* `course_id` → Primary Key
* `course_name` → NOT NULL
* `dept_id` → Foreign Key

The `dept_id` references:

```text
department(dept_id)
```

### Sample Courses

| Course ID | Course Name      | Department       |
| --------: | ---------------- | ---------------- |
|       201 | Database Systems | Computer Science |
|       202 | Thermodynamics   | Mechanical       |
|       203 | Digital Circuits | Electronics      |

---

## 📝 4. Enrollment Table

The `enrollment` table records which students are enrolled in which courses.

| Column      | Data Type | Description         |
| ----------- | --------- | ------------------- |
| `roll_no`   | INT       | Student roll number |
| `course_id` | INT       | Course ID           |
| `semester`  | INT       | Semester number     |
| `grade`     | CHAR(2)   | Student grade       |

### Constraints

The table uses a **Composite Primary Key**:

```text
(roll_no, course_id, semester)
```

It also contains:

* `roll_no` → Foreign Key referencing `student(roll_no)`
* `course_id` → Foreign Key referencing `course(course_id)`
* `semester` → CHECK constraint between 1 and 8

### Sample Enrollment Data

| Roll No. | Course ID | Semester | Grade |
| -------: | --------: | -------: | ----- |
|      101 |       201 |        3 | A     |
|      101 |       203 |        4 | B     |
|      102 |       202 |        3 | A     |
|      103 |       201 |        3 | B     |

---

## 👨‍🏫 5. Faculty Table

The `faculty` table stores information about college faculty members.

| Column         | Data Type   | Description          |
| -------------- | ----------- | -------------------- |
| `faculty_id`   | INT         | Unique faculty ID    |
| `faculty_name` | VARCHAR(50) | Faculty name         |
| `email`        | VARCHAR(50) | Faculty email        |
| `phone_no`     | VARCHAR(15) | Faculty phone number |
| `dept_id`      | INT         | Faculty department   |

### Constraints

* `faculty_id` → Primary Key
* `faculty_name` → NOT NULL
* `email` → UNIQUE
* `phone_no` → UNIQUE
* `dept_id` → Foreign Key

The `dept_id` references:

```text
department(dept_id)
```

### Sample Faculty Data

| Faculty ID | Faculty Name | Department       |
| ---------: | ------------ | ---------------- |
|        201 | Dr. Sharma   | Computer Science |
|        202 | Prof. Mehta  | Mechanical       |
|        203 | Dr. Rao      | Electronics      |

---

# 🔗 Database Relationships

The tables are connected using **Foreign Keys**.

```text
                 ┌──────────────────┐
                 │    DEPARTMENT    │
                 │──────────────────│
                 │ dept_id (PK)     │
                 │ dept_name        │
                 └───────┬──────────┘
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
   ┌────────────┐ ┌────────────┐ ┌────────────┐
   │  STUDENT   │ │   COURSE   │ │  FACULTY   │
   │────────────│ │────────────│ │────────────│
   │ roll_no PK │ │course_id PK│ │faculty_id PK│
   │ name       │ │course_name │ │faculty_name│
   │ dept_id FK │ │ dept_id FK │ │ dept_id FK │
   └──────┬─────┘ └──────┬─────┘ └────────────┘
          │               │
          └───────┬───────┘
                  ▼
          ┌────────────────┐
          │   ENROLLMENT   │
          │────────────────│
          │ roll_no FK     │
          │ course_id FK   │
          │ semester       │
          │ grade          │
          └────────────────┘
```

---

# 🔑 SQL Concepts Used

This project demonstrates the following SQL concepts:

### Primary Key

Used to uniquely identify records.

```sql
PRIMARY KEY
```

Examples:

```text
department.dept_id
student.roll_no
course.course_id
faculty.faculty_id
```

### Foreign Key

Used to create relationships between tables.

```sql
FOREIGN KEY (dept_id)
REFERENCES department(dept_id)
```

### UNIQUE Constraint

Prevents duplicate values.

```sql
email VARCHAR(50) UNIQUE
```

### NOT NULL Constraint

Ensures that a column cannot contain `NULL`.

```sql
name VARCHAR(50) NOT NULL
```

### CHECK Constraint

Restricts values according to a condition.

```sql
CHECK (semester BETWEEN 1 AND 8)
```

### Composite Primary Key

The `enrollment` table uses multiple columns as its primary key:

```sql
PRIMARY KEY (roll_no, course_id, semester)
```

---

# 🚀 How to Run the Project

## Step 1: Create the Database

```sql
CREATE DATABASE college_zoro;
```

## Step 2: Select the Database

```sql
USE college_zoro;
```

## Step 3: Create the Tables

Create the tables in this order:

```text
1. department
2. student
3. course
4. enrollment
5. faculty
```

This order is important because the tables contain foreign-key relationships.

## Step 4: Insert Data

Insert the sample department, student, course, enrollment, and faculty records.

## Step 5: View the Data

Use:

```sql
SELECT * FROM department;
SELECT * FROM student;
SELECT * FROM course;
SELECT * FROM enrollment;
SELECT * FROM faculty;
```

---

# 🔍 Useful SQL Commands

### Show all tables

```sql
SHOW TABLES;
```

### Describe a table

```sql
DESC department;
DESC student;
DESC course;
DESC enrollment;
DESC faculty;
```

### Display all students

```sql
SELECT * FROM student;
```

### Display all courses

```sql
SELECT * FROM course;
```

### Display all faculty members

```sql
SELECT * FROM faculty;
```

### Display enrollment records

```sql
SELECT * FROM enrollment;
```

---

# ⚠️ Important Note

There is a database-name mismatch in the original SQL script:

```sql
CREATE DATABASE college_zoro;
```

but later:

```sql
USE college_demo;
```

If `college_demo` does not already exist, this will cause an error.

### Recommended correction

Replace:

```sql
USE college_demo;
```

with:

```sql
USE college_zoro;
```

and use `college_zoro` consistently throughout the project.

---

# 🎯 Project Objectives

The main objectives of this project are:

* Learn how to create a relational database.
* Understand table creation using `CREATE TABLE`.
* Understand primary and foreign keys.
* Establish relationships between multiple tables.
* Use SQL constraints to maintain data integrity.
* Insert and retrieve records.
* Understand composite primary keys.
* Practice basic MySQL commands.

---

# 🛠️ Technologies Used

* **MySQL**
* **SQL**
* **MySQL Workbench** (recommended)

---

# 🔮 Future Improvements

This database can be expanded by adding:

* Attendance management
* Examination and marks tables
* Semester-wise GPA/CGPA
* Faculty-course relationships
* Student phone numbers
* Course credits
* Timetable management
* Library management
* Fees and payment records
* Student performance reports

---

# 👨‍💻 Author

**Laksh Kapse**

---

## 📜 License

This project is created for **educational and learning purposes**.
