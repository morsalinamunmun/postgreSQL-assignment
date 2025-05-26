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

## 3. Explain the Primary Key and Foreign Key concepts in PostgreSQL.
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