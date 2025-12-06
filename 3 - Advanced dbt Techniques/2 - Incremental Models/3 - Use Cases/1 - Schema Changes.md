## Dealing with Schema Changes

What if we want to have additional control over our incremental models when columns change?

You can deal with it in two ways - via `dbt-project.yml` and via model-level configurations.

**dbt-project.yml**

```yaml
models:
  +on_schema_change: "sync_all_columns"
```

**Model-level configuration**
```sql
{{ config(
    materialized="incremental",
    unique_key = 'date_day',
    on_schema_change="fail",
) }}
```

**`on_schema_change`**

- ignore: Default behavior. If you add a column to this incremental model and run a dbt run, this column will NOT appear in your target table. If you remove a column from your incremental model and run a dbt run, your run will fail.
- fail: Triggers an error message when the source and target schemas diverge.
- append_new_columns: Append new columns to the existing table. Note that this setting does not remove columns from the existing table that are not present in the new data.
- sync_all_columns: Adds any new columns to the existing table, and removes any columns that are now missing. Not that this is inclusive of data type changes. On BigQuery, changing column types requires a full table scan; be mindful of the trade-offs when implementing.

**Resources:**
[Schema changes](https://docs.getdbt.com/docs/build/incremental-models#what-if-the-columns-of-my-incremental-model-change)
