## Incremental Strategy: _microbatch_

- Divides data into atomic, time-bound units (ex: day)
- Splits large models into multiple time-bounded queries: batches!
- dbt takes those queries and inserts them into your target table
- **Best used for:**
  - Very large time-series data sets
  - Time series with regular updates
- **SQL used:**
  - Time-bound SELECT query to construct batch.
  - To insert batch, dbt will use insert/overwrite or delete+insert depending on data platform.

**Configuration**
```sql
{{ config(
    materialized="incremental",
    unique_key = 'order_id',
    incremental_strategy="microbatch",
    event_time = 'order_date',
    begin = '2025-02-13',
    batch_size = 'day'
) }}

select * from {{ ref("some_model") }}
```

**Under the Hood SQL**

<img width="1142" height="225" alt="image" src="https://github.com/user-attachments/assets/78e32161-c24f-453e-86e1-e51be03e9a72" />

<img width="1145" height="194" alt="image" src="https://github.com/user-attachments/assets/f9a3bd2c-fb11-4175-9a58-cb9e848431c1" />

**Benefits**
What's really cool about the microbatch strategy is that each batch corresponds to a bounded time period. The microbatch strategy categorizes data by which batch it's in. So each batch is a unit of data that can be built or replaced on its own, which means that you can run specific batches separately if you really want to. Or if you want to, you can retry failed batches. If I wanted to run only specific batches, I might use a command like this: `dbt run --select fct_orders --event-time-start "2020-04-01" --event-time-end "2020-04-05"`

**Resource**
- [Incremental strategies](https://docs.getdbt.com/docs/build/incremental-strategy)
- [microbatch as a strategy](https://docs.getdbt.com/docs/build/incremental-strategy#microbatch)
- [microbatch incremental models](https://docs.getdbt.com/docs/build/incremental-microbatch#what-is-microbatch-in-dbt)
