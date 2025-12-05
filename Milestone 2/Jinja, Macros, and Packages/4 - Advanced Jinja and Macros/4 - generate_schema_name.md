## generate_schema_name macro

dbt uses a default macro called `generate_schema_name` to determine the name of the schema that a model should be built in.

If your dbt project has a custom macro called `generate_schema_name`, dbt will use it instead of the default macro. This allows you to customize the name generation according to your needs.

**default generate_schema_name macro**

```sql
{% macro generate_schema_name(custom_schema_name, node) -%}

    {%- set default_schema = target.schema -%}
    {%- if custom_schema_name is none -%}

        {{ default_schema }}

    {%- else -%}

        {{ default_schema }}_{{ custom_schema_name | trim }}

    {%- endif -%}

{%- endmacro %}
```

> [!WARNING]
> Don't replace `default_schema` in the macro

**Resources**
- [Custom schema names](https://docs.getdbt.com/docs/build/custom-schemas)

## Customizing schema name per environment

You can do this by configuring **environment variables**

1. On the side panel -> **Orchestration** -> **Environments** -> **Environment variables** -> **Add variable**
2. Provide an arbitrary name to **Key**, then provide a value for **Dev** and **Prod**. Then hit Save.
3. Use the templated environment variable on the `generate_schema_name` macro.

**customized generate_schema_name macro**

```sql
{% macro generate_schema_name(custom_schema_name, node) -%}

    {%- set default_schema = target.schema -%}
    {%- set env = env_var('DBT_KEY') -%}
    {%- if custom_schema_name is none or env != 'prod' -%}

        {{ default_schema }}

    {%- else -%}

        {{ default_schema }}_{{ custom_schema_name | trim }}

    {%- endif -%}

{%- endmacro %}
```
