## CTEs or Intermediate Models

**Continue to reorganize code**

1. Move the filter for `payment_status` found in the `customer_order_history` and `final` CTEs to the import CTE for payments, so we are working on a limited data set before our calculations and transformations.

   <details>
   <summary>Revised payments CTE</summary>

   ```sql
   payments as (

      select * from {{ ref('stg_stripe__payments') }}
      where payments.payment_status != 'fail'

   ),
   ```
   </details>
   
2. Remove the filter on order_status - this doesn't actually filter out anything.

   <details>
   <summary>Remove this filter</summary>

   ```sql
   where orders.order_status not in ('pending')
   ```
   </details>
   
3. In `fct_customer_orders`, create a new CTE above the customer_order_history CTE. Call this CTE order_totals. From the payments table, get the order_id, payment_status, and the total amount of the order - the final result of this CTE should be at the order_id grain.

   <details>
   <summary>order_totals CTE</summary>

   ```sql
   order_totals as (

      select
          order_id,
          payment_status,
          sum(payment_amount) as order_value_dollars
      from payments
      group by 1,2
   )
   ```
   </details>

4. Under the `order_totals` CTE, create a new CTE called `order_values_joined` and join orders data set with the previous CTE to get a new result set of all orders with associated payment status and total information.

   <details>
   <summary>order_values_joined CTE</summary>

   ```sql
   order_values_joined as (
       select
           orders.*,
           order_totals.payment_status,
           order_totals.order_value_dollars
       from orders
       left join order_totals
       on orders.order_id = order_totals.order_id
   )
   ```
   </details>

5. In the `final` CTE, since payments information will be included with orders in future work, remove the join to the `payments` table and rereference any fields from `payments.` to `orders.`. Do the same with `customer_order_history's` reference to payments data.

   <details>
   <summary>Remove this join in final CTE</summary>

   ```sql
   left outer join payments
   on orders.order_id = payments.order_id
   ```
   </details>

6. In the `customer_order_history` CTE, copy the `case when orders.order_status not in ('returned', 'pending') then order_date end` statement and move this logic into the staging model `stg_jaffle_shop__orders` as `valid_order_date`.

   <details>
   <summary>Revised staging orders</summary>

   ```sql
   with

   source as (
    
        select * from {{ source('jaffle_shop', 'orders') }}
    
    ),
    
    transformed as (
    
          select
    
            id as order_id,
            user_id as customer_id,
            order_date,
            status as order_status,
    
            case 
                when order_status not in ('returned','return_pending') 
                then order_date 
            end as valid_order_date,
    
            row_number() over (
                partition by user_id 
                order by order_date, id
            ) as user_order_seq,
    
          from source
    
    )
    
    select * from transformed
   ```
   </details>

7. Back in `fct_customer_orders`, reference the `orders.valid_order_date` anywhere the case when statement is written. 
8. The `case when orders.order_status != 'returned' then 1 end` was a piece of logic that was supposed to be changed to the new logic on `not in ('returned', 'pending')`. Replace this with the new field from step 6.

9. Places where there is the order status logic, but assigning a different value for the `then` clause can simply use `orders.valid_order_date` is not null

   <details>
   <summary>Current query of the fact table</summary>

   ```sql
   with

    -- Import CTEs
    customers as (
    
        select * from {{ ref('stg_jaffle_shop__customers') }}
    
    ),
    
    orders as (
    
        select * from {{ ref('stg_jaffle_shop__orders') }}
    
    ),
    
    payments as (
    
        select * from {{ ref('stg_stripe__payments') }}
        where payments.payment_status != 'fail'
    
    ),
    
    order_totals as (
    
        select
            order_id,
            payment_status,
            sum(payment_amount) as order_value_dollars
        from payments
        group by 1,2
    ),
    
    order_values_joined as (
        select
            orders.*,
            order_totals.payment_status,
            order_totals.order_value_dollars
        from orders
        left join order_totals
        on orders.order_id = order_totals.order_id
    ),
    
    customer_order_history as (
    
        select
            customers.customer_id,
            customers.full_name,
            customers.surname,
            customers.givenname,
            min(orders.order_date) as first_order_date,
    
            min(orders.valid_order_date) as first_non_returned_order_date,
    
            max(orders.valid_order_date) as most_recent_non_returned_order_date,
    
            coalesce(max(orders.user_order_seq),0) as order_count,
    
            coalesce(count(case 
                when orders.valid_order_date is not null
                then 1 end),
                0
            ) as non_returned_order_count,
    
            sum(case 
                when orders.valid_order_date is not null
                then orders.order_value_dollars 
                else 0 
            end) as total_lifetime_value,
    
            sum(case 
                when orders.valid_order_date is not null
                then orders.order_value_dollars 
                else 0 
            end)
            / nullif(count(case 
                when orders.valid_order_date is not null
                then 1 end),
                0
            ) as avg_non_returned_order_value,
    
            array_agg(distinct orders.order_id) as order_ids
    
        from orders
    
        join customers
        on orders.customer_id = customers.customer_id
    
        group by customers.customer_id, customers.full_name, customers.surname, customers.givenname
    
    ),
    
    -- Final CTEs 
    final as (
    
        select 
    
            orders.order_id,
            orders.customer_id,
            customers.surname,
            customers.givenname,
            first_order_date,
            order_count,
            total_lifetime_value,
            orders.order_value_dollars,
            orders.order_status,
            orders.payment_status
    
        from orders
    
        join customers
        on orders.customer_id = customers.id
    
        join customer_order_history
        on orders.customer_id = customer_order_history.customer_id
    
    )
    
    -- Simple Select Statement
    select * from final
   ```
   </details>

##

**Moving logic to intermediate models**

Now we're going to break up our code into an intermediate model.

1. In the `marts` folder, create a folder called `intermediate`.

2. Create a new file in `marts > intermediate` called `int_orders.sql`.

3. Within `int_orders.sql`, import the `stg_jaffle_shop__orders` model and the `stg_stripe__payments` model. Remove these from the `fct_customer_orders` model.

4. Cut from the `fct_customer_orders` model the two CTEs we created above - `order_totals` and `order_values_joined`. Paste these under the import statements in the `int_orders` model, making sure to add your simple select statement at the bottom.

   <details>
   <summary>int_orders</summary>

   ```sql
   with

    orders as (
    
        select * from {{ ref('stg_jaffle_shop__orders') }}
    
    ),
    
    payments as (
    
        select * from {{ ref('stg_stripe__payments') }}
        where payments.payment_status != 'fail'
    
    ),
    
    order_totals as (
    
        select
            order_id, 
            payment_status,
            sum(payment_amount) as order_value_dollars
        from payments
        group by 1,2
    ),
    
    order_values_joined as (
        select
            orders.*,
            order_totals.payment_status,
            order_totals.order_value_dollars
        from orders
        left join order_totals
        on orders.order_id = order_totals.order_id
    )
    
    select * from order_values_joined
   ```
   </details>

5. In `fct_customer_orders`, import the `int_orders` model as a CTE named `orders`.

   <details>
   <summary>Intermediary reference</summary>

   ```sql
   orders as (

        select * from {{ ref('stg_jaffle_shop__orders') }}
    
    ),
   ```
   </details>
   
6. Conduct a `dbt run -m +fct_customer_orders` to ensure your models build successfully.
