## Incremental Strategy: _merge_

- Updates records that already exist using primary key
- Inserts new records based on primary key
- Runs full table scan - can cause performance issues at scale
- **Best used for:** Models that are getting new data added but they could also be updating existing records
- **SQL used: merge into** with matching on primary key

**Configuration**
```sql
{{ config(
    materialized="incremental",
    unique_key = 'order_id',
    incremental_strategy="merge",
) }}

select * from {{ ref("some_model") }}
```
**Under the hood SQl**

<img width="990" height="540" alt="image" src="https://github.com/user-attachments/assets/80c39dc3-3331-49e9-a2d8-f55c389438e3" />

**Resource**
- [Incremental strategies](https://docs.getdbt.com/docs/build/incremental-strategy)
- [merge](https://docs.getdbt.com/docs/build/incremental-strategy#merge)
