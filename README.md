# SQL Commands with MySQL (by Codanics)

> SQL commands to interact with a MySQL database on Windows
![SQL-Commands-Markdown Banner](https://user-images.githubusercontent.com/43797457/184001962-6461bc67-3062-4c17-9c2c-8eb2a1422d24.png)

## Login

```bash
mysql -u root -p
```

## Show Users

```sql
SELECT User, Host FROM mysql.user;
```

## Create User

```sql
CREATE USER 'someuser'@'localhost' IDENTIFIED BY 'somepassword';
```

## Grant All Privileges On All Databases

```sql
GRANT ALL PRIVILEGES ON * . * TO 'someuser'@'localhost';
FLUSH PRIVILEGES;
```

## Show Grants

```sql
SHOW GRANTS FOR 'someuser'@'localhost';
```

## Remove Grants

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'someuser'@'localhost';
```

## Delete User

```sql
DROP USER 'someuser'@'localhost';
```

## Clear Screen

```sql
\! cls;
```

## Exit

```sql
exit;
```

## Show Databases

```sql
SHOW DATABASES
```

## Create Database

```sql
CREATE DATABASE codanics;
```

## Delete Database

```sql
DROP DATABASE codanics;
```

## Select Database

```sql
USE codanics;
```

## Create Table

```sql
CREATE TABLE students(
   stuID int,
   stuNAME VARCHAR(100),
   stuAGE VARCHAR(100),
   stuCITY VARCHAR(50)
);
```

## Delete / Drop Table

```sql
DROP TABLE students;
```

## Show Tables

```sql
SHOW TABLES;
```

## Describe Tables

```sql
DESC students;
```

## Insert Row / Record

```sql
INSERT INTO students (stuID, stuNAME, stuAGE, stuCITY) values (01, 'Minhas', 25, 'Lahore');
```

## Insert Multiple Rows

```sql
INSERT INTO students (stuID, stuNAME, stuAGE, stuCITY) values (02, 'Dawood', 27, 'Lahore'), (03, 'Sunila', 24, 'Sialkot'),(04, 'Sami', 25, 'Faisalabad'),(05, 'Zeeshan', 27, 'Massachusetts'),(06, 'Hamza', 25, 'Layyah');
```

## Select

```sql
SELECT * FROM students;
SELECT stuNAME, stuCITY FROM students;
```

## Where Clause

```sql
SELECT * FROM students WHERE stuCITY ='Faisalabad';
SELECT stuNAME, stuCITY FROM students WHERE stuAGE > 25;
SELECT * FROM students WHERE stuAGE = 25;
```

## Delete Row

```sql
DELETE FROM students WHERE stuID = 5;
```

## Update Row

```sql
UPDATE students SET stuAGE = 30 WHERE stuID = 01;

```

## Add New Column

```sql
ALTER TABLE students ADD stuCOUNTRY TEXT;
```

## Add New Column at a Specific Position

```sql
ALTER TABLE students ADD email VARCHAR(30) AFTER stuAGE;
```

## Modify Column

```sql
ALTER TABLE students MODIFY COLUMN stuCOUNTRY VARCHAR(20);
```

## Add Record in New Column

```sql
UPDATE students SET stuCOUNTRY = "Pakistan" WHERE stuAGE < 27;
```

## Delete Column

```sql
ALTER TABLE students DROP email;
```

## CONSTRAINTS
<ul>
	<li><strong>NOT NULL:</strong> Doesn't accept a NULL value</li>
	<li><strong>UNIQUE:</strong> Doesn't accept a duplicate</li>
        <li><strong>PRIMARY KEY:</strong> The key by which a Table forms relation with another Table. Its NOT NULL and UNIQUE</li>
	<li><strong>FOREIGN KEY:</strong> When PRIMARY KEY of a Table is introduced in another Table it becomes FOREIGN KEY</li>
	<li><strong>CHECK:</strong> Apply conditional statements such as < > = <= >= </li>
	<li><strong>DEFAULT:</strong> The default value for the field when a value isn't present</li>
	<li><strong>INDEX:</strong> To speed up the querying process</li>
</ul>

#### NOT NULL, UNIQUE, PRIMARY KEY
```sql
CREATE TABLE codanians(
stuID INT,
stuNAME VARCHAR(100) UNIQUE,
stuAGE INT NOT NULL DEFAULT 0,
PRIMARY KEY (stuID)
);
```

```sql
INSERT INTO codanians(stuID, stuNAME, stuAGE) VALUES (01, "Arslan", 30),(02, "Ali", 27),(03, "Sunila", 24);
```

#### DEFAULT (A default value will be assigned to the column if we don't insert anything into it)
```sql
CREATE TABLE school(
stuID INT,
stuNAME VARCHAR(100),
stuAGE INT,
stuCITY TEXT DEFAULT "Faisalabad"
UNIQUE (stuID, stuAGE)
);
```

```sql
INSERT INTO school(stuID, stuNAME, stuAGE) VALUES (01, "Arslan", 30),(02, "Ali", 27),(03, "Sunila", 24);
```
```sql
INSERT INTO school(stuID, stuNAME, stuAGE, stuCITY) VALUES (01, "Arslan", 30, "Lahore"),(02, "Ali", 27, "Islamabad"),(03, "Sunila", 24, DEFAULT);
```

#### Assign CONSTRAINT Using ALTER TABLE (Multiple Ways)
```sql
ALTER TABLE school MODIFY stuAGE INT NOT NULL;
```
```sql
ALTER TABLE school ADD UNIQUE (stuNAME);
```

#### COMPOUND PRIMARY KEY
```sql
CREATE TABLE school(
stuID INT,
stuNAME VARCHAR(100),
stuAGE INT,
PRIMARY KEY (stuID, stuAGE)
);
```

#### Assign CONSTRAINTS (Another Method)
```sql
CREATE TABLE school(
stuID INT,
stuNAME VARCHAR(100),
stuAGE INT,
CONSTRAINT PRIMARY KEY (stuID, stuAGE)
);
```

#### Remove CONSTRAINTS (Multiple Ways)
```sql
SHOW INDEX FROM school;
```
```sql
ALTER TABLE school DROP PRIMARY KEY;
```
```sql
ALTER TABLE school DROP INDEX stuID;
```
```sql
DROP INDEX stuID ON school;
```

#### FOREIGN KEY (Relating College to School Table)
```sql
CREATE TABLE college(
Id INT,
schID INT,
name VARCHAR(100),
age INT,
PRIMARY KEY (id),
FOREIGN KEY (schID) REFERENCES school(stuID)
);
```
```sql
INSERT INTO college(Id, name, age) VALUES (01, "Minhas", 30),(02, "Dawood", 27),(03, "Sunila", 24),(04, "Sami", 25), (05, "Zeeshan", 27), (06, "Hamza", 25);
```

#### CHECK (Adding condition that only Adults data can be inserted)
```sql
CREATE TABLE university(
stuID INT,
stuNAME VARCHAR(100),
stuAGE INT,
PRIMARY KEY (stuID),
CHECK (stuAGE >= 18)
);
```

#### CHECK On Multiple Columns
```sql
CREATE TABLE punjab_uni(
stuID INT,
stuNAME VARCHAR(100),
stuAGE INT,
stuCITY VARCHAR(100),
PRIMARY KEY (stuID),
CHECK (stuAGE >= 18 AND stuCITY IN ("FAISALBAD","LAHORE","SARGODHA"))
);
```

#### INDEX (To speed up the query)
```sql
CREATE INDEX uni_index ON punjab_uni (stuID);
SHOW INDEX FROM punjab_uni;
```

## Auto-Increment

```sql
CREATE TABLE punjab_uni(
stuID INT AUTO_INCREMENT,
stuNAME VARCHAR(100),
stuAGE INT,
stuCITY VARCHAR(100),
PRIMARY KEY (stuID)
);
```
```sql
INSERT INTO punjab_uni(stuNAME, stuAGE, stuCITY) VALUES ("Minhas", 30, "LHR"),("Dawood", 27, "LYH"),("Sunila", 24, "SIA"),("Sami", 25, "FSD"), ("Zeeshan", 27, "UK"), ("Hamza", 25, "FSD");

```
## Reset Auto-Increment (If we delete some records)
```sql
DELETE FROM punjab_uni WHERE stuID = 3;
```
```sql
SET @num := 0;
UPDATE punjab_uni SET stuID = @num := (@num+1);
ALTER TABLE punjab_uni AUTO_INCREMENT =1;
```
## SELECT Clause
We will use the sample database from here: https://www.mysqltutorial.org/mysql-sample-database.aspx
#### Select Database
```sql
USE classicmodels; 
```
#### Select all Columns of Customers Table
```sql
SELECT * FROM customers; 
```
#### Select only customer name column from Customers Table
```sql
SELECT customerName FROM customers;
```
#### Select only customer name along with Phone number from Customers Table
```sql
SELECT customerName, phone FROM customers;
```
#### Select multiple columns from Customers Table
```sql
SELECT customerName, phone, city, state FROM customers;
```
#### Using multiple clauses at the same time
```sql
SELECT customerName, phone, city, state 
FROM customers
WHERE city = "paris"
ORDER BY customerName;
```

#### Commenting (Disabling) a clause
```sql
SELECT customerName, phone, city, state 
FROM customers
-- WHERE city = "paris"
ORDER BY customerName;
```

## WHERE Clause
### Comparion Operators
<ul>
	<li>=</li>
	<li>!=</li>
	<li><></li>
	<li>></li>
	<li><</li>
	<li>>=</li>
	<li><=</li>
</ul>

```sql
SELECT * FROM customers
WHERE city = "Singapore";
```
```sql
SELECT * FROM customers
WHERE city != "Singapore";
```
```sql
SELECT * FROM customers
WHERE city <> "Singapore"
AND contactLastName = "Schmitt";
```
```sql
SELECT * FROM customers
WHERE creditLimit > 112500;
```
```sql
SELECT * FROM products
WHERE MSRP > 120;
```

## Data Manipulation
#### Arithmetic operations on columns
```sql
SELECT productName,
	productCode,
        buyPrice,
        MSRP,
        (MSRP + 10) * 1.2
FROM products;
```
#### Assigning Alias to a column
```sql
SELECT productName,
	productCode,
        buyPrice,
        MSRP,
        (MSRP + 10) * 1.2 AS MSRP_adjusted
FROM products;
```
#### Increasing MSRP column and assigning Alias
```sql
SELECT productName, productCode, buyPrice, MSRP,
	(110/100)*MSRP AS "MSRP 10%",
        (120/100)*MSRP AS "MSRP 20%",
        (100.5/100)*MSRP AS "MSRP 0.5%"
FROM products;
```
## Logical opeartors and conditional clauses
### Logical Operators
<ul>
	<li>AND</li>
	<li>OR</li>
	<li>NOT</li>
</ul>

#### Using AND and OR logical operators
```sql
SELECT * FROM products
WHERE productLine = "Motorcycles"
OR (buyPrice > 65 AND MSRP > 100);
```
#### Using NOT to reverse the conditions
```sql
SELECT * FROM products
WHERE productLine = "Motorcycles"
AND NOT buyPrice > 65 AND NOT MSRP > 100;
```
#### Using multiple OR operators
```sql
SELECT * FROM products
WHERE productLine = "Motorcycles"
OR productLine = "Classic cars"
OR productLine = "Trucks and Buses";
```
### Conditional Clauses
<ul>
	<li>IN</li>
	<li>BETWEEN</li>
	<li>LIKE</li>
</ul>

#### Using IN clause instead of multiple OR operators for a single column
```sql
SELECT * FROM products
WHERE productLine IN ("Motorcycles", "Classic cars", "Trucks and Buses");
```
#### Using NOT to reverse the IN clause
```sql
SELECT * FROM products
WHERE productLine NOT IN ("Motorcycles", "Classic cars", "Trucks and Buses");
```

## Order By (Sort)

```sql
SELECT * FROM users ORDER BY last_name ASC;
SELECT * FROM users ORDER BY last_name DESC;
```

## Concatenate Columns

```sql
SELECT CONCAT(first_name, ' ', last_name) AS 'Name', dept FROM users;

```

## Select Distinct Rows

```sql
SELECT DISTINCT location FROM users;

```

## Between (Select Range)

```sql
SELECT * FROM users WHERE age BETWEEN 20 AND 25;
```

## Like (Searching)

```sql
SELECT * FROM users WHERE dept LIKE 'd%';
SELECT * FROM users WHERE dept LIKE 'dev%';
SELECT * FROM users WHERE dept LIKE '%t';
SELECT * FROM users WHERE dept LIKE '%e%';
```

## Not Like

```sql
SELECT * FROM users WHERE dept NOT LIKE 'd%';
```

## IN

```sql
SELECT * FROM users WHERE dept IN ('design', 'sales');
```

## Create & Remove Index

```sql
CREATE INDEX LIndex On users(location);
DROP INDEX LIndex ON users;
```

## New Table With Foreign Key (Posts)

```sql
CREATE TABLE posts(
id INT AUTO_INCREMENT,
   user_id INT,
   title VARCHAR(100),
   body TEXT,
   publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
   PRIMARY KEY(id),
   FOREIGN KEY (user_id) REFERENCES users(id)
);
```

## Add Data to Posts Table

```sql
INSERT INTO posts(user_id, title, body) VALUES (1, 'Post One', 'This is post one'),(3, 'Post Two', 'This is post two'),(1, 'Post Three', 'This is post three'),(2, 'Post Four', 'This is post four'),(5, 'Post Five', 'This is post five'),(4, 'Post Six', 'This is post six'),(2, 'Post Seven', 'This is post seven'),(1, 'Post Eight', 'This is post eight'),(3, 'Post Nine', 'This is post none'),(4, 'Post Ten', 'This is post ten');
```

## INNER JOIN

```sql
SELECT
  users.first_name,
  users.last_name,
  posts.title,
  posts.publish_date
FROM users
INNER JOIN posts
ON users.id = posts.user_id
ORDER BY posts.title;
```

## New Table With 2 Foriegn Keys

```sql
CREATE TABLE comments(
	id INT AUTO_INCREMENT,
    post_id INT,
    user_id INT,
    body TEXT,
    publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY(id),
    FOREIGN KEY(user_id) references users(id),
    FOREIGN KEY(post_id) references posts(id)
);
```

## Add Data to Comments Table

```sql
INSERT INTO comments(post_id, user_id, body) VALUES (1, 3, 'This is comment one'),(2, 1, 'This is comment two'),(5, 3, 'This is comment three'),(2, 4, 'This is comment four'),(1, 2, 'This is comment five'),(3, 1, 'This is comment six'),(3, 2, 'This is comment six'),(5, 4, 'This is comment seven'),(2, 3, 'This is comment seven');
```

## Left Join

```sql
SELECT
comments.body,
posts.title
FROM comments
LEFT JOIN posts ON posts.id = comments.post_id
ORDER BY posts.title;

```

## Join Multiple Tables

```sql
SELECT
comments.body,
posts.title,
users.first_name,
users.last_name
FROM comments
INNER JOIN posts on posts.id = comments.post_id
INNER JOIN users on users.id = comments.user_id
ORDER BY posts.title;

```

## Aggregate Functions

```sql
SELECT COUNT(id) FROM users;
SELECT MAX(age) FROM users;
SELECT MIN(age) FROM users;
SELECT SUM(age) FROM users;
SELECT UCASE(first_name), LCASE(last_name) FROM users;

```

## Group By

```sql
SELECT age, COUNT(age) FROM users GROUP BY age;
SELECT age, COUNT(age) FROM users WHERE age > 20 GROUP BY age;
SELECT age, COUNT(age) FROM users GROUP BY age HAVING count(age) >=2;

```
