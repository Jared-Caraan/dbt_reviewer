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

**Under the hood SQL**

<img width="994" height="169" alt="image" src="https://github.com/user-attachments/assets/a3213274-2e8c-4d03-b22b-81051f417344" />

**Resource**
- [Incremental strategies](https://docs.getdbt.com/docs/build/incremental-strategy)
- [append](https://docs.getdbt.com/docs/build/incremental-strategy#append)
