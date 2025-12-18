## Leveraging Environment Variables

**What do we want to achieve**

<img width="725" height="292" alt="image" src="https://github.com/user-attachments/assets/6225e385-4d0b-44fc-98b3-a135a2bf5525" />

By default, the resulting schema is the concatenation of the **target schema** and the **custom schema** separated by an underscore. But in our case we don't want any concatenation to happen, we want only just the custom schema.

Let's try to change this configuration using environment variables.

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
3. Go to **Orchestration** -> **Environments** -> **Environment variables**
4. Create a variable called `DBT_MY_ENV`.
    - Project default - None (blank)
    - Development - dev
    - QA - qa (depends if you have QA env in your project)
    - Production - prod
