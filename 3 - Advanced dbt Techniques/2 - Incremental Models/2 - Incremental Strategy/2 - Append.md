## Incremental Strategy: _append_

- **Adds** new rows to target table **only**
- Does not check for duplicates
- Does not check for updates
- **Best used for:** Truly immutable event streams
- **SQL used: insert into** - to add new rows

**Configuration**
```sql
{{ config(
    materialized="incremental",
    incremental_strategy="append",
) }}

select * from {{ ref("some_model") }}
```

**Resource**
- [Incremental strategies](https://docs.getdbt.com/docs/build/incremental-strategy)
- [append](https://docs.getdbt.com/docs/build/incremental-strategy#append)
