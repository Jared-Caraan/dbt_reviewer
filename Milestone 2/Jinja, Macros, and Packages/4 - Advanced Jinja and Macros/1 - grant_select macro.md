## grant_select macro

This macro is intended to grant privileges and permission on Snowflake database objects within a specified database and/or schema.

Create a new macro under the `macros` folder and name it `grant_select.sql`.

**grant_select.sql**
```sql
{% macro grant_select(schema=target.schema, role=target.role) %}

  {% set sql %}
  grant usage on schema {{ schema }} to role {{ role }};
  grant select on all tables in schema {{ schema }} to role {{ role }};
  grant select on all views in schema {{ schema }} to role {{ role }};
  {% endset %}

  {{ log('Granting select on all tables and views in schema ' ~ target.schema ~ ' to role ' ~ role, info=True) }}
  {% do run_query(sql) %}
  {{ log('Privileges granted', info=True) }}

{% endmacro %}
```

- The `run_query` macro macro provides a convenient way to run queries and fetch their results.
- The `target` variable contains information about your connection to the warehouse.
- The `log` logs a line to either the log file or stdout

To run the macro on the command line only, execute the command `dbt run-operation <macro_name>`.

> [!NOTE]
> A tilde in Jinja means concatenation

**Resources**:
- [run_query macro documentation](https://docs.getdbt.com/reference/dbt-jinja-functions/run_query)
- [log macro documentation](https://docs.getdbt.com/reference/dbt-jinja-functions/log)
- [target variable documentation](https://docs.getdbt.com/reference/dbt-jinja-functions/target)
