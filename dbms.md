# Database Management Systems (DBMS)

## Part 1: Introduction to Databases

### 1. Databases and Database Users
- **Introduction**: Overview of data, information, and the need for databases.
- **Traditional File-Based Systems**: Limitations (data redundancy, inconsistency, difficulty in sharing, security issues, integrity problems).
    - **Example (Redundancy/Inconsistency)**: Customer address stored in multiple files (Orders, Invoices, Shipping). If changed in one, might not be updated in others, leading to conflicting data.
- **Database Approach**:
    - **Database**: Organized collection of related data.
    - **DBMS**: Software system for creating, maintaining, and controlling access to databases.
    - **Database Application Programs**: Programs that interact with the database.
- **Components of the DBMS Environment**: Hardware, software, data, users, procedures.
- **Roles in the Database Environment**:
    - **Database Administrators (DBA)**: Manages database resources.
    - **Database Designers**: Identifies data and relationships.
    - **Application Developers**: Builds user interfaces and application logic.
    - **End-Users**: Uses the database system.
- **Advantages of Using the DBMS Approach**: Controlled redundancy, consistency, sharing, security, integrity, concurrency, backup/recovery.
- **Brief History of Database Applications**: Hierarchical, network, relational, object-oriented, web, Big Data, NoSQL.
- **When Not to Use a DBMS**: High initial investment, overhead, simplicity of data.

### 2. Database System Concepts and Architecture
- **Data Models, Schemas, and Instances**:
    - **Data Model**: Conceptual tools for describing data.
    - **Schema**: Description of the database structure.
        - **Example**: `CREATE TABLE Employees (EmpID INT PRIMARY KEY, Name VARCHAR(100))` defines a schema for an Employee table.
    - **Instance**: Actual data in the database at a specific moment.
        - **Example**: At 10:00 AM, the `Employees` table contains `{ (1, 'Alice'), (2, 'Bob') }`.
- **Three-Schema Architecture (ANSI/SPARC)**:
    - **External Level (View Level)**: User's view of data.
        - **Example**: A `Managers_View` might only show `EmpID` and `Name` for employees with `Role = 'Manager'`, hiding salary details from non-manager users.
    - **Conceptual Level (Logical Level)**: Global view of the database.
        - **Example**: The entire `Employees` table with all columns and relationships to other tables (Departments, Projects).
    - **Internal Level (Physical Level)**: Physical storage structure.
        - **Example**: `EmpID` is stored as a 4-byte integer, `Name` as variable-length characters, and data is stored in a specific file on disk.
- **Data Independence**:
    - **Physical Data Independence**: Changes in physical schema without affecting conceptual.
        - **Example**: If you change the file organization of the `Employees` table (e.g., from heap file to B-tree indexed file), the application code reading `EmpID` and `Name` doesn't need to change.
    - **Logical Data Independence**: Changes in conceptual schema without affecting external.
        - **Example**: Adding a new column `Email` to the `Employees` table won't affect existing applications that use the `Managers_View` if `Email` is not part of that view.
- **Database Languages and Interfaces**:
    - **DDL (Data Definition Language)**: Defines schema (`CREATE`, `ALTER`, `DROP`).
    - **DML (Data Manipulation Language)**: Manipulates data (`SELECT`, `INSERT`, `UPDATE`, `DELETE`).
    - **SDL (Storage Definition Language)**: Specifies internal schema.
    - **VML (View Mapping Language)**: Defines external schema mappings.
- **Centralized vs. Client/Server Architectures for DBMSs**:
    - **Centralized**: All components on a single machine.
    - **Client/Server**: Clients request services from a database server.
        - **Two-Tier**: Client-server directly.
            - **Example**: A desktop application directly connecting to a MySQL database server.
        - **Three-Tier/N-Tier**: Adds application server layer.
            - **Example**: A web browser (client) connects to a web server (application server), which then connects to a database server.
- **Classification of DBMSs**: Relational, Object-Oriented, Object-Relational, NoSQL.

## Part 2: Relational Data Model and SQL

### 3. The Relational Data Model and Relational Database Constraints
- **Relational Model Concepts**:
    - **Relation (Table)**: Named table of rows and columns.
    - **Tuple (Row)**: A record in the table.
    - **Attribute (Column)**: A named column in the table.
    - **Domain**: Set of allowed values for an attribute.
        - **Example**: The domain for an `Age` attribute might be `INTEGER > 0`.
    - **Schema of a Relation**: Name of relation and list of attributes.
    - **Relational Database Schema**: Collection of relation schemas.
