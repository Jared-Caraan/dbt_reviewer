## Centralizing Logic in Staging Models

**Move 1:1 transformations to CTEs**
1. Ignoring the import CTEs comment, identify where the staging CTEs are. Our staging models, aim to transform just the source. These CTEs don't conduct any joins - notate above this section of CTEs with a comment that says `-- staging`.

   <details>
   <summary>Staging CTEs</summary>
      
   ```sql
   -- staging
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
   )
   ```
   </details>

3. Identify where the marts CTEs are. Whenever we're talking about marts models that is typically indicated by joins and that's because whenever we're joining, what we're typically trying to achieve is we're trying to achieve a different concept that's going to help in our analyses. These CTEs conduct joins - notate above this section of CTEs with a comment that says `-- marts`.

   <details>
   <summary>Marts CTEs</summary>
      
   ```sql
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
   </details>

4. Remove any redundant CTEs that conduct the same transformations on the same data sets. Replace all references to any removed CTEs with the proper references.

5. In the marts area, look at each field and identify the transformations that answer Yes to both of these questions:

   - Can this transformation be done using one data set?
   - Is this transformation done on a field whose value is not due to a join?
   - For example: `case when data_set.status is null` looks like it can be done using one data set, but if the status is null because the row wasn't joined with other data, then doing this earlier than where the join occurs will result in incorrect calculations.

Move these transformations to the appropriate CTE under the -- staging section of code. Ensure that when you move these, you are:

   - Removing redundant transformations
   - Re-referencing the CTE and field names correctly
   - Giving good names to fields that don't have a good name established

5. There was not a subquery that operated only on the `payments` table. Create a new CTE under the -- staging area that selects from the payments CTE, and continue moving transformations that belong to payment data following the rules in step 4.

**Move transformations to staging models**
Once you're done with the above, It's time to split out the code under `-- staging` and create models!

1. Under `staging > jaffle_shop` create files called `stg_jaffle_shop__customers.sql` and `stg_jaffle_shop__orders.sql`.

2. Under `staging > stripe` create a file called stg_stripe__payments.sql.

3. Starting with stg_jaffle_shop__customers.sql, cut from the fct_customer_orders.sql and paste the CTE that operates only on the customers data.

You then need to structure your code as we did in fct_customer_orders.sql:
```sql
with

source as (

    select * from {{ source('jaffle_shop', 'customers') }}

),

transformed as (

    select 

        id as customer_id,
        last_name as surname,
        first_name as givenname,
        first_name || ' ' || last_name as full_name

    from source

)

select * from transformed
```
Do the same with `stg_jaffle_shop__orders.sql` and `stg_stripe__payments.sql`.

4. Back in `fct_customer_orders.sql`, ensure you've moved all of your `-- staging` CTEs into staging models and remove the code, if you haven't already. Change your **import CTEs** to use the `{{ ref() }}` function to refer to your new staging models instead of the source. Ensure everything is referenced correctly in subsequent CTEs.

5. Finally, run `dbt run -m +fct_customer_orders` to ensure your models build successfully.
