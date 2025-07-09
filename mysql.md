# MySQL - Database Notes

## 1. Introduction to MySQL

### What is MySQL?
- An open-source **Relational Database Management System (RDBMS)**.
- Widely used for web applications (part of LAMP/LEMP stack: Linux, Apache/Nginx, MySQL, PHP/Python/Perl).
- Known for its speed, reliability, and ease of use.
- Owned by Oracle Corporation.

### Key Characteristics
- **Client-Server Architecture**: MySQL server manages databases, clients connect to it.
- **Multi-user access**: Supports many concurrent users.
- **Scalability**: Can handle small websites to large-scale applications.
- **Portability**: Runs on various operating systems (Linux, Windows, macOS, etc.).
- **SQL Compliance**: Adheres to SQL standard, with some MySQL-specific extensions.

## 2. MySQL Architecture Overview

### Main Components
- **MySQL Server (mysqld)**: The core daemon that handles all database operations.
- **Storage Engines**: Pluggable modules that manage how data is stored and retrieved. (Crucial for MySQL!)
- **Connectors**: Libraries that allow applications in various languages (Python, PHP, Java, Node.js) to connect to MySQL.
- **Client Programs**: Command-line tools (e.g., `mysql`, `mysqldump`) or GUI tools (e.g., MySQL Workbench).

### Communication Protocol
- Uses TCP/IP for network communication.
- Can also use Unix sockets for local connections (faster).

## 3. Core Concepts & Data Types

### Databases & Tables
- A **database** in MySQL is a collection of related tables. Also called a **schema**.
- A **table** is a collection of related data organized in rows and columns.

### Common MySQL Data Types
- **Numeric Types**:
    - `INT` (or `INTEGER`): Typical whole numbers, default length usually 11.
    - `TINYINT`, `SMALLINT`, `MEDIUMINT`, `BIGINT`: For whole numbers, varying ranges (e.g., `TINYINT` is -128 to 127 signed, or 0 to 255 unsigned).
    - `FLOAT`, `DOUBLE`: For approximate floating-point numbers.
    - `DECIMAL(M,D)`: For exact fixed-point numbers (e.g., currency). `M` is total digits, `D` is digits after decimal.
        - **Example**: `DECIMAL(5,2)` can store `999.99`.
- **String Types**:
    - `VARCHAR(L)`: Variable-length string, `L` max characters (up to 65,535 for a row). Most common.
    - `CHAR(L)`: Fixed-length string, padded with spaces up to `L` characters.
    - `TEXT`, `TINYTEXT`, `MEDIUMTEXT`, `LONGTEXT`: For large text blocks (up to 4GB for `LONGTEXT`).
    - `BLOB`, `TINYBLOB`, `MEDIUMBLOB`, `LONGBLOB`: For binary large objects (e.g., images).
- **Date and Time Types**:
    - `DATE`: 'YYYY-MM-DD'.
    - `TIME`: 'HH:MM:SS'.
    - `DATETIME`: 'YYYY-MM-DD HH:MM:SS' (fixed range, no timezone conversion).
    - `TIMESTAMP`: 'YYYY-MM-DD HH:MM:SS' (stores as UTC, converts to session timezone; range up to ~2038). Often used for recording creation/update times automatically.
    - `YEAR`: 'YYYY'.
- **Enum & Set Types**:
    - `ENUM('val1', 'val2', ...)`: A string column that can only have *one* value from a predefined list.
        - **Example**: `ShirtSize ENUM('S', 'M', 'L', 'XL')`
    - `SET('val1', 'val2', ...)`: A string column that can have *zero or more* values from a predefined list.
        - **Example**: `Skills SET('Java', 'Python', 'SQL')`

## 4. Storage Engines - The MySQL Differentiator

### What are Storage Engines?
- Components of MySQL that handle the actual data storage and retrieval.
- You can specify a different engine for each table.

