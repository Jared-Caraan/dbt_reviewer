## What is the target variable in dbt?

**Target** is a variable accessible in any Jinja macro or code block that contains information about the active connection to your warehouse, like the type of warehouse dbt is connecting to, the credentials used to connect to the warehouse, etc.

**target.name**
dbt Cloud gives us the ability to configure what value will be stored in `target.name`. The target name is configured for each developer and for each job, and can be accessed in a Jinja block of any dbt code by reading the variable target.name

At the job level, the target name can be configured by navigating to the job settings in **Orchestration** --> **Jobs**. As mentioned, each developer also has a target name defined for their development environment in the dbt Cloud IDE. It can be configured by navigating to **_Your Name_** -> **Your profile** -> **Credentials**

## Leveraging Target Variable

**What do we want to achieve**

<img width="725" height="292" alt="image" src="https://github.com/user-attachments/assets/6225e385-4d0b-44fc-98b3-a135a2bf5525" />

By default, the resulting schema is the concatenation of the **target schema** and the **custom schema** separated by an underscore. But in our case we don't want any concatenation to happen, we want only just the custom schema.

Let's try to change this configuration using `target.name`.

1. First is to grab the default macro for generating a model's schema name, and make our version out of it later.

    <details>
    <summary>Generate Schema Name Macro</summary>

    **generate_schema_name.sql**
   
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
    </details>

2. Under the `macros` folder, create a file called `generate_schema_name.sql`. Then, paste the code into that file. Whatever you revision you put in this script will override the default macro activity.
3. Add a logic that would produce only the **custom_schema_name** only in production.

    <details>
    <summary>Revised Generate Schema Name Macro</summary>
    
    **generate_schema_name.sql**
    
    ```sql
    {% macro generate_schema_name(custom_schema_name, node) -%}
    
        {%- set default_schema = target.schema -%}
        {%- if custom_schema_name is none -%}
    
            {{ default_schema }}
    
        {%- elif target.name in ['prod'] -%}
    
            {{ custom_schema_name | trim }}
    
        {%- else -%}
    
            {{ default_schema }}_{{ custom_schema_name | trim }}
    
        {%- endif -%}
    
    {%- endmacro %}
    ```
    </details>

**Resources**
- [target variable](https://docs.getdbt.com/reference/dbt-jinja-functions/target)