- **Relational Model Constraints**:
    - **Key Constraints**: Primary Key, Candidate Key, Super Key.
        - **Primary Key**: `EmpID` in an `Employees` table (uniquely identifies each employee).
        - **Candidate Key**: If `(EmpID, SSN)` both uniquely identify employees, both are candidate keys. One is chosen as PK.
    - **Entity Integrity Constraint**: Primary key attributes cannot be NULL.
        - **Example**: An `EmpID` cannot be left empty when inserting a new employee.
    - **Referential Integrity Constraint (Foreign Key)**: Foreign key values must match primary key values in the referenced table or be NULL.
        - **Example**: `DeptID` in `Employees` table is a foreign key referencing `DeptID` (primary key) in `Departments` table. You cannot assign an employee to a `DeptID` that doesn't exist in the `Departments` table.
    - **Domain Constraints**: Attribute values must be from their domains.
        - **Example**: `Gender` attribute constrained to 'M' or 'F'.
- **Update Operations and Dealing with Constraint Violations**:
    - **Insert**: Adding new tuples.
    - **Delete**: Removing tuples.
    - **Update**: Modifying attribute values.
    - **Actions on Constraint Violation**:
        - **Restrict**: Prevent the action.
        - **Cascade**: Apply the action to related tuples.
            - **Example (Cascade Delete)**: If `DeptID` is deleted from `Departments` with `ON DELETE CASCADE`, all employees in that department are also deleted from `Employees`.
        - **Set NULL**: Set foreign key to NULL.
            - **Example (Set NULL Delete)**: If `DeptID` is deleted from `Departments` with `ON DELETE SET NULL`, employees in that department will have their `DeptID` set to `NULL`.
        - **Set Default**: Set foreign key to a default value.

### 4. Basic SQL
- **SQL Data Definition and Data Types**:
    - `CREATE TABLE`: Defining table schema, constraints, data types (e.g., `INT`, `VARCHAR`, `DATE`, `DECIMAL`).
        ```sql
        CREATE TABLE Employees (
            EmpID INT PRIMARY KEY,
            Name VARCHAR(100) NOT NULL,
            DeptID INT,
            Salary DECIMAL(10, 2),
            HireDate DATE,
            FOREIGN KEY (DeptID) REFERENCES Departments(DeptID) ON DELETE SET NULL
        );
        ```
    - `DROP TABLE`: Deleting tables.
    - `ALTER TABLE`: Modifying table structure.
- **Specifying Constraints in SQL**: `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`, `CHECK`.
- **Basic Retrieval Queries (`SELECT`)**:
    - `SELECT FROM WHERE`: Basic query structure.
        ```sql
        SELECT Name, Salary FROM Employees WHERE DeptID = 101;
        ```
    - `DISTINCT`: Eliminating duplicate rows.
        ```sql
        SELECT DISTINCT DeptID FROM Employees;
        ```
    - `ORDER BY`: Sorting results.
        ```sql
        SELECT Name, Salary FROM Employees ORDER BY Salary DESC;
        ```
    - `LIMIT`/`TOP`: Restricting number of results.
        ```sql
        SELECT Name FROM Employees ORDER BY Salary DESC LIMIT 5; -- Top 5 highest paid
        ```
- **`INSERT`, `DELETE`, and `UPDATE` Statements**:
    ```sql
    INSERT INTO Employees (EmpID, Name, DeptID, Salary) VALUES (3, 'Charlie', 102, 60000.00);
    UPDATE Employees SET Salary = 75000.00 WHERE EmpID = 1;
    DELETE FROM Employees WHERE Name = 'Charlie';
    ```

### 5. More SQL: Complex Queries, Triggers, Views, and Schema Modification
- **Complex SQL Retrieval Queries**:
    - **Aggregate Functions**: `COUNT`, `SUM`, `AVG`, `MAX`, `MIN`.
        ```sql
        SELECT AVG(Salary) FROM Employees;
        ```
    - **`GROUP BY`**: Grouping rows for aggregation.
        ```sql
        SELECT DeptID, AVG(Salary) FROM Employees GROUP BY DeptID; -- Avg salary per department
        ```
    - **`HAVING`**: Filtering groups.
        ```sql
        SELECT DeptID, COUNT(EmpID) FROM Employees GROUP BY DeptID HAVING COUNT(EmpID) > 5; -- Departments with more than 5 employees
        ```
    - **Nested Queries (Subqueries)**: Queries within queries.
        ```sql
        SELECT Name FROM Employees WHERE DeptID IN (SELECT DeptID FROM Departments WHERE DeptName = 'Sales');
        ```
    - **`EXISTS`, `NOT EXISTS`**: Checking for existence of rows.
        ```sql
        SELECT Name FROM Employees E WHERE EXISTS (SELECT 1 FROM Projects P WHERE P.ManagerID = E.EmpID); -- Employees who are managers of a project
        ```
    - **`ANY`, `ALL`**: Comparing with a set of values.
    - **JOIN Operations**:
        - `INNER JOIN`: Returns matching rows from both tables.
            ```sql
            SELECT E.Name, D.DeptName
            FROM Employees E INNER JOIN Departments D
            ON E.DeptID = D.DeptID;
            ```
        - `LEFT JOIN`/`LEFT OUTER JOIN`: All rows from left, matching from right (or NULLs).
            ```sql
            SELECT E.Name, D.DeptName
            FROM Employees E LEFT JOIN Departments D
            ON E.DeptID = D.DeptID; -- Includes employees without a department
            ```
