## union_tables_by_prefix macro

The purpose of this macro is to unionize tables that has names which complies with the given prefix.

**union_tables_by_prefix macro code:**

```sql
{%- macro union_tables_by_prefix(database, schema, prefix) -%}

  {%- set tables = dbt_utils.get_relations_by_prefix(database=database, schema=schema, prefix=prefix) -%}

  {% for table in tables %}

      {%- if not loop.first -%}
      union all 
      {%- endif %}
        
      select * from {{ table.database }}.{{ table.schema }}.{{ table.name }}
      
  {% endfor -%}
  
{%- endmacro -%}
```

**union_tables_by_orders_prefix model code:**

```sql
{{ union_tables_by_prefix(
    database='raw',
    schema='dbt_learn_jinja', 
    prefix='orders__' 
    )      
}}
```


> [!WARNING]
> The macro `get_relations_by_prefix` will soon be deprecated in favor of the more flexible `get_relations_by_pattern macro`

**Resources:**
- [execute variable documentation](https://docs.getdbt.com/reference/dbt-jinja-functions/execute)
- [agate file types documentation](https://agate.readthedocs.io/en/latest/api/table.html#agate.Table.columns)
- [get_relations_by_prefix documentation](https://github.com/dbt-labs/dbt-utils?tab=readme-ov-file#get_relations_by_prefix-source)
