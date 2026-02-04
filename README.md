# Hiber9 Demo Project

This project is a simple Java application demonstrating basic JPA/Hibernate usage with entities such as `Teacher`, `TeacherMoreInfo`, `Course`, and `Region`.  
It is built with Maven and uses Jakarta Persistence annotations and Lombok to reduce boilerplate.

## Prerequisites

- **Java**: JDK 17+ (recommended)
- **Maven**: 3.8+  
- (Optional) A database supported by your JPA provider (e.g. PostgreSQL, MySQL, H2, etc.), configured in `persistence.xml`.

## Project Structure

- `src/main/java/gr/aueb/cf/`
  - `App.java`: Main application entry point (if used).
  - `model/`: JPA entities (`Teacher`, `TeacherMoreInfo`, `Course`, `Region`, etc.).
  - `enums/`: Enum types such as `GenderType`, `LessonType`.
- `src/main/resources/META-INF/persistence.xml`: JPA persistence configuration.
- `src/test/java/gr/aueb/cf/AppTest.java`: Sample tests.

## Building

From the project root:

mvn clean compile
