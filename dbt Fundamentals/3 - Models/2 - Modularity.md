## Modularity
This is the process of breaking down a system's components into parts that can easily be assembled. This kind of thinking can be applied to data modeling. Instead of putting every logic in one model, we can separate each pieces into different dbt models. This also allows the developer to reuse models in different places as needed.

## Modularizing a Model
Let's start modularizing this query:
```sql
with customers as (
    select
        id as customer_id,
        first_name,
        last_name
    from raw.jaffle_shop.customers
),
orders as (
    select
        id as order_id,
        user_id as customer_id,
        order_date,
        status
    from raw.jaffle_shop.orders
),
customer_orders as (
    select
        customer_id,
        min(order_date) as first_order_date,
        max(order_date) as most_recent_order_date,
        count(order_id) as number_of_orders
    from orders
    group by 1
),
final as (
    select
        customers.customer_id,
        customers.first_name,
        customers.last_name,
        customer_orders.first_order_date,
        customer_orders.most_recent_order_date,
        coalesce(customer_orders.number_of_orders, 0) as number_of_orders
    from customers
    left join customer_orders using (customer_id)
)
select * from finalr_orders using (customer_id)
)
select * from final
```
1. First is to copy the *customers* section on the CTE to another model.
2. Create a new sql file under the *models* folder. In this example, I named it `stg_jaffle_shop__customers.sql`. This followed the convention *stg_<schema_name>__<file_name>*.
3. Copy this query into `stg_jaffle_ship__customers.sql` and hit **Save**.
```sql
select
    id as customer_id,
    first_name,
    last_name
from raw.jaffle_shop.customers
```
4. Do the same thing for orders. Create a sql file named `stg_jaffle_shop__orders.sql` and copy the query below. Then click **Save**.
```sql
select
    id as order_id,
    user_id as customer_id,
    order_date,
    status
from raw.jaffle_shop.orders
```
## Using the `ref` function
The `ref` function allows you to reuse the logic of a dbt model to another dbt model without hardcoding the object name beneath it.
The syntax would be `{{ ref('<model_name>') }}`
1. Apply the `ref` function for both the *customers* and *orders* query. The final query should look something like this.
```sql
with customers as (

    select * from {{ ref("stg_jaffle_shop__customers") }}

),
orders as (

    select * from {{ ref("stg_jaffle_shop__orders") }}
    
),
customer_orders as (
    select
        customer_id,
        min(order_date) as first_order_date,
        max(order_date) as most_recent_order_date,
        count(order_id) as number_of_orders
    from orders
    group by 1
),
final as (
    select
        customers.customer_id,
        customers.first_name,
        customers.last_name,
        customer_orders.first_order_date,
        customer_orders.most_recent_order_date,
        coalesce(customer_orders.number_of_orders, 0) as number_of_orders
    from customers
    left join customer_orders using (customer_id)
)
select * from final
```
2. The lineage now also looks more promising as we can have a better understanding of the data flow and model dependencies. Both `stg__` models are the upstream models followed by the downstream model which is `customers.sql`
<img width="665" height="323" alt="image" src="https://github.com/user-attachments/assets/96bcfd6e-1f9f-4e0f-98be-5a4074fa9843" />