- **Specifying Constraints as Assertions and Actions as Triggers**:
    - **Assertions**: General constraints over the database.
        - **Example**: `CREATE ASSERTION Check_Salary_Range CHECK (NOT EXISTS (SELECT * FROM Employees WHERE Salary < 20000 OR Salary > 200000));` (Ensures all salaries are within a specific range).
    - **Triggers**: Event-driven actions (e.g., `BEFORE INSERT`, `AFTER UPDATE`).
        - **Example**: A trigger that automatically updates `LastModifiedDate` column of a row whenever it's updated. Or a trigger that logs all deletions from a table.
- **Views (Virtual Tables) in SQL**:
    - `CREATE VIEW`: Defining a virtual table based on a query.
        ```sql
        CREATE VIEW Sales_Employees_View AS
        SELECT EmpID, Name, Salary FROM Employees WHERE DeptID = (SELECT DeptID FROM Departments WHERE DeptName = 'Sales');
        ```
        Users can then query `Sales_Employees_View` as if it were a real table, without knowing the underlying complexity or sensitive data.
- **Schema Change Statements in SQL**: `ALTER TABLE` for adding/dropping columns, constraints.

### 6. The Relational Algebra and Relational Calculus
- **Relational Algebra**: Procedural query language.
    - **Unary Operations**:
        - `SELECT` ($\sigma$): Filters rows. $\sigma_{Salary > 50000}(Employees)$
        - `PROJECT` ($\pi$): Selects columns. $\pi_{Name, DeptID}(Employees)$
    - **Set Theory Operations**: `UNION` ($\cup$), `INTERSECTION` ($\cap$), `DIFFERENCE` ($-$), `CARTESIAN PRODUCT` ($\times$).
    - **Binary Operations**:
        - `JOIN` ($\bowtie$): Combines relations based on a condition. $Employees \bowtie_{Employees.DeptID = Departments.DeptID} Departments$
        - `DIVISION` ($\div$): For queries like "find all X that are related to ALL Y."
            - **Example**: Finding students who have taken *all* courses taught by a specific instructor.
- **Relational Calculus**: Non-procedural query language.
    - **Tuple Relational Calculus (TRC)**: Based on tuple variables.
    - **Domain Relational Calculus (DRC)**: Based on domain variables.

## Part 3: Conceptual Modeling and Database Design

### 7. Data Modeling Using the Entity-Relationship (ER) Model
- **Using High-Level Conceptual Data Models for Database Design**: Importance of conceptual modeling.
- **Entity Types, Entity Sets, Attributes, and Keys**:
    - **Entity**: Object in the real world.
    - **Entity Type**: Collection of entities with common attributes. (e.g., STUDENT, COURSE)
    - **Entity Set**: Current collection of entities of an entity type. (e.g., all current students)
    - **Attributes**: Properties of entities (simple, composite, multi-valued, derived).
        - **Example**:
            - Simple: `StudentID`
            - Composite: `Address` (composed of `Street`, `City`, `Zip`)
            - Multi-valued: `PhoneNumbers` (a student can have multiple phones)
            - Derived: `Age` (derived from `DateOfBirth`)
    - **Key Attributes**: Uniquely identify entities. (e.g., `StudentID` for the `STUDENT` entity type)
- **Relationship Types, Relationship Sets, Roles, and Structural Constraints**:
    - **Relationship Type**: Association among entity types. (e.g., `ENROLLS` between `STUDENT` and `COURSE`)
    - **Relationship Set**: Current collection of relationships.
    - **Role**: Role played by an entity in a relationship. (e.g., in `ENROLLS`, `STUDENT` plays the 'Enrolling' role, `COURSE` plays the 'Enrolled In' role)
    - **Cardinality Ratios**:
        - 1:1 (One student has one locker)
        - 1:N (One department has many employees)
        - M:N (Many students enroll in many courses)
    - **Participation Constraints**:
        - **Total**: Every entity in the entity set must participate. (e.g., Every employee *must* belong to a department). Represented by a double line.
        - **Partial**: An entity *may or may not* participate. (e.g., A manager *may or may not* manage a project). Represented by a single line.
