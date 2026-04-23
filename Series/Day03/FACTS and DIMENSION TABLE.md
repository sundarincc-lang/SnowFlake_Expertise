## 🧮 Fact Table vs. Dimension Table

### Key Insights
- **Fact Table:** Holds numeric metrics for analysis.  
- **Dimension Table:** Holds descriptive attributes for context.  
- Together, they form a **Star Schema** for efficient querying in data warehouses.

   Fact Table (Blue Section)

Stores quantitative data — metrics like sales, revenue, quantity.

Example columns: Order ID, Customer ID, Product ID, Amount, Order Date.

Each row represents a transaction or event.

Used for data analysis and aggregations (SUM, AVG, COUNT).

🔸 Dimension Tables (Orange Section)

Store descriptive attributes — who, what, where, when.

Examples:

Customer Dimension → Customer ID, Name, Location.

Product Dimension → Product ID, Product Name, Category.

Provide context to facts for slicing and dicing data.

🏗️ Data Warehouse Schema

The Fact Table sits at the center.

Connected to multiple Dimension Tables via foreign keys.

This structure forms a Star Schema — ideal for OLAP analytics.

![Fact vs Dimension Table](https://copilot.microsoft.com/th/id/BCO.5854f872-2e22-4fe5-9e16-d1373fb252a9.png)


