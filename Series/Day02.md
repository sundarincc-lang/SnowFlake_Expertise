## 🔄 Normalization vs. Denormalization


### Key Differences
- **Normalization**: Splits data into smaller related tables → reduces redundancy, ensures consistency.  
- **Denormalization**: Combines tables with repeated data → improves query speed, simplifies reporting.  

**Use Case:**  
- Normalization → OLTP (transactional systems).  
- Denormalization → OLAP (analytics & reporting).

  🔹 Normalization
Definition: Organizing data into multiple related tables to reduce redundancy and improve consistency.
Goal: Avoid duplication, ensure data integrity.

Key Points
Data is split into smaller tables with relationships (using keys).

Follows normal forms (1NF, 2NF, 3NF, etc.).

Example: Instead of storing customer details in every order row, you keep a separate Customer table and reference it with a customer_id.

Advantages:

Saves storage space.

Easier to maintain consistency (update once, reflect everywhere).

Reduces anomalies (insert, update, delete).

Disadvantages:

More complex queries (joins across multiple tables).

Slower performance for read-heavy workloads.

🔹 Denormalization
Definition: Combining tables and allowing redundancy to improve query performance.
Goal: Optimize for fast reads and reporting.

Key Points
Data is stored in fewer tables, often with repeated values.

Example: An Orders table might include customer name and address directly, instead of referencing a separate Customer table.

Advantages:

Faster queries (fewer joins).

Simpler schema for analytics and reporting.

Useful in data warehouses and OLAP systems.

Disadvantages:

More storage required.

Risk of inconsistency (same data stored in multiple places).

Updates are harder to manage.
![Normalization vs Denormalization](https://github.com/sundarincc-lang/SnowFlake_Expertise/blob/51748728ca50c3e856ea3222621dbb42000fee48/Series/Normalization_Denormalizaton.png)