- **Weak Entity Types**: Entity types that cannot be identified solely by their own attributes; they depend on a "strong" (owner) entity type.
    - **Example**: `DEPENDENT` entity type (of an `EMPLOYEE`) might be identified by `DependentName` *along with* the `EmployeeID` of the owning `EMPLOYEE`. Represented by a double rectangle.
- **ER Diagrams**: Graphical representation of ER models.
- **Relationship Types of Degree Higher than Two**: Ternary, n-ary relationships.
    - **Example (Ternary)**: `SUPPLY` relationship involving `SUPPLIER`, `PART`, and `PROJECT`. A specific supplier supplies a specific part to a specific project.

### 8. The Enhanced Entity-Relationship (EER) Model
- **Subclasses, Superclasses, and Inheritance**:
    - **Specialization**: Top-down process, breaking down a superclass into subclasses.
        - **Example**: `EMPLOYEE` superclass specialized into `SECRETARY`, `ENGINEER`, `TECHNICIAN`.
    - **Generalization**: Bottom-up process, combining subclasses into a superclass.
        - **Example**: Combining `CAR`, `TRUCK` into `VEHICLE`.
    - **Inheritance**: Subclasses inherit attributes and relationships from superclasses.
- **Constraints and Characteristics of Specialization/Generalization Hierarchies**:
    - **Disjoint (d) vs. Overlapping (o)**:
        - **Disjoint**: An entity can belong to at most one subclass. (e.g., an employee can be *either* a Secretary *or* an Engineer, but not both).
        - **Overlapping**: An entity can belong to multiple subclasses. (e.g., a person can be a `STUDENT` and an `EMPLOYEE`).
    - **Total (double line from superclass) vs. Partial (single line)**:
        - **Total**: Every entity in the superclass must belong to at least one subclass. (e.g., Every `EMPLOYEE` *must* be either a `SECRETARY`, `ENGINEER`, or `TECHNICIAN`).
        - **Partial**: An entity in the superclass may or may not belong to a subclass. (e.g., Not every `PERSON` is necessarily a `STUDENT` or `FACULTY`).
- **Modeling of UNION Types Using Categories**: Representing a collection of objects that are members of different entity types.
    - **Example**: `OWNER` could be a category for `COMPANY` entities and `PERSON` entities (i.e., an owner can be either a company or a person).
- **Data Abstraction, Knowledge Representation, and Ontology Concepts**: Deeper theoretical aspects.

### 9. Relational Database Design by ER- and EER-to-Relational Mapping
- **ER-to-Relational Mapping Algorithm**: Rules for converting ER diagrams into relational schemas.
    - **Mapping of regular entity types**: Each entity type becomes a table, its simple attributes become columns, key attribute becomes primary key.
    - **Mapping of weak entity types**: Becomes a table, includes primary key of owner entity as foreign key, its partial key becomes part of its own primary key.
    - **Mapping of 1:1 relationships**: Either merge tables or add foreign key to one table.
    - **Mapping of 1:N relationships**: Add foreign key to the 'N' side.
    - **Mapping of M:N relationships**: Create a new 'junction' or 'bridge' table with foreign keys to both participating entities.
        - **Example (M:N)**: `STUDENT` (StudentID, Name) and `COURSE` (CourseID, Title). `ENROLLS` (StudentID, CourseID, Grade). The `ENROLLS` table has FKs to `STUDENT` and `COURSE`, and its PK is (StudentID, CourseID).
    - **Mapping of multi-valued attributes**: Create a new table for the multi-valued attribute, with a foreign key to the entity it belongs to.
        - **Example (Multi-valued)**: `EMPLOYEE` has `PhoneNumbers`. Create `EMP_PHONES` (EmpID, PhoneNumber) where EmpID is FK to Employee.

### 10. Database Design Process
- **Phases of Database Design**:
    - **Requirements Collection and Analysis**: Understanding user needs.
    - **Conceptual Design**: High-level modeling (ER/EER).
    - **Logical Design (Data Model Mapping)**: Transforming conceptual model to a specific DBMS model (e.g., relational).
    - **Physical Design**: Specifying storage structures, indexes, access paths.
    - **Implementation**: Creating database schema and loading data.
    - **Operation and Maintenance**: Ongoing management, tuning, backup.
- **Automated Design Tools**: CASE tools for database design.

## Part 4: Database Programming Techniques

### 11. Introduction to SQL Programming Techniques
- **Embedded SQL**: SQL statements within a host programming language.
    - **Example (Pseudocode)**: `EXEC SQL SELECT Name INTO :host_name FROM Employees WHERE EmpID = :host_emp_id;`
