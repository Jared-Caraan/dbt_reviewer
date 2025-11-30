## Cents to Dollars macro

1. In the `macros` folder, create a new file named `cents_to_dollars.sql`.
2. To start a macro, create the macro tag along with the macro name with a parenthesis.
   <details>
   <summary>Beginning macro tag</summary>
  
   ```jinja
   {% macro cents_to_dollars() %}
   ```
   </details>

3. Create the end macro tag.
   <details>
   <summary>End macro tag</summary>
  
   ```jinja
   {% endmacro %}
   ```
   </details>

4. Add the logic in the middle between the two macro tags.
   <details>
   <summary>Basic macro logic</summary>
  
   ```jinja
   {% macro cents_to_dollars() %}
     amount / 100
   {% endmacro %}
   ```
   </details>

 5. Make it more dynamic, like adding the column name as an input parameter.
 6. Add a feature to round-off to a specific significant value.
 7. Replace the original SQL query with the macro function.
 8. Create a macros documentation under the `macros` folder and name it `_macros_docs.yml`

    <details>
    <summary>Macro doc</summary>
  
    ```yaml
    macros:
    - name: cents_to_dollars
      description: A macro that converts dollars to cents and rounds to the user input decimal places, or 2 if none is provided.
      arguments:
        - name: column_name
          type: string
          description: The name of the column you want to convert
        - name: decimals
          type: integer
          description: Number of decimal places, defaults to 2

    ```
    </details>
    
<details>
<summary>Final macro</summary>

```sql
{% macro cents_to_dollars(column_name, decimals=2) -%}
    ROUND({{column_name}} / 100, {{decimals}})
{%- endmacro %}
```
</details>
<details>
<summary>Query without Macro</summary>

```sql
select
    id as payment_id,
    orderid as order_id,
    paymentmethod as payment_method,
    status,

    -- amount is stored in cents, convert it to dollars
    amount / 100 as amount,
    created as created_at

from {{ source('stripe', 'payment') }}
```
</details>
<details>
<summary>Query with Macro</summary>

```sql
select
    id as payment_id,
    orderid as order_id,
    paymentmethod as payment_method,
    status,

    -- amount is stored in cents, convert it to dollars
    {{ cents_to_dollars("amount", 4) }} as amount,
    created as created_at

from {{ source('stripe', 'payment') }}
```
</details>
