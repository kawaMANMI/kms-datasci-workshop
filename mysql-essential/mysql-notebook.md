# MySQL Essential Training Notebook

## Table of Contents
1. [Part 1: Installation and Configuration](#part-1-installation-and-configuration)
   - MySQL Server Installation
   - MySQL Workbench Installation
   - Basic Server Configuration
   - Security Setup
   - Environmental Variables

2. [Part 2: Essential MySQL Commands](#part-2-essential-mysql-commands)
   - User Management
   - Database Operations
   - Table Operations
   - CRUD Operations
   - Advanced Queries
   - Joins and Relationships
   - Functions and Aggregates

## Part 1: Installation and Configuration

### Prerequisites
- Operating System Requirements
  - Windows: Windows 10 or later
  - Mac: macOS 10.15 or later
  - Linux: Most modern distributions

### Installation Steps

#### MySQL Server Installation
1. Download MySQL Server
   - Visit mysql.com/downloads
   - Choose MySQL Community Server
   - Select version appropriate for your OS

2. Installation Process
   - Windows:
     ```bash
     # Run MSI installer
     # Choose "Developer Default" for complete installation
     # Set root password during installation
     ```
   - Mac:
     ```bash
     # Using Homebrew
     brew install mysql
     
     # Start MySQL Service
     brew services start mysql
     ```
   - Linux (Ubuntu):
     ```bash
     sudo apt update
     sudo apt install mysql-server
     sudo systemctl start mysql
     ```

3. Verify Installation
   ```bash
   mysql --version
   ```

### Basic Configuration

1. MySQL Configuration File Location
   - Windows: `C:\ProgramData\MySQL\MySQL Server 8.0\my.ini`
   - Mac: `/usr/local/etc/my.cnf`
   - Linux: `/etc/mysql/my.cnf`

2. Essential Configuration Parameters
   ```ini
   [mysqld]
   # Network
   port=3306
   bind-address=127.0.0.1
   
   # Storage
   datadir=/var/lib/mysql
   
   # Character Set
   character-set-server=utf8mb4
   collation-server=utf8mb4_unicode_ci
   ```

3. Environment Setup
   ```bash
   # Add MySQL to PATH
   # Windows
   SET PATH=%PATH%;C:\Program Files\MySQL\MySQL Server 8.0\bin
   
   # Mac/Linux
   export PATH=${PATH}:/usr/local/mysql/bin
   ```

### Security Setup

1. Initial Security Configuration
   ```bash
   # Secure Installation
   mysql_secure_installation
   ```

2. Basic Security Measures
   - Change root password
   - Remove anonymous users
   - Disable remote root login
   - Remove test database

## Part 2: Essential MySQL Commands

### User Management

1. Login to MySQL
   ```sql
   mysql -u root -p
   ```

2. Create and Manage Users
   ```sql
   -- Create new user
   CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
   
   -- Grant privileges
   GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost';
   FLUSH PRIVILEGES;
   
   -- Show users
   SELECT User, Host FROM mysql.user;
   
   -- Remove user
   DROP USER 'username'@'localhost';
   ```

### Database Operations

1. Database Management
   ```sql
   -- Show databases
   SHOW DATABASES;
   
   -- Create database
   CREATE DATABASE database_name;
   
   -- Select database
   USE database_name;
   
   -- Delete database
   DROP DATABASE database_name;
   ```

### Table Operations

1. Create and Modify Tables
   ```sql
   -- Create table
   CREATE TABLE users (
       id INT AUTO_INCREMENT,
       username VARCHAR(50) NOT NULL,
       email VARCHAR(100) NOT NULL,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       PRIMARY KEY (id)
   );
   
   -- Show tables
   SHOW TABLES;
   
   -- Describe table structure
   DESCRIBE users;
   
   -- Add column
   ALTER TABLE users ADD COLUMN phone VARCHAR(15);
   
   -- Modify column
   ALTER TABLE users MODIFY COLUMN phone VARCHAR(20);
   
   -- Drop table
   DROP TABLE users;
   ```

### CRUD Operations

1. Create (Insert) Data
   ```sql
   -- Single row insert
   INSERT INTO users (username, email) 
   VALUES ('john_doe', 'john@example.com');
   
   -- Multiple rows insert
   INSERT INTO users (username, email) VALUES 
   ('jane_doe', 'jane@example.com'),
   ('bob_smith', 'bob@example.com');
   ```

2. Read (Select) Data
   ```sql
   -- Select all
   SELECT * FROM users;
   
   -- Select specific columns
   SELECT username, email FROM users;
   
   -- Conditional select
   SELECT * FROM users WHERE id > 5;
   
   -- Ordered select
   SELECT * FROM users ORDER BY username ASC;
   
   -- Limited select
   SELECT * FROM users LIMIT 5;
   ```

3. Update Data
   ```sql
   -- Update records
   UPDATE users 
   SET email = 'newemail@example.com' 
   WHERE username = 'john_doe';
   ```

4. Delete Data
   ```sql
   -- Delete records
   DELETE FROM users WHERE id = 1;
   ```

### Advanced Queries

1. WHERE Clause Operators
   ```sql
   -- Comparison operators
   SELECT * FROM products WHERE price > 100;
   SELECT * FROM products WHERE price BETWEEN 50 AND 100;
   SELECT * FROM users WHERE email LIKE '%@gmail.com';
   
   -- Logical operators
   SELECT * FROM products 
   WHERE price > 100 AND category = 'Electronics';
   ```

2. Sorting and Filtering
   ```sql
   -- Order by multiple columns
   SELECT * FROM users 
   ORDER BY last_name ASC, first_name DESC;
   
   -- Group by with having
   SELECT category, COUNT(*) as count 
   FROM products 
   GROUP BY category 
   HAVING count > 5;
   ```

### Joins and Relationships

1. Types of Joins
   ```sql
   -- Inner join
   SELECT orders.id, users.username 
   FROM orders 
   INNER JOIN users ON orders.user_id = users.id;
   
   -- Left join
   SELECT users.username, orders.id 
   FROM users 
   LEFT JOIN orders ON users.id = orders.user_id;
   ```

2. Multiple Table Joins
   ```sql
   SELECT orders.id, users.username, products.name 
   FROM orders 
   INNER JOIN users ON orders.user_id = users.id 
   INNER JOIN products ON orders.product_id = products.id;
   ```

### Functions and Aggregates

1. String Functions
   ```sql
   SELECT CONCAT(first_name, ' ', last_name) as full_name FROM users;
   SELECT UPPER(username) FROM users;
   SELECT SUBSTRING(description, 1, 50) FROM products;
   ```

2. Numeric Functions
   ```sql
   SELECT ROUND(price, 2) FROM products;
   SELECT ABS(balance) FROM accounts;
   ```

3. Aggregate Functions
   ```sql
   SELECT COUNT(*) FROM users;
   SELECT AVG(price) FROM products;
   SELECT MAX(price) FROM products;
   SELECT MIN(price) FROM products;
   SELECT SUM(quantity) FROM order_items;
   ```

### Best Practices

1. Performance
   - Use appropriate indexes
   - Avoid SELECT *
   - Use EXPLAIN to analyze queries
   - Regularly optimize tables

2. Security
   - Use prepared statements
   - Implement proper access controls
   - Regular backups
   - Keep MySQL updated

3. Maintenance
   ```sql
   -- Optimize tables
   OPTIMIZE TABLE tablename;
   
   -- Check table
   CHECK TABLE tablename;
   
   -- Repair table
   REPAIR TABLE tablename;
   ```

This notebook serves as a comprehensive guide for MySQL essentials, from installation to advanced operations. Keep it handy as a reference for your MySQL development journey.
