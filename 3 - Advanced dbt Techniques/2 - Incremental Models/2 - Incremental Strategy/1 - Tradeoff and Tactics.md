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
where
updated_at >= (select max(updated_at) from {{this}})
```
