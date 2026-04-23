Slowly Changing Dimensions (SCD) — showing how data evolves in a dimension table over time.

🧩 Type 1 – Overwrite (No History)
Scenario: A customer moves to a new address.
Action: Update the existing record; old data is lost.

UPDATE customer_dim
SET address = '789 Pine St'
WHERE customer_id = 1;

Result:

Customer ID	Name	Address
1	Alice	789 Pine St

✅ Use Case: When historical data isn’t needed (e.g., correcting typos).

🧩 Type 2 – Add New Row (Keep History)
Scenario: Track address changes over time.
Action: Insert a new row with start and end dates.  

INSERT INTO customer_dim
(customer_id, name, address, start_date, end_date, current_flag)
VALUES (1, 'Alice', '789 Pine St', '2021‑06‑16', NULL, 'Y');

UPDATE customer_dim
SET end_date = '2021‑06‑15', current_flag = 'N'
WHERE customer_id = 1 AND current_flag = 'Y';


Result:

Customer ID	Name	Address	Start Date	End Date	Current Flag
1	Alice	456 Oak Ave	2019‑01‑01	2021‑06‑15	N
1	Alice	789 Pine St	2021‑06‑16	NULL	Y

✅ Use Case: When full history is required (e.g., customer tracking).

🧩Type 3 – Add New Column (Partial History)
Scenario: Track only the previous status.
Action: Add a column for the old value.

ALTER TABLE customer_dim ADD previous_status VARCHAR(20);

UPDATE customer_dim
SET previous_status = current_status,
    current_status = 'Active'
WHERE customer_id = 1;


Result:

Customer ID	Name	Current Status	Previous Status
1	Alice	Active	Inactive

✅ Use Case: When only limited history is needed (e.g., last known status).



## 🧠 SCD Type 2 in Snowflake ETL Pipeline

![SCD Type 2 in Snowflake](https://copilot.microsoft.com/th/id/BCO.ce52136b-6b38-4dbf-8fd1-bcb30f9eb515.png)

### Key Insights
- **Streams:** Capture incremental changes.  
- **Tasks:** Automate scheduled ETL jobs.  
- **Merge:** Upsert logic for historical tracking.  
- **Dimension Table:** Stores full history with surrogate keys.
