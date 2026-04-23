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

SCD Type 2 in Snowflake ETL Pipeline visual — a complete flow showing how historical changes are tracked using Streams, Tasks, and Merge operations.

🔹 Process Overview

Source Data → ERP, CRM, or cloud systems feed updates.

Stream Capture → Snowflake Streams detect changes in staging tables.

Task Execution → Scheduled Tasks run ETL logic automatically.

Merge Operation →

Marks old records as inactive (end_date, current_flag = 'N').

Inserts new records with updated values (start_date, current_flag = 'Y').

Dimension Table → Maintains full history using surrogate keys.

🔸 Example Flow

Old Record: Customer ID 101 | Alice | 456 Oak Ave | Start: 2019‑01‑01 | End: 2021‑06‑15 | Flag: N

New Record: Customer ID 101 | Alice | 789 Pine St | Start: 2021‑06‑16 | End: NULL | Flag: Y

✅ Result:  
Snowflake keeps both versions, enabling accurate historical analysis and time‑based reporting

MERGE INTO customer_dim AS target
USING staging_customer AS source
ON target.customer_id = source.customer_id
WHEN MATCHED AND target.address <> source.address THEN
  UPDATE SET end_date = CURRENT_DATE(), current_flag = 'N'
WHEN NOT MATCHED THEN
  INSERT (customer_id, name, address, start_date, current_flag)
  VALUES (source.customer_id, source.name, source.address, CURRENT_DATE(), 'Y');


![SCD Type 2 in Snowflake](https://copilot.microsoft.com/th/id/BCO.ce52136b-6b38-4dbf-8fd1-bcb30f9eb515.png)

### Key Insights
- **Streams:** Capture incremental changes.  
- **Tasks:** Automate scheduled ETL jobs.  
- **Merge:** Upsert logic for historical tracking.  
- **Dimension Table:** Stores full history with surrogate keys.
