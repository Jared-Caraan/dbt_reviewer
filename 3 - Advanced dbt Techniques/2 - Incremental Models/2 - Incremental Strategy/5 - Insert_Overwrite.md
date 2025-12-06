## Incremental Strategy: _insert_overwrite_

- Replaces entire partitions in a destination table.
- Does not require scanning entire source table - will only scan the partitions you configure.
- **Much more efficient than merge on BigQuery**
- **Best used for:** Models _that are partitioned_ getting new data and updates to old rows, but _merge_ is too slow and costly. `insert_overwrite` is more complex, and most useful on BigQuery.
- **SQL used:**
    - In BigQuery: creates temp table, declares partitions to replace, then merge into.
    - In other databases: DELETE FROM then INSERT INTO

**Configuration**
```sql
{{ config(
    materialized="incremental",
    unique_key = 'order_id',
    partition_by = {
        "field":"order_date",
        "data_type":"date",
        "granularity":"day",
    },
    incremental_strategy="insert_overwrite",
) }}

select * from {{ ref("some_model") }}
```

**Under the Hood SQL**

<img width="1168" height="207" alt="image" src="https://github.com/user-attachments/assets/77cfe673-c3e2-4b0d-90e3-4b3d99852b1c" />


**Resource**
- [Incremental strategies](https://docs.getdbt.com/docs/build/incremental-strategy)
- [insert_overwrite](https://docs.getdbt.com/docs/build/incremental-strategy#insert_overwrite)
- [BigQuery partition_by](https://docs.getdbt.com/reference/resource-configs/bigquery-configs#using-table-partitioning-and-clustering)
