What is the primary purpose of the `run_query` macro in dbt?

a. To log the results of a SQL query.\
b. To execute a SQL query against the warehouse and return the results.\
c. To validate the syntax of a SQL query.\
d. To compile SQL code without executing it.

Answer: b

##
Which Jinja function would you use to dynamically log messages during the execution of a dbt macro?

a. `run_query`\
b. `do`\
c. `log`\
d. `execute`

Answer: c

##
How would you use the `target` variable to set a default schema in a macro that grants select permissions?

a. `{{ target.database }}`\
b. `{{ target.schema }}`\
c. `{{ target.name }}`\
d. `{{ target.role }}`

Answer: b

##
In the context of advanced Jinja in dbt, what is the purpose of the `execute` variable?

a. It is used to validate whether SQL code is executable.\
b. It logs the execution time of SQL queries.\
c. It sets the environment for dbt (e.g., development, production).\
d. It determines if dbt is in execute mode and can run SQL queries.

Answer: d

##
Which of the following is the correct syntax for using environment variables within a macro?

A.
```sql
{% macro generate_schema_name(custom_schema_name, node) -%}
    {%- set default_schema = target.schema -%}
    {%- set env = env_var('VAR_NAME') -%}
    {%- if custom_schema_name is none or env == 'dev' -%}
        {{ default_schema }}
    {%- else -%}
        {{ custom_schema_name | trim }}
    {%- endif -%}
{%- endmacro %}
```

B.
```sql
{% macro generate_schema_name(custom_schema_name, node) -%}
    {%- set default_schema = target.schema -%}
    {%- set env = env-var('DBT_ENV_NAME') -%}
    {%- if custom_schema_name is none or env == 'dev' -%}
        {{ default_schema }}
    {%- else -%}
        {{ custom_schema_name | trim }}
    {%- endif -%}
{%- endmacro %}
```

C.
```sql
{% macro generate_schema_name(custom_schema_name, node) -%}
    {%- set default_schema = target.schema -%}
    {%- set env = {{ env_var('DBT_ENV_NAME') }} -%}
    {%- if custom_schema_name is none or env == 'dev' -%}
        {{ default_schema }}
    {%- else -%}
        {{ custom_schema_name | trim }}
    {%- endif -%}
{%- endmacro %}
```

D.
```sql
{% macro generate_schema_name(custom_schema_name, node) -%}
    {%- set default_schema = target.schema -%}
    {%- set env = env_var('DBT_ENV_NAME') -%}
    {%- if custom_schema_name is none or env == 'dev' -%}
        {{ default_schema }}
    {%- else -%}
        {{ custom_schema_name | trim }}
    {%- endif -%}
{%- endmacro %}
```

a. A\
b. B\
c. C\
d. D

Answer: d
