Slowly Changing Dimensions (SCD) — showing how data evolves in a dimension table over time.

Slowly Changing Dimension (SCD) types 0–6, showing how each handles changes in dimension data over time — perfect for data warehousing and Snowflake implementations.

## 🧠 SCD Types 0–6 Comparison

![SCD Types Comparison](https://copilot.microsoft.com/th/id/BCO.0c3483be-34e6-412d-9f6f-5511683710cd.png)

### Key Insights
- **SCD 0:** Fixed, no changes.  
- **SCD 1:** Overwrite, no history.  
- **SCD 2:** Add new row, full history.  
- **SCD 3:** Add column, partial history.  
- **SCD 4:** Separate history table.  
- **SCD 6:** Hybrid of multiple types.



## 🧠 SCD Type 2 in Snowflake ETL Pipeline

![SCD Type 2 in Snowflake](https://copilot.microsoft.com/th/id/BCO.ce52136b-6b38-4dbf-8fd1-bcb30f9eb515.png)

### Key Insights
- **Streams:** Capture incremental changes.  
- **Tasks:** Automate scheduled ETL jobs.  
- **Merge:** Upsert logic for historical tracking.  
- **Dimension Table:** Stores full history with surrogate keys.
