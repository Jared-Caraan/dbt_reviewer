## Configuring Incremental Models

**Materializing model as incremental**

```sql
{{
    config(
        materialized='incremental'
    )
}}
```

**How do we know which rows are the new ones?**

```sql
{{
    config(
        materialized='incremental'
    )
}}

select * from {{ ref('fct_marketing_web_analysis') }}
where
updated_at >= (select max(updated_at) from {{this}})
```

`{{this}}` represents the currently existing database object mapped to this model. We're selecting from (and then building) new rows after the most recent `updated_at` timestamp from the currently existing version of the model in your warehouse.

**is_incremental()**

- The `is_incremental()` macro powers incremental materializations. It will return `True` if all of the following conditions are met:
  - The model must already exist in the database
  - The full-refresh flag is not passed e.g. `dbt run --full-refresh`
  - The running model is configured with `materialized = 'incremental'`
- To tell dbt which rows it should transform on an incremental run, wrap valid SQL that filters for these rows in the `is_incremental()` macro.

```sql
{{
    config(
        materialized='incremental'
    )
}}

select * from {{ ref('fct_marketing_web_analysis') }}
{% if is_incremental() %}
where
updated_at >= (select max(updated_at) from {{this}})
{% endif %}
```

> [!TIP]
> The shortcut for the incremental materialization config block is `__config-incremental`

> [!NOTE]
> When you click **Preview** on an incremental model, it will show you the new rows only. But it will materialize all old + new rows in the data platform.
