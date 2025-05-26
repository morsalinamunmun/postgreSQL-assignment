# postgreSQL-assignment
## 1. What is PostgreSQL?
Ans: PostgreSQL is a powerful open-source object-relational database system. It helps manage databases efficiently, allowing users to easily create, store, and organize data. PostgreSQL plays a vital role in defining table structures and ensuring data integrity.

**Key Features:**
**Open source:** PostgreSQL is a free to used, modify & distributed.
**Object Relational:** The relational database is object oriented features supports.
**SQL:** The SQL used for managing data and querying.
**Support JSON & NoSQL:** Store & query json data, allowing NoSQL data functionality.
**Advanced Data Types:** Beyond standard SQL types, PostgreSQL supports JSON, arrays, geometric types, and custom data types.
**Extensibility**: You can add custom functions, operators, and even create your own data types.

## History: 
Started as the POSTGRES Project at UC Berkeley in 1986
Used a query language called "PostQUEL"
In 1994, became Postgres95 with SQL support replacing PostQUEL
Eventually renamed to PostgreSQL to reflect SQL capabilities
Many people still call it "Postgres" for simplicity

## Usage:
- This system Well for small & large applications
- Supports fo complex queries & joins.
- excellent performance optimization features
- Integrates well with popular frameworks and cloud platforms & Offers robust security features
- PostgreSQl uses more applications, so, Web applications, Mobile applications, Data warehousing, financial application.

**Example with SQL:**
```sql
-- Creating a table
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
);

-- Inserting data
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');

-- Querying data
SELECT * FROM users;
```

## 2. Explain the Primary Key and Foreign Key concepts in PostgreSQL.
Ans: Primary keys and foreign keys are fundamental concepts in relational databases that help maintain data integrity and establish relationships between tables.
**Primary Key:** A primary key is a unique value that is used to find a specific row of data in a table.
**Key Characteristics:** 
- No two rows can have the same primary key value.
- Primary key values cannot be NULL.
- Each table can have only one primary key
**Example:**
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,  -- Auto-incrementing primary key
    email VARCHAR(100) UNIQUE NOT NULL,
    name VARCHAR(50) NOT NULL
);
```
PostgreSQL provides `SERIAL` as a convenient way to create auto-incrementing primary keys
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    order_details TEXT
);

INSERT INTO orders (order_details)
VALUES ('Order-1'), ('Order-2'), ('Order-3');
```

**Foreign Keys:** A foreign key is a column (or combination of columns) that creates a link between two tables by referencing the primary key of another table.

### Key Characters:
- Points to a primary key in a different table.
- Ensures referenced records exist.
- A table can have multiple foreign keys

### Example:

```sql
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INTEGER REFERENCES customers(customer_id),
    order_date DATE NOT NULL
);
```

**Relationships Type:** This type of relationship , One-to-Many, Many-to-Many
**One-to-Many:** The most common relationship where one record in the parent table can have multiple related records in the child table.
```sql
-- One customer can have many orders
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    customer_id INTEGER REFERENCES customers(id),
    total DECIMAL(10,2)
);
```
**Many-to-Many:** Requires a junction table to connect two tables.
```sql
-- Students and courses (many-to-many)
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE courses (
    id SERIAL PRIMARY KEY,
    title VARCHAR(100)
);

CREATE TABLE enrollments (
    student_id INTEGER REFERENCES students(id),
    course_id INTEGER REFERENCES courses(id),
    PRIMARY KEY (student_id, course_id)
);
```
### Benefit: 
**Data Integrity**: Prevents orphaned records and maintains consistent relationships
**Performance**: Primary keys automatically create indexes for faster queries
**Referential Integrity**: Foreign keys ensure data consistency across tables
**Query Optimization**: Database can optimize joins using key relationships

## 3. What is the difference between the VARCHAR and CHAR data types?
Both VARCHAR and CHAR are character data types in PostgreSQL
**VARCHAR:** VARCHAR has a variable size & data type stores variable formate. 

**Key Features**
- Uses only the space needed for the actual string.
- Stores the exact string without adding spaces.
- Cannot exceed the specified characters

### Example
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50),    
    email VARCHAR(100)    
);

INSERT INTO users (username, email) 
VALUES ('Moon', 'moon@gail.com');
```
### CHAR: 
CHAR has a fixed length. CHAR values are padded with spaces count length.

**Key Features**
- Always uses exactly characters of storage.
- If the string is shorter than `n`, it's padded with spaces.
- Minimal overhead since length is fixed.
- Cannot exceed the specified `n` characters.

### Example: 
```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    product_code CHAR(10), 
    name VARCHAR(100)
);

INSERT INTO products (product_code, name) 
VALUES ('ABC123', 'Widget');
```

## 4. Explain the purpose of the WHERE clause in a SELECT statement.
Ans: The WHERE clause is used to filter data in a SELECT statement, allowing you to retrieve only the rows that meet specific conditions. Without a WHERE clause, a SELECT statement returns all rows from a table. This is allow only select data.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
### **Data filtering:**
only the data you need instead of all rows:
```sql
SELECT * FROM users WHERE age > 18;
```
### **Performance Optimization:**
Reduces the amount of data processed and transferred:

```sql
SELECT name, email FROM users WHERE city = 'New York';
```
### **Precise Data Retrieval:**
Get exactly the information you're looking for:

```sql
SELECT * FROM users WHERE username = 'john_doe';
```

### **WHERE Clause Examples**
### Exact Match Filtering

```sql
SELECT * FROM users WHERE username = 'alex';
```

### Range Filtering

```sql
SELECT * FROM orders WHERE order_date BETWEEN '2023-01-01' AND '2023-01-31';
SELECT * FROM products WHERE price > 100 AND price < 500;
```

### List-Based Filtering

```sql
SELECT * FROM products WHERE category_id IN (1, 2, 5);

SELECT * FROM employees WHERE department_id NOT IN (3, 4);
```

### Pattern Matching

```sql
SELECT * FROM customers WHERE email LIKE '%@gmail.com';
SELECT * FROM products WHERE name LIKE '%widget%';
```

### NULL Value Handling

```sql
SELECT * FROM users WHERE last_login IS NULL;
SELECT * FROM users WHERE phone_number IS NOT NULL;
```
### Combining Multiple Conditions

```sql
SELECT * FROM sales 
WHERE amount > 500 
  AND sales_date >= '2023-01-01' 
  AND sales_date <= '2023-01-31';

SELECT * FROM users 
WHERE city = 'New York' 
   OR city = 'Los Angeles' 
   OR city = 'Chicago';

SELECT * FROM products 
WHERE (category = 'Electronics' OR category = 'Computers') 
  AND price < 1000;
```

### Subqueries in WHERE

```sql
SELECT * FROM orders 
WHERE customer_id IN (
    SELECT customer_id 
    FROM customers 
    WHERE country = 'Spain'
);
```