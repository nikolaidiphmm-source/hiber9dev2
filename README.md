# Hibernate School Management System

A Java application demonstrating Hibernate/JPA ORM capabilities for managing a school system with teachers, courses, and regions.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies](#technologies)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Setup Instructions](#setup-instructions)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Entity Relationships](#entity-relationships)
- [Development](#development)

## 🎯 Overview

This project is a school management system built with Java, Hibernate ORM, and MySQL. It demonstrates JPA entity relationships including One-to-One, One-to-Many, and Many-to-Many associations.

## ✨ Features

- **Teacher Management**: Create and manage teacher records with additional information
- **Course Management**: Manage courses with different lesson types
- **Region Management**: Organize teachers by regions
- **Bidirectional Relationships**: Properly managed associations between entities
- **JPA/Hibernate ORM**: Object-relational mapping with automatic schema generation

## 🛠️ Technologies

- **Java 21**: Programming language
- **Maven**: Build and dependency management
- **Hibernate 6.6.41**: JPA implementation
- **MySQL 9.5.0**: Database
- **Lombok 1.18.42**: Reduces boilerplate code
- **JUnit 5**: Testing framework

## 📦 Prerequisites

Before running this project, ensure you have the following installed:

- **JDK 21** or higher
- **Maven 3.6+**
- **MySQL 8.0+** (or compatible database)
- **IDE** (IntelliJ IDEA, Eclipse, or VS Code) with Lombok plugin enabled

## 📁 Project Structure

```
hiber9dev2ai/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── gr/aueb/cf/
│   │   │       ├── App.java                    # Main application entry point
│   │   │       ├── enums/
│   │   │       │   ├── GenderType.java         # Gender enumeration
│   │   │       │   └── LessonType.java         # Lesson type enumeration
│   │   │       └── model/
│   │   │           ├── Teacher.java            # Teacher entity
│   │   │           ├── TeacherMoreInfo.java    # Additional teacher info (One-to-One)
│   │   │           ├── Course.java             # Course entity
│   │   │           └── Region.java             # Region entity
│   │   └── resources/
│   │       └── META-INF/
│   │           └── persistence.xml             # JPA persistence configuration
│   └── test/
│       └── java/
│           └── gr/aueb/cf/
│               └── AppTest.java                # Unit tests
├── pom.xml                                      # Maven configuration
└── README.md                                    # This file
```

## 🗄️ Database Schema

The application uses the following main entities:

### Teachers Table
- `id` (Primary Key, Auto-generated)
- `firstname` (NOT NULL)
- `lastname` (NOT NULL)
- `active` (Boolean)
- `region_id` (Foreign Key to Regions)
- `teacher_more_info_id` (Foreign Key to TeacherMoreInfo)

### Courses Table
- `id` (Primary Key, Auto-generated)
- `title` (NOT NULL, UNIQUE)
- `comments` (VARCHAR 1000)
- `lesson_type` (Enum: THEORY, LAB, MIXED)

### Regions Table
- `id` (Primary Key, Auto-generated)
- `title` (NOT NULL, UNIQUE)

### TeacherMoreInfo Table
- `id` (Primary Key, Auto-generated)
- `date_of_birth` (LocalDateTime)
- `gender` (Enum: MALE, FEMALE, OTHER)

### Courses_Teachers Table (Join Table)
- `course_id` (Foreign Key to Courses)
- `teacher_id` (Foreign Key to Teachers)

## ⚙️ Setup Instructions

### 1. Clone or Download the Project

```bash
git clone <repository-url>
cd hiber9dev2ai
```

### 2. Create MySQL Database

Connect to your MySQL server and create the database:

```sql
CREATE DATABASE hiber9dev2;
```

### 3. Create Database User (Optional)

```sql
CREATE USER 'cf9user'@'localhost' IDENTIFIED BY '12345';
GRANT ALL PRIVILEGES ON hiber9dev2.* TO 'cf9user'@'localhost';
FLUSH PRIVILEGES;
```

### 4. Configure Database Connection

Edit `src/main/resources/META-INF/persistence.xml` and update the following properties if needed:

```xml
<property name="hibernate.connection.url" value="jdbc:mysql://localhost:3306/hiber9dev2?serverTimezone=UTC" />
<property name="hibernate.connection.username" value="cf9user" />
<property name="hibernate.connection.password" value="12345" />
```

**⚠️ Security Note**: For production, use environment variables or externalized configuration files instead of hardcoded credentials.

### 5. Build the Project

```bash
mvn clean install
```

### 6. Enable Lombok in Your IDE

- **IntelliJ IDEA**: Install Lombok plugin and enable annotation processing
- **Eclipse**: Install Lombok plugin
- **VS Code**: Install "Language Support for Java" extension

## 🔧 Configuration

### Persistence Configuration

The `persistence.xml` file contains the following key settings:

- **Persistence Unit**: `schoolPU`
- **Provider**: Hibernate JPA
- **Schema Generation**: `hibernate.hbm2ddl.auto=update` (automatically creates/updates tables)
- **SQL Logging**: Enabled for development (`hibernate.show_sql=true`)

### Hibernate Settings

- **Show SQL**: `true` (logs all SQL queries)
- **Format SQL**: `true` (formats SQL output)
- **DDL Auto**: `update` (updates schema on startup)

## 🚀 Running the Application

### Using Maven

```bash
mvn compile exec:java -Dexec.mainClass="gr.aueb.cf.App"
```

### Using IDE

1. Open the project in your IDE
2. Navigate to `gr.aueb.cf.App`
3. Run the `main` method

### Running Tests

```bash
mvn test
```

## 🔗 Entity Relationships

### One-to-One: Teacher ↔ TeacherMoreInfo
- One teacher has one additional info record
- Cascade: ALL (operations cascade to related entity)
- Orphan Removal: Enabled

### One-to-Many: Region ↔ Teachers
- One region can have many teachers
- Bidirectional relationship
- Fetch Type: LAZY

### Many-to-Many: Teachers ↔ Courses
- Many teachers can teach many courses
- Join table: `courses_teachers`
- Bidirectional relationship with helper methods

## 💻 Development

### Adding New Entities

1. Create entity class in `gr.aueb.cf.model` package
2. Add JPA annotations (`@Entity`, `@Table`, etc.)
3. Configure relationships with other entities
4. Hibernate will automatically create the table on next run

### Code Style

- Uses Lombok for getters, setters, and constructors
- Entities use `@NoArgsConstructor` from Lombok
- Collections are initialized and protected with access modifiers
- Helper methods provided for bidirectional relationship management

### Best Practices Implemented

- ✅ Unmodifiable collections returned via `getAllXxx()` methods
- ✅ Bidirectional relationship synchronization in helper methods
- ✅ Proper cascade and orphan removal configuration
- ✅ Enum types for type-safe values

## 📝 Notes

- The database schema is automatically generated/updated on application startup
- SQL queries are logged to console for debugging
- The project uses Java 21 features
- Lombok requires annotation processing to be enabled in your IDE

## 🔮 Future Improvements

- Add Service/DAO layer for business logic separation
- Implement proper exception handling
- Add input validation with Bean Validation
- Create REST API endpoints
- Add comprehensive unit and integration tests
- Implement database migrations with Flyway/Liquibase
- Add logging framework (SLF4J/Logback)
- Externalize configuration to properties files

## 📄 License

This project is for educational purposes.

## 👤 Author

Created as part of Hibernate/JPA learning project.

---

**Happy Coding! 🎉**