### Key Storage Engines
1.  **InnoDB (Default and Recommended)**:
    - **ACID Compliant**: Supports Atomicity, Consistency, Isolation, Durability.
    - **Transactions**: Full support for `COMMIT` and `ROLLBACK`.
    - **Foreign Keys**: Enforces referential integrity.
    - **Row-Level Locking**: Allows high concurrency (multiple users can modify different rows in the same table simultaneously).
    - **Crash Recovery**: Uses a transaction log for recovery.
    - **Recommended for general-purpose OLTP (Online Transaction Processing) workloads.**

2.  **MyISAM (Older, but still used for specific cases)**:
    - **NOT ACID Compliant**: No transaction support, no foreign keys.
    - **Table-Level Locking**: Only one user can write to the table at a time.
    - **Faster for Read-Heavy Workloads**: Historically, simpler design meant faster reads for certain simple queries.
    - **Full-Text Search**: Native support for full-text indexing (though InnoDB now has it too).
    - **Crash Recovery**: Less robust; requires `CHECK TABLE`/`REPAIR TABLE` after crashes.
    - **Use Case**: Often for logging tables, data warehouses where writes are batched and integrity isn't paramount, or very simple read-only tables.

### How to specify/check Storage Engine:
- When creating a table: `CREATE TABLE my_table (id INT) ENGINE = InnoDB;`
- To check existing table: `SHOW CREATE TABLE my_table;` or `SHOW TABLE STATUS LIKE 'my_table';`

## 5. MySQL Specific SQL & Commands

### Basic Server Interaction (Command Line Client `mysql`)
- Connect to MySQL: `mysql -u username -p` (will prompt for password)
- Show databases: `SHOW DATABASES;`
- Select a database: `USE database_name;` (must select before accessing tables)
- Show tables in current database: `SHOW TABLES;`
- Describe table structure: `DESCRIBE table_name;` or `SHOW COLUMNS FROM table_name;`
- Show server status: `STATUS;` or `\s`
- Exit: `EXIT;` or `\q`

### DDL (Data Definition Language)
- **Database Operations**:
    ```sql
    CREATE DATABASE my_company_db;
    DROP DATABASE my_company_db; -- CAUTION: Deletes all tables and data!
    ALTER DATABASE my_company_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    ```
- **Table Operations**:
    - **Creating a Table**:
    ```sql
    CREATE TABLE Products (
        ProductID INT PRIMARY KEY AUTO_INCREMENT, -- AUTO_INCREMENT for auto-generated unique IDs
        ProductName VARCHAR(255) NOT NULL,       -- Cannot be NULL
        Price DECIMAL(10, 2) DEFAULT 0.00,       -- Default value if not specified
        QuantityInStock INT UNSIGNED,            -- UNSIGNED for non-negative integers
        LastUpdated TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP, -- Auto-updates on row modification
        Category ENUM('Electronics', 'Books', 'Food'),
        INDEX (ProductName)                      -- Create an index on ProductName
    ) ENGINE=InnoDB;                             -- Specify storage engine
    ```
    - **Modifying a Table**:
    ```sql
    ALTER TABLE Products ADD COLUMN Description TEXT;
    ALTER TABLE Products DROP COLUMN Category;
    ALTER TABLE Products MODIFY COLUMN Price DECIMAL(12, 2) NOT NULL; -- Change type and add NOT NULL
    ALTER TABLE Products RENAME TO InventoryItems;
    ```
    - **Deleting all data / Dropping table**:
    ```sql
    TRUNCATE TABLE Products; -- Deletes all rows, resets AUTO_INCREMENT, faster than DELETE FROM. DDL operation.
    DROP TABLE Products;     -- Deletes the table structure and all data.
    ```
- **Indexes**:
    ```sql
    CREATE INDEX idx_product_name ON Products (ProductName);
    CREATE UNIQUE INDEX idx_product_code ON Products (ProductCode); -- Ensures ProductCode is unique across rows
    DROP INDEX idx_product_name ON Products;
    ```

### DML (Data Manipulation Language)

