## Centralizing Logic in Staging Models

**Move 1:1 transformations to CTEs**
1. Ignoring the import CTEs, identify where the staging CTEs are. These CTEs don't conduct any joins - notate above this section of CTEs with a comment that says `-- staging`.

2. Identify where the marts CTEs are. These CTEs conduct joins - notate above this section of CTEs with a comment that says `-- marts`.

3. Remove any redundant CTEs that conduct the same transformations on the same data sets. Replace all references to any removed CTEs with the proper references.

4. In the marts area, look at each field and identify the transformations that answer Yes to both of these questions:

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
