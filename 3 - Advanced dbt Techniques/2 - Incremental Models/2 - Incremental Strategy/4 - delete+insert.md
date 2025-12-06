## Incremental Strategy: _delete+insert_

- Grabs all selected records, deletes old version of those records if they exist in the target table.
- Inserts new records and the new version of the records deleted based on primary key
- Requires full table scan
- **Best used for:** Models are getting new data and updates to old rows, but the data platform does not support MERGE.
- **SQL used:** delete from and then insert into with matching on primary key

**Configuration**
```sql
{{ config(
    materialized="incremental",
    unique_key = 'order_id',
    incremental_strategy="delete+insert",
) }}

select * from {{ ref("some_model") }}
```

**Under the hood SQL**
<img width="1151" height="734" alt="image" src="https://github.com/user-attachments/assets/2217a5d1-1bd1-4284-92f3-abb8442e4dd4" />


**Resource**
- [Incremental strategies](https://docs.getdbt.com/docs/build/incremental-strategy)
- [delete+insert](https://docs.getdbt.com/docs/build/incremental-strategy#deleteinsert)