-   **`INSERT` Statements**: Add new rows.
    ```sql
    -- Insert specific values for all columns (order must match table definition)
    INSERT INTO Customers VALUES (1, 'Alice', 'Smith', 'alice@example.com');

    -- Insert specific values for selected columns
    INSERT INTO Customers (FirstName, LastName, Email) VALUES ('Bob', 'Johnson', 'bob@example.com');

    -- Insert multiple rows
    INSERT INTO Products (ProductName, Price) VALUES
    ('Laptop', 1200.00),
    ('Mouse', 25.00),
    ('Keyboard', 75.00);
    ```

-   **`SELECT` Statements**: Retrieve data.
    ```sql
    -- Select all columns from a table
    SELECT * FROM Customers;

    -- Select specific columns
    SELECT FirstName, Email FROM Customers;

    -- Select with WHERE clause (filtering rows)
    SELECT * FROM Products WHERE Price > 1000;
    SELECT * FROM Customers WHERE LastName = 'Smith';
    SELECT * FROM Orders WHERE OrderDate > '2024-01-01' AND TotalAmount < 500;
    SELECT * FROM Products WHERE ProductName LIKE '%book%'; -- Case-insensitive search (default for many collations)
    SELECT * FROM Customers WHERE Age BETWEEN 20 AND 30;
    SELECT * FROM Orders WHERE CustomerID IN (1, 3, 5);
    ```
    -   **`DISTINCT`**: Eliminating duplicate rows.
        ```sql
        SELECT DISTINCT Category FROM Products;
        ```
    -   **`ORDER BY`**: Sorting results. `ASC` (ascending, default) or `DESC` (descending).
        ```sql
        SELECT ProductName, Price FROM Products ORDER BY Price DESC; -- Highest price first
        SELECT ProductName, Price FROM Products ORDER BY ProductName ASC, Price DESC; -- Sort by name, then by price if names are same
        ```
    -   **`LIMIT` Clause**: Restricting the number of results. Used for pagination.
        ```sql
        SELECT * FROM Orders LIMIT 5; -- Get first 5 rows
        SELECT * FROM Orders LIMIT 10 OFFSET 20; -- Get 10 rows starting from row 21 (for page 3, if 10 items per page)
        ```

-   **`UPDATE` Statements**: Modify existing data.
    ```sql
    UPDATE Customers SET Email = 'new.alice@example.com' WHERE CustomerID = 1;
    UPDATE Products SET Price = Price * 1.05 WHERE Category = 'Electronics'; -- Increase price by 5%
    ```

-   **`DELETE` Statements**: Remove rows.
    ```sql
    DELETE FROM Customers WHERE CustomerID = 2;
    DELETE FROM Orders WHERE OrderDate < '2023-01-01';
    DELETE FROM Products; -- Deletes all rows (slower than TRUNCATE)
    ```

### MySQL-Specific Functions & Features
- **`AUTO_INCREMENT`**: Automatically generates unique numbers for a primary key.
    - **Example**: `ProductID INT PRIMARY KEY AUTO_INCREMENT`
    - To get last inserted ID (per connection): `SELECT LAST_INSERT_ID();`
- **String Functions**:
    - `CONCAT(str1, str2, ...)`: Concatenates strings. `SELECT CONCAT(FirstName, ' ', LastName) AS FullName FROM Customers;`
    - `LENGTH(str)`: Returns length of string.
    - `SUBSTRING(str, start, length)`: Extracts a substring.
    - `UPPER(str)`, `LOWER(str)`: Converts to upper/lower case.
    - `TRIM(str)`: Removes leading/trailing spaces.
- **Date/Time Functions**:
    - `NOW()`: Current date and time.
    - `CURDATE()`: Current date.
    - `CURTIME()`: Current time.
    - `DATEDIFF(date1, date2)`: Difference in days.
    - `DATE_FORMAT(date, format)`: Formats a date. `SELECT DATE_FORMAT(OrderDate, '%Y-%m-%d %H:%i') FROM Orders;`
    - `DATE_ADD(date, INTERVAL expr unit)`, `DATE_SUB(date, INTERVAL expr unit)`: Add/subtract time.
        - **Example**: `SELECT DATE_ADD(CURDATE(), INTERVAL 7 DAY);`
