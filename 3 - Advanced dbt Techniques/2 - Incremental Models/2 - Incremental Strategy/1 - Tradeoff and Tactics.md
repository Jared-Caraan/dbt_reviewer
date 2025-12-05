## Tradeoff and Tactics

**What if our data shows up late?**

Our cutoff time might mean we miss this data!

We could try widening the cutoff window!

```sql
{{
    config(
        materialized='incremental'
    )
}}

select * from {{ ref('fct_marketing_web_analysis') }}
{% if is_incremental() %}
where
updated_at >= dateadd(day, -3, (select max(updated_at) from {{ this }}))
{% endif %}
```

But a wider lookback can lead to duplicate records since the where clause may capture again the older records.

<img width="840" height="395" alt="image" src="https://github.com/user-attachments/assets/73be06d9-fe2b-4c9a-90d2-32ddb8e42195" />

We want dbt to replace existing rows that were updated and insert new ones into the overlap window.

**Handling late arriving data: `unique_key`**

Using the `unique_key` to avoid duplicates:

```sql
{{
    config(
        materialized='incremental',
        unique_key = 'web_user_id'
    )
}}

select * from {{ ref('fct_marketing_web_analysis') }}
{% if is_incremental() %}
where
updated_at >= dateadd(day, -3, (select max(updated_at) from {{ this }}))
{% endif %}
```

### Under the hood

**What's the DDL/DML dbt is running?**
- Create a temp table of new records.
- Reconcile the existing table with the temp table, using one of:
    - merge("upsert" new field values on row)
    - delete+insert ("delete" entire row and "insert" new row in place)
    - insert_overwrite ("replace" entire partitions)

**Depends on:**
- Database support (e.g. Redshift does not have a merge statement)
- User input: you can specify your incremental strategy
<hr>

**What if data arrives _really_ late?**

In our opinion, the goal of incremental models is to approximate the 'true' table in a fraction of the runtime:
- Perform an analysis on the arrival time of data
- Figure out your organization's tolerance for correctness.
- Set the cutoff based on these two inputs.
- Once a week, perform a --full-refresh run to get the 'true' table

"Close enough & performant"
<hr>

**Incremental models introduce tradeoffs**
- Most incremental models are "approximately correct"
- They introduce a level of code complexity (i.e. how easy it is for someone to understand your code)
- Prioritizing correctness can negate performance gains from incrementality.

Think of incremental models as an _upgrade_, not necessarily a _starting point_.
<hr>

**Should I use an incremental model?**

Good candidates:
- Immutable event streams: tall and skinny tables, append-only, no updates
- If there are any updates, a reliable `updated_at` field

Not-so-good candidates:
- A small table
- Data changes constantly: new columns, renamed columns, etc.
- Data is updated in unpredictable ways
- Transfomations perform comparisons or calculations that require other rows
<hr>

**Tactics**
- How do we want to materialize this model?
    - Start with _view_
    - When it takes too long to query, switch to _table_
    - When it takes too long to build, switch to _incremental_
