🧩 Normalization Example Scenario
You have customer and order data. Instead of repeating customer details in every order, you split them into separate tables.

Tables
Customers
CREATE OR REPLACE TABLE customers (customer_id INT, name STRING, address STRING ); 
INSERT INTO customers VALUES (1, 'Alice', '123 Maple St'), (2, 'Bob', '456 Oak Ave');

Orders
CREATE OR REPLACE TABLE orders (order_id INT, customer_id INT, product STRING, price NUMBER, order_date DATE ); 
INSERT INTO orders VALUES (101, 1, 'Laptop', 1200, '2022-01-05'), (102, 1, 'Headphones', 100, '2022-01-10'), (103, 2, 'Camera', 500, '2022-01-12');

Query (Join normalized tables)
SELECT c.name, c.address, o.product, o.price, o.order_date FROM customers c JOIN orders o ON c.customer_id = o.customer_id; 

Result: Each customer’s details appear once in the customers table, reducing redundancy.

🧩 Denormalization Example Scenario
You combine everything into one table for faster reads in analytics.

Orders_Denormalized
CREATE OR REPLACE TABLE orders_denormalized (order_id INT, customer_name STRING, address STRING, product STRING, price NUMBER, order_date DATE ); 
INSERT INTO orders_denormalized VALUES (101, 'Alice', '123 Maple St', 'Laptop', 1200, '2022-01-05'), (102, 'Alice', '123 Maple St', 'Headphones', 100, '2022-01-10'), (103, 'Bob', '456 Oak Ave', 'Camera', 500, '2022-01-12');

Query (Simple read)
SELECT customer_name, SUM(price) AS total_spent FROM orders_denormalized GROUP BY customer_name; 

✅ Result: Quick aggregation for analytics — but customer info is repeated in every row.

⚖️ Summary
Aspect | Normalization | Denormalization
--- | --- | ---
Structure | Multiple related tables | Single wide table
Redundancy | Minimal | High
Performance | Slower reads, faster writes | Faster reads, slower writes
Use Case | OLTP (transactions) | OLAP (analytics)
