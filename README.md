# MySQL Using Docker
Name - Uttkarsh Sharma

This guide explains how to set up and run MySQL inside a Docker container.

## Documentation
- [Docker](https://www.docker.com/)
- [MySQL](https://www.mysql.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)

## Installation
### 1️⃣ Create the SQL File
Create a file named **database_students.sql** and add the following content:

```sql
CREATE DATABASE student;
USE student;

CREATE TABLE students (
    StudentID INT NOT NULL AUTO_INCREMENT,
    FirstName VARCHAR(100) NOT NULL,
    Surname VARCHAR(100) NOT NULL,
    PRIMARY KEY (StudentID)
);

INSERT INTO students (FirstName, Surname)
VALUES ("John", "Andersen"), ("Emma", "Smith");
```

### 2️⃣ Create the Dockerfile
Create a **Dockerfile** in the same directory as your SQL file:

```dockerfile
FROM mysql:latest

ENV MYSQL_ROOT_PASSWORD=root

COPY ./database_students.sql /docker-entrypoint-initdb.d/
```

## Deployment
Now, follow these steps to deploy MySQL using Docker.

### 🔹 Check Existing Docker Images
```sh
docker images
```

### 🔹 Build the Docker Image
```sh
docker build -t mysql_db .
```

### 🔹 Run MySQL Container (Interactive Mode)
```sh
docker run mysql_db -uroot -p
```

### 🔹 Run MySQL Container in Detached Mode
```sh
docker run -d --name my_mysql_container -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 mysql_db
```

### 🔹 Connect to MySQL Container
```sh
docker exec -it my_mysql_container mysql -uroot -p
```

### 🔹 Show Available Databases
```sql
SHOW DATABASES;
```

### 🔹 Select the student Database
```sql
USE student;
```

### 🔹 View Table Data
```sql
SELECT * FROM students;
```

Now your MySQL database is running inside Docker! 🚀

