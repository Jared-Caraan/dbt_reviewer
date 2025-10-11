## Configure Sources

We will configure the sources in our existing demo project *jaffle shop*. Currently, all sources are hardcoded so we want to tweak and change that into something more dynamic.

<img width="656" height="283" alt="image" src="https://github.com/user-attachments/assets/f58102ec-5af9-42bf-9edc-d788fddb8334" />

1. Under `staging/jaffle_shop` directory, create a new YAML file named as `_src_jaffle_shop.yml`. Similarly, under `staging/stripe` directory, create a new YAML file named as `_src_stripe.yml`.
> [!NOTE]
> The underscore at the front of the source yaml ensures that it always appears at the top of the directory
2. In your `_src_jaffle_shop.yml`, put this following code
```yaml
sources:
  - name: jaffle_shop
    database: raw
    schema: jaffle_shop
    tables:
      - name: customers
      - name: orders
```
Then, in your `_src_stripe.yml`, put this following code
```yaml
sources:
  - name: stripe
    database: raw
    schema: stripe
    tables:
      - name: payment
```
> [!TIP]
> To avoid typing everything on source configuration, you can type `__source`.
> 
3. Replace the hardcoded source in `stg_jaffle_shop__orders.sql`. The code should now be similar to this:
```sql
select
    id as order_id,
    user_id as customer_id,
    order_date,
    status
from {{ source('jaffle_shop', 'orders') }}
```
4. Replace the hardcoded source in `stg_jaffle_shop__customers.sql`. The code should now be similar to this:
```sql
select
    id as customer_id,
    first_name,
    last_name
from {{ source('jaffle_shop', 'customers') }}
```
5. Replace the hardcoded source in `stg_stripe__payments.sql`. The code should now be similar to this:
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
6. Execute `dbt run` to verify your objects.
7. Commit and merge once done.

You can also write source configurations using **codegen** package from [hub.getdbt.com](http://hub.getdbt.com/)

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
``name: jaffle_shop`` - This is the name you'll use in the source function. It identifies the database and the schema. This means that `jaffle_shop` refers to `raw.jaffle_shop_dataset`.

``name: orders`` - This is the name you'll use in the source function. It identifies the table name. The hardcoded value would be `raw.jaffle_shop_dataset.jaffle_orders_information_table`

If there are no `identifier:`, then ``name: orders`` points to its literal table name. The hardcoded value would be `raw.jaffle_shop_dataset.orders`.