- **Conditional Logic**:
    - `IF(condition, value_if_true, value_if_false)`: Simple conditional.
        - **Example**: `SELECT ProductName, IF(Price > 100, 'Expensive', 'Affordable') AS PriceStatus FROM Products;`
    - `CASE WHEN ... THEN ... ELSE ... END`: More complex conditional.
        ```sql
        SELECT ProductName,
            CASE
                WHEN Price > 1000 THEN 'Very Expensive'
                WHEN Price > 100 THEN 'Expensive'
                ELSE 'Affordable'
            END AS PriceCategory
        FROM Products;
        ```
- **Aggregate Functions**: (`COUNT`, `SUM`, `AVG`, `MAX`, `MIN`)
    - `GROUP BY`: Groups rows for aggregation. `SELECT Category, AVG(Price) FROM Products GROUP BY Category;`
    - `HAVING`: Filters groups. `SELECT Category, COUNT(*) FROM Products GROUP BY Category HAVING COUNT(*) > 5;`
- **`GROUP_CONCAT()`**: Concatenates strings from a group into a single string.
    - **Example**: `SELECT DeptID, GROUP_CONCAT(Name ORDER BY Name SEPARATOR ', ') AS EmployeesInDept FROM Employees GROUP BY DeptID;`
- **`NULLIF()`**: Returns NULL if two expressions are equal, otherwise the first expression.
- **`COALESCE()`**: Returns the first non-NULL expression in a list.
    - **Example**: `SELECT COALESCE(PhoneNumber, Email, 'N/A') FROM Customers;` (Returns phone, if null then email, if both null then 'N/A').

## 6. Indexing in MySQL

### Types of Indexes (conceptually)
- **Primary Key Index**: Automatically created on the primary key, usually a clustered index for InnoDB.
- **Secondary Indexes**: All other indexes.
    - **Unique Index**: Ensures all values in the indexed column(s) are unique.
    - **Full-Text Index**: For searching large text blocks (MyISAM, and now InnoDB).

### How InnoDB Uses Indexes
- **Clustered Index**: The primary key index physically orders the data rows in the table. There can be only one per table.
    - If no primary key is defined, InnoDB creates a hidden clustered index (gen_clust_idx).
- **Secondary Indexes**: Store the indexed column(s) value and the *primary key value* (not direct row pointers like MyISAM). This means a lookup via a secondary index first finds the primary key, then uses the clustered index to find the actual row.

### `EXPLAIN` Statement
- Essential tool for query optimization. Shows how MySQL executes a `SELECT` query.
    ```sql
    EXPLAIN SELECT * FROM Customers WHERE City = 'New York';
    ```
- **Key Columns in `EXPLAIN` Output**:
    - `id`: Query part ID.
    - `select_type`: Type of select query (SIMPLE, PRIMARY, SUBQUERY, UNION).
    - `table`: The table name.
    - `type`: **Join type (MOST IMPORTANT)**. Indicates how tables are scanned.
        - `ALL`: Full table scan (bad for large tables).
        - `index`: Full index scan (better than `ALL`, but still reads entire index).
        - `range`: Index range scan (good for `WHERE` clauses on indexed columns using ranges like `>`, `<`, `BETWEEN`).
        - `ref`: Non-unique index lookup (good for equality matches).
        - `eq_ref`: Unique index lookup (very good, joins unique indexes).
        - `const`/`system`: Fastest, for single matching row.
    - `possible_keys`: Indexes MySQL *could* use.
    - `key`: Index MySQL *actually* chose.
    - `rows`: Estimated number of rows examined. (Lower is better).
    - `Extra`: Additional information (e.g., "Using where", "Using index" (covering index), "Using filesort" (needs sorting), "Using temporary" (needs temp table)).

## 7. User Management & Security

### Creating Users & Granting Privileges
- **Creating a User**:
    ```sql
    -- User accessible only from the local machine
    CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'MySecurePassword!';
    -- User accessible from any host (less secure, use with caution)
    CREATE USER 'app_user'@'%' IDENTIFIED BY 'AnotherPassword';
    ```
