### 1. Purpose of Normalization in Database Design

**Normalization** is the process of organizing data in a database to reduce redundancy and improve data integrity. The main goals are:
- **Eliminate Redundant Data:** Avoid storing the same data in multiple places.
- **Ensure Data Integrity:** Maintain consistency and accuracy of data.
- **Simplify Database Design:** Make the database structure logical and efficient.
- **Improve Query Performance:** Optimize data retrieval by reducing unnecessary complexity.

Normalization is achieved through a series of **normal forms** (e.g., 1NF, 2NF, 3NF, BCNF), each addressing specific types of redundancy and dependency issues.

---

### 2. Difference Between SQL and NoSQL Databases

| **SQL Databases** | **NoSQL Databases** |
|--------------------|---------------------|
| Relational databases (tables with rows and columns). | Non-relational databases (key-value, document, graph, or columnar stores). |
| Use structured query language (SQL) for queries. | Use various query languages or APIs (e.g., MongoDB uses JSON-like queries). |
| Schema is fixed and predefined. | Schema is dynamic and flexible. |
| Best for structured data with complex queries. | Best for unstructured or semi-structured data. |
| Examples: MySQL, PostgreSQL, Oracle. | Examples: MongoDB, Cassandra, Redis. |

---

### 3. Handling Database Transactions in SQL

A **database transaction** is a sequence of operations performed as a single logical unit of work. In SQL, transactions are managed using the following commands:
- **BEGIN TRANSACTION:** Starts a new transaction.
- **COMMIT:** Saves all changes made during the transaction.
- **ROLLBACK:** Reverts all changes made during the transaction if an error occurs.

**Example:**
```sql
BEGIN TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```
If any operation fails, you can use `ROLLBACK` to undo the changes.

---

### 4. ACID Properties of Database Transactions

ACID stands for:
- **Atomicity:** Ensures that a transaction is treated as a single unit. Either all operations succeed, or none are applied.
- **Consistency:** Ensures that the database remains in a valid state before and after the transaction.
- **Isolation:** Ensures that concurrent transactions do not interfere with each other.
- **Durability:** Ensures that once a transaction is committed, its changes are permanent, even in the event of a system failure.

---

### 5. Importance of Indexing in Relational Databases

**Indexing** improves the speed of data retrieval operations by creating a data structure (e.g., B-tree, hash) that allows quick lookup of rows based on specific columns. Key benefits:
- **Faster Queries:** Reduces the time required to search for data.
- **Efficient Sorting:** Speeds up `ORDER BY` and `GROUP BY` operations.
- **Unique Constraints:** Ensures uniqueness of values in indexed columns.

However, excessive indexing can slow down write operations (e.g., `INSERT`, `UPDATE`, `DELETE`) because indexes must be updated.

---

### 6. Concept of Database Joins

A **join** combines rows from two or more tables based on a related column. Common types of joins include:
- **INNER JOIN:** Returns rows with matching values in both tables.
- **LEFT JOIN (or LEFT OUTER JOIN):** Returns all rows from the left table and matching rows from the right table.
- **RIGHT JOIN (or RIGHT OUTER JOIN):** Returns all rows from the right table and matching rows from the left table.
- **FULL JOIN (or FULL OUTER JOIN):** Returns all rows when there is a match in either table.
- **CROSS JOIN:** Returns the Cartesian product of both tables.

**Example:**
```sql
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.id;
```

---

### 7. Optimizing a Slow SQL Query

To optimize a slow SQL query:
1. **Use Indexes:** Ensure relevant columns are indexed.
2. **Avoid `SELECT *`:** Retrieve only the necessary columns.
3. **Optimize Joins:** Use appropriate join types and ensure join conditions are indexed.
4. **Limit Results:** Use `LIMIT` or `TOP` to reduce the number of rows returned.
5. **Analyze Execution Plan:** Use tools like `EXPLAIN` (in MySQL) or `EXPLAIN ANALYZE` (in PostgreSQL) to identify bottlenecks.
6. **Avoid Subqueries:** Replace subqueries with joins where possible.
7. **Normalize/Denormalize:** Balance normalization for data integrity and denormalization for performance.

---

### 8. Advantages of Using an ORM Framework

**Object-Relational Mapping (ORM)** frameworks (e.g., Hibernate for Java, Entity Framework for C#) map database tables to application objects. Advantages include:
- **Simplified Database Interaction:** Write code in the application's language instead of raw SQL.
- **Reduced Boilerplate Code:** Automates CRUD operations.
- **Database Agnosticism:** Easily switch between different databases.
- **Improved Security:** Reduces the risk of SQL injection attacks.
- **Code Maintainability:** Encourages cleaner, more modular code.

---

### 9. Concept of Sharding in NoSQL Databases

**Sharding** is a technique used to distribute data across multiple servers (shards) to improve scalability and performance. Each shard contains a subset of the data. Benefits include:
- **Horizontal Scaling:** Distributes the load across multiple servers.
- **Improved Performance:** Reduces the amount of data each server needs to handle.
- **Fault Tolerance:** If one shard fails, others remain operational.

Challenges include managing data distribution and ensuring consistency across shards.

---

### 10. Ensuring Data Consistency in a Distributed Database System

In a distributed database system, data consistency can be ensured through:
- **Replication:** Maintain multiple copies of data across nodes.
- **Consensus Protocols:** Use protocols like Paxos or Raft to agree on data values.
- **ACID Transactions:** Implement distributed transactions with ACID properties.
- **Eventual Consistency:** Allow temporary inconsistencies, with the guarantee that all nodes will eventually converge to the same state.
- **Conflict Resolution:** Use techniques like version vectors or last-write-wins to resolve conflicts.

Tools like **Apache Cassandra** and **Google Spanner** are designed to handle distributed consistency effectively.
