## Translating Hard Coded Tables

The first thing we'll do with our legacy code is look for all of our hardcoded table references and replace them with the source function.

1. Create a subfolder under your `models` folder called `marts`.
2. Create a subfolder under your `models` folder called `staging`.
3. Under your `models > staging` folder, create two subfolders - one for each source schema that our original query pulls from.  These subfolders are `stripe` and `jaffle_shop`.
4. Create a file under `models > staging > jaffle_shop` called `_sources.yml`.
5. Create a file under `models > staging > stripe` called `_sources.yml`.
6. Declare configurations for the corresponding source in each file:

**models/staging/jaffle_shop/_sources.yml**
```yaml
version: 2

sources:
  - name: jaffle_shop
    database: raw
    tables:
      - name: customers
      - name: orders
```
**models/staging/stripe/_sources.yml**
```yaml
version: 2

sources:
  - name: stripe
    database: raw
    tables:
      - name: payment

```
7. Now that your sources are configured, open your customer_orders.sql file and replace any hardcoded references (i.e, raw.jaffle_shop.customers) with a source function, referencing the sources you have set up.
```sql
select 
    orders.id as order_id,
    orders.user_id as customer_id,
    last_name as surname,
    first_name as givenname,
    first_order_date,
    order_count,
    total_lifetime_value,
    round(amount/100.0,2) as order_value_dollars,
    orders.status as order_status,
    payments.status as payment_status
from {{ source('jaffle_shop', 'orders') }} as orders

join (
      select 
        first_name || ' ' || last_name as name, 
        * 
      from {{ source('jaffle_shop', 'customers') }}
) customers
on orders.user_id = customers.id

join (

    select 
        b.id as customer_id,
        b.name as full_name,
        b.last_name as surname,
        b.first_name as givenname,
        min(order_date) as first_order_date,
        min(case when a.status NOT IN ('returned','return_pending') then order_date end) as first_non_returned_order_date,
        max(case when a.status NOT IN ('returned','return_pending') then order_date end) as most_recent_non_returned_order_date,
        COALESCE(max(user_order_seq),0) as order_count,
        COALESCE(count(case when a.status != 'returned' then 1 end),0) as non_returned_order_count,
        sum(case when a.status NOT IN ('returned','return_pending') then ROUND(c.amount/100.0,2) else 0 end) as total_lifetime_value,
        sum(case when a.status NOT IN ('returned','return_pending') then ROUND(c.amount/100.0,2) else 0 end)/NULLIF(count(case when a.status NOT IN ('returned','return_pending') then 1 end),0) as avg_non_returned_order_value,
        array_agg(distinct a.id) as order_ids

    from (
      select 
        row_number() over (partition by user_id order by order_date, id) as user_order_seq,
        *
      from {{ source('jaffle_shop', 'orders') }}
    ) a

    join ( 
      select 
        first_name || ' ' || last_name as name, 
        * 
      from {{ source('jaffle_shop', 'customers') }}
    ) b
    on a.user_id = b.id

    left outer join {{ source('stripe', 'payment') }} c
    on a.id = c.orderid

    where a.status NOT IN ('pending') and c.status != 'fail'

    group by b.id, b.name, b.last_name, b.first_name

) customer_order_history
on orders.user_id = customer_order_history.customer_id

left outer join {{ source('stripe', 'payment') }} payments
on orders.id = payments.orderid

where payments.status != 'fail'
```
8. Conduct a `dbt run -m customer_orders` to ensure that your sources are configured properly and your model builds successfully in the warehouse.
