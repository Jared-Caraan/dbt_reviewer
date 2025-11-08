## CTE Groupings and Cosmetic Cleanups

1. The cosmetic cleanups in this video are listed below. Use this guideline to refactor the cosmetics of your `fct_customer_orders` model:

   - Add whitespacing
   - No lines over 80 characters
   - Lowercased keywords

2. CTE restructuring

   Refactor your code to follow this structure:
   ```sql
   -- with statement
   -- import CTEs
   -- logical CTEs
   -- final CTE
   -- simple select statement
   ```

   a) Add a `with` statement to the top of your `fct_customer_orders` model

   b) Add **import CTEs** after the `with` statement for each source table that the query uses. Ensure that subsequent `from` statements after the import CTEs reference the named CTEs rather than the `{{ source() }}`.

   c) Move any subqueries into their own CTEs, and then reference those CTEs instead of the subquery.

   d) Wrap the remaining `select` statement in a CTE and call this CTE `final`.

   e) Add a simple select statement at the end - `select * from final`.

Exemplar:

**fct_customer_orders.sql**

```sql
with

-- Import CTEs
base_customers as (
    select * from {{ source('jaffle_shop', 'customers') }}
),

orders as (
    select * from {{ source('jaffle_shop', 'orders') }}
),

payments as (
    select * from {{ source('stripe', 'payment') }}
),

-- Logical CTEs
customers as (
    select 
        first_name || ' ' || last_name as name, 
        * 
    from base_customers
),

a as (
      select 
        row_number() over (
            partition by user_id 
            order by order_date, id
        ) as user_order_seq,
        *
      from orders
),

b as ( 
    select 
        first_name || ' ' || last_name as name, 
        *
    from customers
),

customer_order_history as (
    select 
        b.id as customer_id,
        b.name as full_name,
        b.last_name as surname,
        b.first_name as givenname,

        min(order_date) as first_order_date,

        min(case 
            when a.status not in ('returned','return_pending') 
            then order_date 
        end) as first_non_returned_order_date,

        max(case 
            when a.status not in ('returned','return_pending') 
            then order_date 
        end) as most_recent_non_returned_order_date,

        coalesce(max(user_order_seq),0) as order_count,

        coalesce(count(case 
            when a.status != 'returned' 
            then 1 end),
            0
        ) as non_returned_order_count,

        sum(case 
            when a.status not in ('returned','return_pending') 
            then round(c.amount/100.0,2) 
            else 0 
        end) as total_lifetime_value,

        sum(case 
            when a.status not in ('returned','return_pending') 
            then round(c.amount/100.0,2) 
            else 0 
        end)
        / nullif(count(case 
            when a.status not in ('returned','return_pending') 
            then 1 end),
            0
        ) as avg_non_returned_order_value,

        array_agg(distinct a.id) as order_ids

    from a

    join b
    on a.user_id = b.id

    left outer join payments as c
    on a.id = c.orderid

    where a.status not in ('pending') and c.status != 'fail'

    group by b.id, b.name, b.last_name, b.first_name

),

-- Final CTEs 
final as (
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

    from orders

    join customers
    on orders.user_id = customers.id

    join customer_order_history
    on orders.user_id = customer_order_history.customer_id

    left outer join payments
    on orders.id = payments.orderid

    where payments.status != 'fail'

)

-- Simple Select Statement
select * from final
```
