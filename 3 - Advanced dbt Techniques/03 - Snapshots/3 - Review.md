Analysts often need to "look back in time" at previous data states in their mutable tables. While some source data systems are built in a way that makes accessing historical data possible, this is not always the case. dbt provides a mechanism, snapshots, which records changes to a mutable table over time.

Snapshots:

- Are built as a table in the database, usually in a dedicated schema.
- On the first run, build entire table and adds four columns: dbt_scd_id, dbt_updated_at, dbt_valid_from, and dbt_valid_to
- In future runs, dbt will scan the underlying data and append new records based on the configuration that is made.
- This allows you to capture historical data
