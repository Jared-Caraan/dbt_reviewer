You are auditing your dbt project's DAG. Where will sources appear?

a. Sources are the last node in a DAG, all the way to the right.\
b. Sources are the second node in a DAG, connected to the raw data.\
c. Sources are the first node in a DAG, all the way to the left.\
d. Sources appear directly to the right of a model in the DAG.

Answer: c

##
Consider this yaml file.

`models/staging/jaffle_shop/_stg_tpch.yml`
```yaml
sources:
  - name: tpch
    database: snowflake_sample_data
    schema: tpch_prod
    tables:
      - name: orders
      - name: customers
      - name: order_items
```
How will you correctly select all from customers utilizing the source macro?

a. `select * from {{source('snowflake_sample_data','customers')`\
b. `select * from {{ source('tpch','customers') }}`\
c. `select * from {{ source('tpch_prod','customers') }}`\
d. `select * from {{ source('customers','tpch') }}`

Answer: b

##
You have a table in your data platform called `raw.jaffle_shop.orders`.

You are attempting to run this select statement to preview the 'orders' source:

`select * from {{ source( 'jaffle_shop', 'orders') }}`

This statement is not running. Examine this YAML configuration :
```yaml
sources:
  - name: jaffle_shop
    database: jaffle_shop
    schema: raw  
    tables:
      - name: orders
      - name: customers
```
What is the problem with this YAML file?

a. The source name is `jaffle_shop`, and should replace `raw` in the source macro.\
b. The database and the schema field should be swapped.\
c. The schema name and database name should match.\
d. The source macro should also include the database name in addition to the schema name.

Answer: b

##
You have written the following source file, but are encountering a syntax error:

`models/staging/jaffle_shop/_stg_analytics.yml`
```yaml
sources:
  - name: analytics
    database: raw
    schema: analytics
    tables:
        - name: agg_customer_orders__all_time
      - name: agg_regions_segments
```
What went wrong?

a. The names of tables should come before the name of the source.\
b. The line identifying `agg_customer_orders_all_time` is indented one tab too far.\
c. The database and schema names should always match.\
d. The "tables" key should be indented to match the indentation of `agg_customer_orders__all_time`.

Answer: b

##
What is the purpose of declaring a source in dbt?

a. Tells dbt the pre-existing data to query from the data platform.\
b. Tells dbt what data to copy from the data platform into dbt.\
c. Tells dbt what data should be stored in tables and not views.\
d. Tells dbt where to store your transformation results.

Answer: a

##
A new model that you are creating needs to reference your `jaffle_orders_information_table`.

Examine this source configuration:
```yaml
sources:
  - name: jaffle_shop
    database: raw  
    schema: jaffle_shop_dataset 
    tables:
      - name: orders
        identifier: jaffle_orders_information_table
      - name: customers
        identifier: jaffle_customers_information_table
```
How would you reference this information using the source macro?

a. `{{ source('jaffle_shop', 'jaffle_orders_information_table') }}`\
b. `{{ source('jaffle_shop_dataset', 'orders') }}`\
c. `{{ source('jaffle_shop', 'orders') }}`\
d. `{{ source('jaffle_shop_dataset', 'jaffle_orders_information_table') }}`

Answer: c