- **Dynamic SQL**: Constructing and executing SQL statements at runtime.
    - **Example (Pseudocode)**: Building a `SELECT` statement string based on user input, then executing it. `SQL_Query_String = "SELECT * FROM " + user_table_name; EXECUTE IMMEDIATE SQL_Query_String;`
- **SQL/CLI (Call-Level Interface)**: API for database access (e.g., ODBC, JDBC).
    - **Example**: `Connection.prepareStatement("SELECT * FROM Customers").executeQuery();` (JDBC)
- **Stored Procedures**: Pre-compiled SQL code executed on the server.
    - **Example**: A procedure `GetEmployeeSalary(emp_id INT)` that returns the salary of a specific employee. Calling it: `CALL GetEmployeeSalary(101);`
- **Functions**: User-defined functions for data manipulation.

### 12. Web Database Programming
- **Accessing Databases on the Web**: Web architectures (e.g., three-tier).
- **Technologies**: CGI, ASP, JSP, PHP, servlets, frameworks (e.g., Node.js with Express).
- **Security Considerations**: SQL Injection prevention, XSS.

## Part 5: Object, Object-Relational, and XML: Concepts, Models, Languages, and Standards

### 13. Object and Object-Relational Databases
- **Object-Oriented Concepts**: Encapsulation, inheritance, polymorphism.
- **Object Database (OODBMS)**: Direct storage of objects.
    - **Example**: Storing a `Car` object directly with its methods and attributes, rather than decomposing it into separate relational tables.
- **Object-Relational Database (ORDBMS)**: Extends relational model with object features (e.g., complex data types, object identity, inheritance).
    - **Example**: PostgreSQL with custom data types like `GEOMETRY` or arrays, or table inheritance where one table inherits columns from another.

### 14. XML: Extensible Markup Language
- **XML Hierarchical Model**: Tree-based structure.
- **XML Documents and DTDs/XML Schema**: Structure definition.
- **XML Query Languages**: XPath, XQuery.
    - **Example (XPath)**: `/bookstore/book[price>35]/title` to select titles of books with price > 35.
- **XML and Databases**: Storing XML data in relational databases, native XML databases.

## Part 6: Database Design Theory and Normalization

