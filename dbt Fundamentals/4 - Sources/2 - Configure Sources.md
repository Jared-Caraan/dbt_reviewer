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
