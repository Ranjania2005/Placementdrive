## Placement Drive Management System

A console-based Java application for managing college placement drives, student applications, and company recruitment.

## Project Overview

This is a student-level software engineering project that demonstrates:
- Object-oriented programming principles
- JDBC for database connectivity
- Menu-driven console interface
- Exception handling
- Collection usage
- Modular project structure

## Features

- **Admin Authentication**: Secure login for placement officers
- **Student Management**: Add and view student details with CGPA tracking
- **Company Management**: Add company details, salary, and requirements
- **Eligibility Check**: Check which companies a student is eligible for based on CGPA
- **Application Management**: Students can apply for companies they're eligible for
- **Interview Results**: Update selection/rejection status for student applications
- **Statistics**: View placement statistics and metrics
- **Search**: Search for students or companies by name

## Project Structure

```
placementdrive/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/example/placementdrive/
│       │       ├── model/
│       │       │   ├── Student.java
│       │       │   ├── Company.java
│       │       │   └── Application.java
│       │       ├── service/
│       │       │   ├── AdminService.java
│       │       │   ├── StudentService.java
│       │       │   ├── CompanyService.java
│       │       │   └── ApplicationService.java
│       │       ├── db/
│       │       │   └── DBConnection.java
│       │       ├── util/
│       │       │   └── InputUtil.java
│       │       └── main/
│       │           └── PlacementDriveApp.java
│       └── resources/
│           └── application.properties
├── database_schema.sql
├── pom.xml
└── README.md
```

## Package Details

### `model/`
Contains entity classes representing database tables:
- `Student.java` - Student entity with getters/setters
- `Company.java` - Company entity with details like salary and eligibility criteria
- `Application.java` - Application entity linking students and companies

### `service/`
Business logic layer:
- `AdminService.java` - Handles admin authentication
- `StudentService.java` - CRUD operations for students
- `CompanyService.java` - CRUD operations for companies
- `ApplicationService.java` - Application management, eligibility check, statistics

### `db/`
- `DBConnection.java` - JDBC connection utility using MySQL connector

### `util/`
- `InputUtil.java` - Helper methods for console input/output

### `main/`
- `PlacementDriveApp.java` - Main application with menu-driven interface

## Database Schema

Three main tables:

1. **students** - Stores student information
   - std_id, name, email, cgpa, branch_id

2. **companies** - Stores company details
   - comp_id, comp_name, industry, salary, openings, min_cgpa, drive_date

3. **applications** - Tracks student applications
   - app_id, std_id, comp_id, app_date, status

See `database_schema.sql` for complete schema with sample data.

## Prerequisites

- Java 8 or higher
- MySQL 5.7 or higher
- MySQL Connector/J (Java JDBC driver)

## Installation & Setup

### 1. Database Setup
```bash
mysql -u root -p < database_schema.sql
```

Default credentials: root / root (can be modified in DBConnection.java)

### 2. Add MySQL Driver to Project
Update `pom.xml` with:
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
</dependency>
```

### 3. Update Database Credentials
Edit `src/main/java/com/example/placementdrive/db/DBConnection.java`:
```java
private static final String URL = "jdbc:mysql://localhost:3306/placement_db";
private static final String USER = "root";
private static final String PASSWORD = "root";
```

## Compilation & Running

### Using Maven
```bash
mvn clean compile
mvn exec:java -Dexec.mainClass="com.example.placementdrive.main.PlacementDriveApp"
```

### Using Command Line (without Maven)
```bash
javac -cp mysql-connector-java-8.0.33.jar src/main/java/com/example/placementdrive/**/*.java
java -cp .:mysql-connector-java-8.0.33.jar com.example.placementdrive.main.PlacementDriveApp
```

## Usage

### Login
```
Admin ID: admin
Password: admin123
```

### Main Menu Options

1. **Add Student** - Register a new student
2. **Add Company** - Register a new company for recruitment
3. **View All Students** - List all registered students
4. **View All Companies** - List all companies
5. **Check Student Eligibility** - See which companies a student can apply to
6. **Apply for Company Drive** - Submit application to a company
7. **View Applied Students** - See all applications for a company
8. **Update Interview Result** - Mark students as Selected/Rejected
9. **View Placement Statistics** - See placement metrics
10. **Search** - Find students or companies
11. **Exit** - Close the application

## Sample Workflow

```
1. Login with admin credentials
2. Add 2-3 companies with different eligibility criteria
3. Add 3-4 students with different CGPA values
4. Check student eligibility for companies
5. Submit applications for eligible students
6. Update results for applications
7. View placement statistics
```

## Key Methods

### StudentService
- `addStd()` - Add new student
- `showAllStd()` - Display all students
- `searchStd()` - Search student by name
- `getStdById(int)` - Fetch student details

### CompanyService
- `addComp()` - Add new company
- `showComp()` - Display all companies
- `searchComp()` - Search company by name
- `getCompById(int)` - Fetch company details

### ApplicationService
- `chkElig(int)` - Check eligible companies for student
- `applyDrive()` - Submit application
- `showAppliedStd()` - View applications for a company
- `updateResult()` - Update selection status
- `showStats()` - Display statistics

## Error Handling

All database operations include try-catch blocks for SQLException handling. Input validation is done for:
- Email format
- CGPA range (0-10)
- Status values (Selected/Rejected)
- Duplicate applications prevention

## Notes

- Students cannot apply twice to same company (UNIQUE constraint)
- Students can only apply if CGPA meets company requirement
- All dates stored in YYYY-MM-DD format
- CGPA precision: 2 decimal places
- Salary in LPA (Lakhs Per Annum)

## Future Enhancements

- Student login functionality
- Email notifications
- PDF report generation
- Spring Boot refactoring
- REST API implementation
- Web UI with Servlets

## License

This is an educational project for learning purposes.
#