### 15. Basics of Functional Dependencies and Normalization for Relational Databases
- **Informal Design Guidelines for Relational Databases**: Avoiding anomalies.
- **Functional Dependencies (FDs)**: `X -> Y` (X determines Y).
    - **Example**: `StudentID -> StudentName` (If you know StudentID, you know StudentName).
    - **Example**: `{StudentID, CourseID} -> Grade` (A student's grade in a course is determined by both student and course ID).
- **Inference Rules for FDs**: Armstrong's Axioms (Reflexivity, Augmentation, Transitivity).
- **Closure of a Set of FDs**: All FDs implied by a given set.
- **Minimal Cover**: Smallest equivalent set of FDs.
- **Normalization**: Process of decomposing relations to reduce redundancy and anomalies.
    - **Insertion Anomaly**: Cannot add data without adding other related data.
        - **Example**: In a table `(EmpID, EmpName, DeptName, DeptLocation)`, you can't add a new department without having an employee for it.
    - **Deletion Anomaly**: Deleting data causes loss of other related data.
        - **Example**: If you delete the last employee from a department in the table above, you lose information about that department itself.
    - **Update Anomaly**: Changing one piece of data requires multiple updates.
        - **Example**: If a department's location changes in the above table, you have to update it for every employee in that department.
- **Normal Forms**:
    - **1NF (First Normal Form)**: Atomic values, no repeating groups.
        - **Violation Example**: A column `PhoneNumbers` containing "123-4567, 987-6543". To fix, create a separate `Employee_Phones` table `(EmpID, PhoneNumber)`.
    - **2NF (Second Normal Form)**: 1NF + no partial dependencies. (Applies to tables with composite primary keys).
        - **Violation Example**: Table `(StudentID, CourseID, Grade, CourseName)`. PK is `(StudentID, CourseID)`. `CourseID -> CourseName` is a partial dependency. To fix, decompose into `(StudentID, CourseID, Grade)` and `(CourseID, CourseName)`.
    - **3NF (Third Normal Form)**: 2NF + no transitive dependencies.
        - **Violation Example**: Table `(EmpID, EmpName, DeptID, DeptName, DeptLocation)`. PK is `EmpID`. `EmpID -> DeptID` and `DeptID -> DeptName, DeptLocation`. `EmpID -> DeptName` is transitive. To fix, decompose into `(EmpID, EmpName, DeptID)` and `(DeptID, DeptName, DeptLocation)`.
    - **BCNF (Boyce-Codd Normal Form)**: Stronger than 3NF, every determinant is a candidate key.

### 16. Relational Database Design Algorithms and Further Dependencies
- **Algorithms for Relational Database Design**: Decomposition algorithms.
- **Multivalued Dependencies (MVDs)**: `X ->> Y` (X determines a set of values for Y, independently of other attributes).
    - **Example**: In `(Student, Course, Hobby)`, if a student has multiple courses and multiple hobbies, but courses and hobbies are independent of each other. `Student ->> Course` and `Student ->> Hobby`.
- **4NF (Fourth Normal Form)**: BCNF + no MVDs.
- **Join Dependencies (JDs)**: Relation can be reconstructed by joining smaller relations.
- **5NF (Fifth Normal Form)**: 4NF + no JDs.
- **Domain-Key Normal Form (DKNF)**: All constraints are logical consequences of domain and key constraints.

## Part 7: File Structures, Hashing, Indexing, and Physical Database Design

### 17. Disk Storage, Basic File Structures, and Hashing
- **Secondary Storage Devices**: Disks, RAID.
- **Buffering**: Managing data movement between main memory and disk.
- **File Organizations**:
    - **Heap Files**: Unordered records. Fast for insertion, slow for search.
    - **Sorted Files**: Records ordered by a key. Good for range queries and sequential scans on the sorted attribute.
    - **Hashed Files**: Records distributed based on a hash function. Fast for equality search on the hash key.
        - **Static Hashing**: Fixed number of buckets. Prone to overflows if data grows.
        - **Dynamic Hashing**: Buckets grow/shrink dynamically (e.g., Extendable Hashing, Linear Hashing). Better for fluctuating data size.

### 18. Indexing Structures for Files and Physical Database Design
- **Indexes**: Data structures to speed up data access.
    - **Primary Index**: Index on the ordering key of a file. (e.g., an index on `EmpID` if the `Employees` table is physically sorted by `EmpID`).
    - **Secondary Index**: Index on a non-ordering key. (e.g., an index on `DeptID` in the `Employees` table).
- **Tree-based Indexing**:
    - **B-Trees**: Balanced tree structures for efficient retrieval, insertion, deletion.
    - **B+-Trees**: Variation of B-trees optimized for disk storage, all data pointers at leaf level. Most common for database indexes.
        - **Example**: Searching for `EmpID = 500`. The B+-tree quickly navigates from root to leaf node, finds the pointer to the disk block containing employee 500.
- **Multi-level Indexes**: Indexes on indexes.
- **Physical Database Design**: Decisions about file organizations, indexing, and data placement for performance.

## Part 8: Query Processing and Optimization

### 19. Strategies for Query Processing
- **Translating SQL Queries into Relational Algebra**: Initial step in query processing.
- **Algorithms for Relational Algebra Operations**: Implementations of SELECT, PROJECT, JOIN, etc.
    - **Example (Join Algorithms)**: Nested-Loop Join, Block Nested-Loop Join, Sort-Merge Join, Hash Join. Each has different performance characteristics depending on data size and available memory.
- **Query Trees**: Internal representation of queries.

### 20. Query Optimization
- **Heuristic Optimization**: Rule-based optimization (e.g., pushing selections down early to reduce intermediate result size).
- **Cost-Based Optimization**: Estimating cost of different execution plans.
    - **Join Order Optimization**: Choosing the best order for joins. `(A JOIN B) JOIN C` vs. `A JOIN (B JOIN C)`.
    - **Cost Estimation Models**: CPU, I/O costs.
- **Measures of Query Cost**: Disk accesses, CPU time, communication costs.

## Part 9: Transaction Processing, Concurrency Control, and Recovery

### 21. Introduction to Transaction Processing Concepts and Theory
- **Transaction**: A logical unit of database processing.
    - **Example**: Transferring money from account A to account B involves two steps: `DEBIT A` and `CREDIT B`. Both must succeed or neither.
- **ACID Properties**:
    - **Atomicity**: All or nothing. (If `DEBIT A` fails, `CREDIT B` is undone, leaving A and B unchanged).
    - **Consistency**: Preserves database integrity. (Ensures total money in system remains same before and after transfer).
    - **Isolation**: Concurrent transactions appear to run sequentially. (If two transfers happen simultaneously, they don't interfere, result is as if one ran after the other).
    - **Durability**: Committed changes are permanent. (Once money transfer is committed, it's saved even if system crashes).
- **Transaction States**: Active, partially committed, committed, failed, aborted.

### 22. Concurrency Control Techniques
- **Problem of Concurrency**:
    - **Lost Updates**: Two transactions read, modify, and write back, one's update is overwritten.
        - **Example**: T1 reads `Balance=100`, T2 reads `Balance=100`. T1 adds 10, writes 110. T2 subtracts 5, writes 95. The +10 is lost.
    - **Dirty Reads (Uncommitted Dependency)**: Transaction reads data written by another uncommitted transaction.
        - **Example**: T1 updates `Balance` to 90. T2 reads 90. T1 aborts (rolls back). T2 has read invalid data.
    - **Unrepeatable Reads**: A transaction reads the same data twice and gets different results because another committed transaction modified it between reads.
    - **Phantom Reads**: A transaction re-executes a query returning a set of rows and gets a different set because another committed transaction inserted or deleted rows matching the query.
- **Locking Techniques**:
    - **Binary Locks**: Simple lock/unlock.
    - **Shared/Exclusive Locks**: Shared (read) locks allow multiple readers. Exclusive (write) locks allow only one writer.
    - **Two-Phase Locking (2PL)**:
        - **Growing Phase**: Transaction acquires locks but cannot release any.
        - **Shrinking Phase**: Transaction releases locks but cannot acquire any new ones. Ensures serializability.
- **Timestamp Ordering**: Transactions are ordered based on their timestamps (usually start time).
- **Multiversion Concurrency Control (MVCC)**: Maintaining multiple versions of data items (each read operates on a consistent snapshot).
    - **Example**: PostgreSQL, Oracle, SQL Server use MVCC to allow readers to not block writers.
- **Validation (Optimistic) Concurrency Control**: Transactions run without locks, validated at commit. If conflict, abort. Good for low contention.
- **Granularity of Locking**: Row, page, table, database level.

### 23. Database Recovery Techniques
- **Crashes and Failures**: Transaction, system, disk failures.
- **Recovery Concepts**:
    - **Log file (Journal)**: Records all database modifications (undo/redo information).
    - **Checkpoints**: Point where all committed transactions are written to disk, reducing recovery time.
- **Recovery Algorithms**:
    - **Deferred Update**: Writes to disk only after commit. If crash, only REDO needed.
    - **Immediate Update**: Writes to disk during transaction execution. If crash, both UNDO and REDO may be needed.
    - **Shadow Paging**: Copying updated pages. Old page (shadow) used for recovery if crash.
- **ARIES (Algorithm for Recovery and Isolation Exploiting Semantics)**: Widely used recovery algorithm in commercial DBMS.

## Part 10: Distributed Databases, NoSQL Systems, Cloud Computing, and Big Data

### 24. Distributed Database Concepts
- **Distributed DBMS (DDBMS)**: Database spread across multiple sites.
    - **Example**: A bank database where customer accounts are managed by different servers in different cities.
- **Homogeneous vs. Heterogeneous DDBMS**.
- **Data Fragmentation**: Dividing data across sites.
    - **Horizontal Fragmentation**: Dividing rows. (e.g., Employees in Toronto on Server A, Employees in London on Server B).
    - **Vertical Fragmentation**: Dividing columns. (e.g., Employee personal info on Server A, Employee salary info on Server B).
- **Data Replication**: Storing copies of data at multiple sites for availability and performance.
- **Distributed Query Processing and Optimization**.
- **Distributed Transaction Management**:
    - **Two-Phase Commit (2PC)**: Protocol to ensure atomicity of transactions across multiple sites.
        - **Phase 1 (Vote)**: Coordinator asks participants to prepare.
        - **Phase 2 (Decision)**: If all prepared, coordinator commits; otherwise, aborts.
    - **Three-Phase Commit (3PC)**: Adds a third phase to handle coordinator failure during 2PC.

### 25. NoSQL Databases and Big Data Storage Systems
- **Why NoSQL?**: Scalability, flexibility, handling unstructured data, horizontal scaling.
- **Types of NoSQL Databases**:
    - **Key-Value Stores**: Simple (key -> value).
        - **Example**: Redis (caching), Riak (highly available key-value). Good for sessions, shopping cart data.
    - **Document Databases**: Store data as semi-structured documents (e.g., JSON, XML).
        - **Example**: MongoDB, Couchbase. Flexible schema, good for content management, catalogs.
    - **Column-Family Stores**: Data organized into columns that belong to column families.
        - **Example**: Cassandra, HBase. Good for time-series data, large-scale analytics.
    - **Graph Databases**: Store data as nodes and edges.
        - **Example**: Neo4j, ArangoDB. Good for social networks, recommendation engines, fraud detection.
- **CAP Theorem**: A distributed system can only guarantee two out of three:
    - **Consistency**: All nodes see the same data at the same time.
    - **Availability**: System remains operational even if some nodes fail.
    - **Partition Tolerance**: System continues to operate despite network partitions.
    - **Example**: A database choosing **AP** (Availability, Partition Tolerance) might sacrifice immediate consistency for higher uptime in a distributed environment (e.g., some NoSQL DBs).
- **BASE Properties**: (Alternative to ACID for NoSQL) Basically Available, Soft state, Eventually consistent.

### 26. Big Data Technologies Based on MapReduce and Hadoop
- **Big Data Characteristics**: Volume (amount), Velocity (speed), Variety (types), Veracity (trustworthiness).
- **Hadoop Ecosystem**:
    - **HDFS (Hadoop Distributed File System)**: Distributed file system for large datasets.
    - **MapReduce**: Programming model for processing large datasets in parallel.
        - **Example**: Counting word frequencies in a huge text file. `Map` phase emits (word, 1) pairs, `Reduce` phase sums counts for each word.
- **Other Technologies**: Spark (faster in-memory processing), Hive (SQL-like interface over Hadoop), Pig (scripting language).

## Part 11: Advanced Database Models, Systems, and Applications

### 27. Enhanced Data Models: Active, Temporal, Spatial, Multimedia, and Deductive Databases
- **Active Databases**: Rules (ECA - Event-Condition-Action) that automatically execute.
    - **Example**: An ECA rule `ON INSERT INTO ORDERS IF OrderValue > 1000 THEN NOTIFY Manager;`
- **Temporal Databases**: Store historical data and time-varying information.
    - **Example**: Tracking the salary history of an employee, including valid time periods for each salary.
- **Spatial Databases**: Store and query geographical data.
    - **Example**: Finding all restaurants within 5km of a user's current location. Queries use spatial data types (points, lines, polygons).
- **Multimedia Databases**: Store and manage multimedia objects (images, audio, video).
- **Deductive Databases**: Combine database technology with logic programming (Datalog).

### 28. Introduction to Information Retrieval and Web Search
- **Information Retrieval (IR)**: Finding relevant documents.
- **Web Search Engines**: Indexing, ranking (PageRank).
- **Text Databases**: Storing and querying textual data.

### 29. Data Mining Concepts
- **What is Data Mining?**: Discovering patterns in large datasets.
- **Data Mining Tasks**:
    - **Classification**: Predicting a category (e.g., spam/not spam).
    - **Clustering**: Grouping similar data points (e.g., customer segmentation).
    - **Association Rule Mining**: Finding relationships (e.g., "customers who buy diapers also buy baby wipes").
    - **Prediction**: Forecasting numerical values (e.g., sales forecasting).
- **Knowledge Discovery in Databases (KDD) Process**.

### 30. Overview of Data Warehousing and OLAP
- **Data Warehouse**: Subject-oriented, integrated, time-variant, non-volatile collection of data for decision support.
    - **Example**: A separate database built for historical analysis, distinct from the operational database.
- **ETL (Extract, Transform, Load)**: Process for building data warehouses.
- **OLAP (Online Analytical Processing)**: Multidimensional analysis (ROLAP, MOLAP, HOLAP).
    - **Cubes**: Multidimensional representation of data (e.g., Sales by Product, Region, Time).
    - **Operations**:
        - **Slice**: Selecting a single dimension value (e.g., sales for 'Q1 2024').
        - **Dice**: Selecting a sub-cube (e.g., sales for 'Electronics' in 'North America' during 'Q1 2024').
        - **Roll-up**: Aggregating data to a higher level (e.g., daily sales to monthly sales).
        - **Drill-down**: Going to a more detailed level (e.g., monthly sales to daily sales).
        - **Pivot**: Rotating the view of the data.

## Part 12: Additional Database Topics: Security

### 31. Database Security
- **Threats to Database Security**: Unauthorized access, data modification, denial of service.
- **Database Security Issues**: Legal, ethical, and professional issues.
- **Access Control**:
    - **Discretionary Access Control (DAC)**: Owners grant/revoke privileges.
    - **Mandatory Access Control (MAC)**: Based on security labels (e.g., Top Secret, Secret).
- **Privileges and Roles**: `GRANT`, `REVOKE`.
    - **Example**: `GRANT SELECT ON Employees TO Public;` `REVOKE DELETE ON Employees FROM HR_Manager_Role;`
- **SQL Injection Attacks**: Malicious SQL code inserted into input fields.
    - **Prevention**: Parameterized queries, prepared statements.
    - **Example (Attack)**: User enters `'; DROP TABLE Users; --` into a login field, attempting to delete the Users table.
- **Encryption**: Protecting data at rest and in transit.
- **Database Audit**: Tracking user activities.
