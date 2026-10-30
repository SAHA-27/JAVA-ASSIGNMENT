# 🎓 KEC R2024 – Student Academic & Continuous Evaluation System

### Java | JDBC | MySQL | Database Management System

A **Java-based Student Academic and Continuous Evaluation System** developed for Kongu Engineering College (KEC) under the R2024 academic regulations. This project simplifies student record management, course enrollment, attendance monitoring, assessment mark entry, and academic result generation using Java JDBC and MySQL.

The system provides a menu-driven interface that allows users to manage academic information and generate student performance reports through database operations.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Objectives](#-objectives)
- [Key Features](#-key-features)
- [Technology Stack](#-technology-stack)
- [System Architecture](#-system-architecture)
- [Database Design](#-database-design)
- [Academic Evaluation Rules](#-academic-evaluation-rules)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Installation and Setup](#-installation-and-setup)
- [How to Run](#-how-to-run)
- [Application Menu](#-application-menu)
- [Expected Reports](#-expected-reports)
- [Future Enhancements](#-future-enhancements)
- [Learning Outcomes](#-learning-outcomes)
- [Author](#-author)

---

## 📖 Project Overview

The Student Academic & Continuous Evaluation System is designed to manage academic records and support continuous student evaluation.

The application uses Java for application logic and MySQL for persistent data storage. JDBC (Java Database Connectivity) connects the Java application to the MySQL database and executes SQL queries.

The system manages student information, course details, enrollment records, attendance, and assessment marks. It also supports academic reporting, including semester mark sheets, attendance defaulter reports, and department-level result summaries.

This project demonstrates the practical implementation of **Object-Oriented Programming, JDBC connectivity, relational database management, SQL queries, and academic evaluation logic**.

## 🎯 Objectives

- To maintain student academic records in a centralized database.
- To manage courses and student enrollments.
- To record and monitor student attendance.
- To store continuous internal assessment and end-semester examination marks.
- To apply academic evaluation and pass/fail rules.
- To identify students with attendance shortages.
- To generate semester mark sheets and academic performance reports.
- To demonstrate Java–MySQL integration using JDBC.

---

## ✨ Key Features

### 1. Student Management
- Register new students.
- Store roll number, student name, department, and current semester.
- View registered student records.

### 2. Course Management
- Add new courses.
- Store course code, course title, credits, and course type.
- Support THEORY, PRACTICAL, and EMBEDDED course categories.

### 3. Student Enrollment
- Enroll students in courses.
- Maintain enrollment and semester information.
- Associate attendance and assessment records with enrollments.

### 4. Attendance Management
- Record total classes conducted and classes attended.
- Calculate attendance percentages.
- Identify students with attendance below the required threshold.
- Support medical condonation approval where applicable.

### 5. Assessment Management
- Enter and update CIA1 marks.
- Enter and update CIA2 marks.
- Record assignment marks.
- Record End-Semester Examination (ESE) marks.
- Maintain examination absence information.

### 6. Student Semester Mark Sheet
Generate a student academic report containing the available assessment and result information, including:

- Student details
- Course details
- Internal assessment marks
- External examination marks
- Total marks
- Letter grade
- Pass/fail status
- SGPA and equivalent percentage, where implemented

### 7. Attendance Defaulter Report
- Identify students whose attendance is below 65%.
- Flag eligible records with the `SA` status.
- Display attendance information for monitoring.

### 8. Department Result Summary
- Summarize academic results by department.
- Support pass/fail statistics and class performance reporting.
- Provide a foundation for calculating average SGPA.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Java | Application development and business logic |
| Java JDBC | Database connectivity and SQL execution |
| MySQL | Relational database management |
| SQL | Table creation, data manipulation, and report queries |
| MySQL Connector/J | JDBC driver for connecting Java to MySQL |
| Visual Studio Code | Source code development and execution |
| MySQL Workbench | Database creation, management, and query execution |
| Git | Version control |
| GitHub | Source code hosting and project collaboration |

### Technical Concepts Used

- Object-Oriented Programming (OOP)
- Data Access Object (DAO) pattern
- CRUD operations
- Primary keys and foreign keys
- Relational database design
- SQL constraints
- Exception handling
- JDBC connection management
- Menu-driven console application
- Academic assessment calculations

---

## 🏗️ System Architecture

The application follows a simple layered architecture.

```text
        USER
          |
          v
  +------------------+
  |    MainApp.java  |
  |  Menu Interface  |
  +------------------+
          |
          v
  +------------------+
  |    StudentDAO    |
  |   AcademicDAO    |
  +------------------+
          |
          v
  +------------------+
  |  DBConnection    |
  |   JDBC Driver    |
  +------------------+
          |
          v
  +------------------+
  |  MySQL Database  |
  |  kec_academic    |
  +------------------+
          |
          v
  +------------------+
  | Academic Reports |
  | Marks & Results  |
  +------------------+
```

**Workflow:**

1. The user selects an operation from the console menu.
2. The application receives the required information.
3. DAO classes execute database operations through JDBC.
4. MySQL stores or retrieves the academic records.
5. The application displays the operation result or generates a report.

---

## 🗄️ Database Design

The project uses a MySQL database named `kec_academic`.

### 1. Students Table

**Table name:** `students`

Stores student details.

| Column | Description |
|---|---|
| roll_no | Unique student roll number |
| name | Student name |
| department | Department name |
| current_semester | Current semester |

### 2. Courses Table

**Table name:** `courses`

Stores course information.

| Column | Description |
|---|---|
| course_code | Unique course code |
| course_title | Name of the course |
| credits | Course credit value |
| course_type | THEORY, PRACTICAL, or EMBEDDED |

### 3. Enrollments Table

**Table name:** `enrollments`

Connects students with courses and maintains attendance information.

| Column | Description |
|---|---|
| enrollment_id | Unique enrollment identifier |
| roll_no | Student reference |
| course_code | Course reference |
| semester | Enrollment semester |
| classes_held | Total classes conducted |
| classes_attended | Total classes attended |
| medical_approved | Medical condonation approval status |

### 4. Assessment Marks Table

**Table name:** `assessment_marks`

Stores assessment and examination marks.

| Column | Description |
|---|---|
| enrollment_id | Enrollment reference |
| cia1 | First Continuous Internal Assessment mark |
| cia2 | Second Continuous Internal Assessment mark |
| assignment_marks | Assignment marks |
| ese_marks | End-Semester Examination marks |
| ese_absent | Indicates whether the student was absent for ESE |

### Database Relationships

- One student can have multiple enrollments.
- One course can have multiple student enrollments.
- Each enrollment connects a student and a course.
- Assessment marks are associated with an enrollment.
- Primary keys and foreign keys help maintain data integrity.

---

## 📊 Academic Evaluation Rules

The project requirements specify different internal and external assessment weightages for different course types.

| Course Type | Internal Weightage | ESE Weightage | Minimum ESE Requirement |
|---|---:|---:|---:|
| THEORY | 40% | 60% | 27 out of 60 |
| PRACTICAL | 60% | 40% | 20 out of 40 |
| EMBEDDED | 50% | 50% | 22.5 out of 50 |

Additional rules:

- The required overall passing total is 50 marks.
- Attendance of 75% or above meets the normal attendance requirement.
- Attendance from 65% to below 75% may qualify for consideration with approved medical condonation.
- Attendance below 65% is flagged as `SA`.
- Examination absence must be handled separately from ordinary marks.

**Note:** The final result depends on the assessment calculations, attendance rules, and pass/fail logic implemented in the Java source code. The rules above describe the specified project requirements.

---

## 📂 Project Structure

```text
JAVA-ASSIGNMENT/
│
├── DBConnection.java
├── StudentDAO.java
├── AcademicDAO.java
├── MainApp.java
├── kec_schema.sql
├── README.md
└── Screenshots/
    ├── student_registration.png
    ├── course_registration.png
    ├── student_enrollment.png
    ├── attendance_entry.png
    ├── assessment_marks.png
    ├── student_mark_sheet.png
    ├── attendance_defaulters.png
    └── department_result_summary.png
```

*The Screenshots folder is optional. Add it when you have captured the actual application outputs.*

### Source Files

| File | Responsibility |
|---|---|
| `DBConnection.java` | Establishes the JDBC connection to MySQL |
| `StudentDAO.java` | Handles student and course database operations |
| `AcademicDAO.java` | Handles enrollment, attendance, marks, and academic reports |
| `MainApp.java` | Provides the menu-driven application interface |
| `kec_schema.sql` | Creates the database tables and their constraints |
| `README.md` | Documents the project, setup, and execution |

---

## ⚙️ Prerequisites

Install the following software before running the application:

1. **Java JDK** — required to compile and run Java programs.
2. **MySQL Server** — required to store academic records.
3. **MySQL Workbench** — recommended for managing the database.
4. **Visual Studio Code** — recommended for editing Java files.
5. **MySQL Connector/J** — required for JDBC connectivity.

Verify the Java installation:

```bash
java -version
javac -version
```

Verify that MySQL Server is running before starting the application.

---

## 🚀 Installation and Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/SAHA-27/JAVA-ASSIGNMENT.git
```

Navigate to the project directory:

```bash
cd JAVA-ASSIGNMENT
```

Alternatively, download the repository as a ZIP file from GitHub and extract it.

### Step 2: Create the Database

Open MySQL Workbench and execute:

```sql
CREATE DATABASE IF NOT EXISTS kec_academic;

USE kec_academic;
```

### Step 3: Create the Tables

Run the SQL script provided in `kec_schema.sql`.

If the file is in the project folder, open it in MySQL Workbench and execute the script.

Confirm that the tables exist:

```sql
USE kec_academic;

SHOW TABLES;
```

The database should contain:

```text
students
courses
enrollments
assessment_marks
```

### Step 4: Configure Database Connectivity

Open `DBConnection.java` and verify the connection settings.

Example:

```java
private static final String URL =
    "jdbc:mysql://localhost:3306/kec_academic";

private static final String USER = "root";

private static final String PASSWORD = "YOUR_PASSWORD";
```

Replace `YOUR_PASSWORD` with your actual MySQL password.

**Security note:** Do not upload real database passwords or other credentials to a public GitHub repository.

### Step 5: Configure MySQL Connector/J

Download MySQL Connector/J from the official MySQL website if it is not already available.

Place the JAR file in the project directory or configure it in your Java classpath.

Example JAR filename:

```text
mysql-connector-j-9.x.x.jar
```

Use the actual filename of the JAR file you have installed.

---

## ▶️ How to Run

### Windows Command Prompt

Open Command Prompt and navigate to the project directory.

Example:

```cmd
cd /d "E:\java project"
```

Compile the source files:

```cmd
javac -cp ".;mysql-connector-j-9.x.x.jar" DBConnection.java StudentDAO.java AcademicDAO.java MainApp.java
```

Run the application:

```cmd
java -cp ".;mysql-connector-j-9.x.x.jar" MainApp
```

**Important:** Replace `mysql-connector-j-9.x.x.jar` with your actual JAR filename. If the JAR is configured elsewhere, update the classpath accordingly.

The application will display a menu in the console.

---

## 🖥️ Application Menu

The application provides the following menu options:

```text
====================================
 KEC R2024 ACADEMIC EVALUATION SYSTEM
====================================

1. Register Student
2. Add Course
3. View Students
4. Enroll Student in Course
5. Update Attendance
6. Approve Medical Condonation
7. Enter / Update Assessment Marks
8. Generate Student Mark Sheet
9. Attendance Defaulter Report
10. Department Result Summary
0. Exit

Enter your choice:
```

The exact menu text depends on the current implementation of `MainApp.java`.

---

## 📑 Expected Reports

### 1. Student Registration

Displays a confirmation message when a student is successfully registered.

### 2. Course Registration

Displays a confirmation message when a course is added.

### 3. Student Semester Mark Sheet

The intended report includes:

- Student roll number and name
- Department and semester
- Course details
- Internal and external marks
- Total marks
- Letter grade
- Pass/fail status
- SGPA
- Equivalent percentage

### 4. Attendance Defaulter Report

Identifies students whose attendance is below 65% and flags them with `SA`.

### 5. Department Result Summary

The intended summary includes department-wise student counts, pass/fail counts, and average SGPA.

**Implementation note:** These are the expected reporting requirements. Confirm that each calculation and report is implemented and tested in the current source code before presenting it as a completed feature.

---

## 🔮 Future Enhancements

The system can be extended with the following features:

- A graphical user interface using Java Swing or JavaFX.
- Student and faculty login authentication.
- Role-based access control for administrators and faculty.
- PDF generation for semester mark sheets.
- Excel export for attendance and result reports.
- A web-based academic dashboard.
- Automated email notifications for attendance shortages.
- Improved analytics and semester-wise performance visualization.
- Automated testing and validation of assessment calculations.

---

## 🎓 Learning Outcomes

This project provides practical experience in:

- Java programming and object-oriented design.
- JDBC connectivity between Java and MySQL.
- Relational database design and SQL constraints.
- Implementing CRUD operations.
- Using DAO classes to organize database logic.
- Handling attendance and assessment records.
- Generating reports from relational data.
- Debugging and executing Java applications.
- Using Git and GitHub for source code management.

---

## 👩‍💻 Author

**Sri Sahana Udhayakumar**

Student Developer | Information Technology

### GitHub

[SAHA-27](https://github.com/SAHA-27)

### Project Repository

[JAVA-ASSIGNMENT](https://github.com/SAHA-27/JAVA-ASSIGNMENT)
## 🎥 Project Demo Video

Click below to watch the complete project demonstration.

[▶️ Watch Project Demo Video]https://drive.google.com/file/d/1bbh1UqYm-oBkswQw9eFa617p-Dfgv6hC/view?usp=drive_link

---

## 📜 License

This project was developed for academic learning and demonstration purposes.

Add a license file if you intend to distribute the project under a specific open-source license.

---

⭐ If you find this project useful, consider starring the repository on GitHub!