- **Granting Privileges**:
    ```sql
    -- Grant SELECT, INSERT, UPDATE, DELETE on the 'products' table in 'my_db' database
    GRANT SELECT, INSERT, UPDATE, DELETE ON my_db.products TO 'myuser'@'localhost';
    -- Grant all privileges on all tables in 'my_db' database
    GRANT ALL PRIVILEGES ON my_db.* TO 'app_user'@'%';
    -- Grant global privileges (e.g., CREATE, DROP on any database/table)
    GRANT CREATE, DROP ON *.* TO 'dba_user'@'localhost';
    ```
- **Revoking Privileges**:
    ```sql
    REVOKE DELETE ON my_db.products FROM 'myuser'@'localhost';
    ```
- **Applying Changes**: `FLUSH PRIVILEGES;` (Reloads grant tables, necessary after direct manipulation of `mysql.user` tables).

### Security Best Practices
- **Strong Passwords**: For all users, especially root.
- **Least Privilege**: Grant only necessary permissions.
- **Limit Host Access**: Restrict user accounts to specific IPs (`'user'@'localhost'`, `'user'@'192.168.1.100'`).
- **SQL Injection Prevention**: **Crucial for web applications.** Use **Prepared Statements** (e.g., in PHP using `PDO`, Python using `psycopg2` or `mysql.connector`). **Never concatenate user input directly into SQL queries.**
    - **Example (Vulnerable)**: `SELECT * FROM users WHERE username = '` + userInput + `' AND password = '` + userPass + `'`;
    - **Example (Secure with Prepared Statement)**: `SELECT * FROM users WHERE username = ? AND password = ?` (parameters are sent separately and not interpreted as SQL code).
- **Regular Backups**: Crucial for disaster recovery.
- **Encrypt Sensitive Data**: At rest (e.g., disk encryption) and in transit (SSL/TLS for client connections).
- **Keep MySQL Updated**: Apply security patches regularly.

## 8. Backup & Recovery

### Logical Backups (`mysqldump`)
- Creates SQL statements to recreate the database (useful for migrating or restoring to different MySQL versions/servers).
- **Full Backup of a single database**:
    ```bash
    mysqldump -u username -p my_db > my_db_backup.sql
    ```
- **Backup all databases**:
    ```bash
    mysqldump -u username -p --all-databases > all_databases_backup.sql
    ```
- **Restoring a database from a dump file**:
    ```bash
    mysql -u username -p my_db < my_db_backup.sql
    ```
    (Or create the database first: `CREATE DATABASE my_db;` then run the command).

### Binary Log (BinLog) - For Point-in-Time Recovery & Replication
- Records all data-modifying operations (DML and DDL) as "events".
- **Enabling BinLog**: In `my.cnf` (or `my.ini` on Windows):
    ```ini
    [mysqld]
    log_bin = /var/log/mysql/mysql-bin # Path to binary log files
    server_id = 1                       # Unique ID for each server in replication
    binlog_format = ROW                 # Recommended format for safety
    ```
- **Point-in-Time Recovery**:
    - Restore a full backup taken *before* the desired recovery point.
    - Apply binary logs from the time of backup up to the specific point in time or event before the disaster.
    ```bash
    # Apply all changes from a binlog file
    mysqlbinlog /var/log/mysql/mysql-bin.000001 | mysql -u root -p
    # For recovery up to a specific time (e.g., before an accidental DELETE)
    mysqlbinlog --start-datetime="2025-07-08 10:00:00" --stop-datetime="2025-07-08 11:30:00" /var/log/mysql/mysql-bin.000001 | mysql -u root -p
    ```
- **Used extensively for MySQL Replication.**

## 9. Replication

### What is Replication?
- The process of copying data from one MySQL database server (Master) to another (Slave).
- **Asynchronous by default**: Master doesn't wait for slave to confirm receipt.
- **Uses BinLog**: Master writes changes to its binary log, slave reads from it and applies them.

