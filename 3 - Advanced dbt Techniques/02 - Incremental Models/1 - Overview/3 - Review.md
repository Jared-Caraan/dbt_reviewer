An **incremental model** only processes **new or changed data**, instead of rebuilding the entire table every time. They are the ideal materialization for extremely large datasets.

**The Incremental Materialization:**

The incremental materialization is included in the model you'd like to materialize as incremental.

`{{ config(materialized='incremental') }}`

**Writing incremental logic with `{{this}}` and `is_incremental`**
- `{{this}}` represents the currently existing database object mapped to this model.
  - We’re selecting from (and then building) new rows after the most recent updated_at timestamp from the currently-existing version of the model in your warehouse.
- The `is_incremental()` macro powers incremental materializations. It will return True if all of the following conditions are met:
  - The model must already exist in the database
  - The full-refresh flag is not passed 
  - The running model is configured with materialized='incremental'
- To tell dbt which rows it should transform on an incremental run, wrap valid SQL that filters for these rows in the `is_incremental()` macro.

```sql
{{
    config(
        materialized='incremental'
    )
}}

select * from {{ ref('example_model') }}
{% if is_incremental() %}
where 
updated_at >= (select max(updated_at) from {{this}} 
{% endif %}
```