### Common Replication Scenarios
1.  **High Availability/Failover**: If master fails, promote a slave to new master.
2.  **Read Scaling**: Distribute read queries across multiple slaves to reduce load on the master.
3.  **Analytics/Reporting**: Run heavy reports on slaves, not impacting master performance.
4.  **Backups**: Take consistent backups from a slave to minimize master downtime.

### Key Terms
- **Master**: The server where data originates and writes are performed.
- **Slave**: The server(s) that receive and apply changes from the master.
- **Binary Log (BinLog)**: On the master, records all changes.
- **Relay Log**: On the slave, stores events received from the master's binlog before applying them.
- **Replication Threads (on Slave)**:
    - **IO Thread**: Connects to master, reads binlog events, writes to relay log.
    - **SQL Thread**: Reads events from relay log, applies them to slave database.

### Basic Setup Steps (Simplified)
1.  **Master Configuration**: Enable `log_bin`, set a unique `server_id`. Create a replication user.
2.  **Slave Configuration**: Set a unique `server_id`.
3.  **Master Dump**: Take a snapshot of master data (`mysqldump`).
4.  **Slave Load**: Load snapshot onto slave.
5.  **Slave Connect**: Use `CHANGE MASTER TO ...` command to tell slave how to connect to master (host, user, password, master log file, master log position).
    ```sql
    -- On Slave
    CHANGE MASTER TO
        MASTER_HOST='master_ip_address',
        MASTER_USER='repl_user',
        MASTER_PASSWORD='repl_password',
        MASTER_LOG_FILE='mysql-bin.000001', -- From master's SHOW MASTER STATUS;
        MASTER_LOG_POS=12345;               -- From master's SHOW MASTER STATUS;
    ```
6.  **Start Slave**: `START SLAVE;`
7.  **Check Status**: `SHOW SLAVE STATUS\G;` (Look for `Slave_IO_Running: Yes`, `Slave_SQL_Running: Yes`, and `Seconds_Behind_Master: 0`).

### MySQL Group Replication (MGR)
- A more advanced, built-in feature for multi-master updates and high availability within a cluster.
- Provides stronger consistency guarantees (e.g., Virtual Synchrony) than traditional async replication.

## 10. Performance Tuning & Optimization

### Key Areas
- **Schema Design**:
    - Proper normalization (or judicious denormalization for specific read performance needs).
    - Use correct and smallest suitable data types.
    - Add `NOT NULL` where logically applicable (can help index efficiency).
- **Indexing**:
    - Create indexes on columns used in `WHERE`, `JOIN`, `ORDER BY`, `GROUP BY` clauses.
    - Use `EXPLAIN` to verify index usage and identify full table scans.
    - Understand **covering indexes** (index includes all columns needed by query, avoiding table lookup).
    - Avoid over-indexing (slows down writes, increases disk space).
- **Query Optimization**:
    - Avoid `SELECT *`. Select only needed columns.
    - Use `LIMIT` with `ORDER BY` for large result sets and pagination.
    - Avoid functions on indexed columns in `WHERE` clauses (e.g., `WHERE DATE(order_date) = '...'` prevents index use on `order_date`).
    - Optimize `JOIN` order (smaller result sets first).
    - Avoid `OR` in `WHERE` clauses where `IN` can be used.
- **Server Configuration (`my.cnf`)**:
    - **`innodb_buffer_pool_size`**: Most critical for InnoDB performance. Allocate 50-80% of available RAM to cache data/indexes.
    - **`innodb_log_file_size`**: Size of transaction logs.
    - **`max_connections`**: Max concurrent client connections.
    - **`tmp_table_size` / `max_heap_table_size`**: For in-memory temporary tables (used for complex queries like `GROUP BY` on large datasets).
    - **`sort_buffer_size`**: For sorting large results.
    - **`log_slow_queries` / `slow_query_log_file` / `long_query_time`**: Enable and analyze slow queries to find bottlenecks.
- **Hardware**: Faster CPU, more RAM, SSDs (Solid State Drives) greatly improve performance for I/O-bound workloads.