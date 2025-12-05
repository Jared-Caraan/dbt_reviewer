## Building Data Tests

We will add some data tests on our ongoing `jaffle_shop` project.

1. Create a yaml file under `staging/jaffle_shop` and name it `_stg_jaffle_shop.yml`. This is where you will put your dbt tests for `customers` and `orders`.
2. Inside `_stg_jaffle_shop.yml`, do the following code:
```yaml
models:
  - name: stg_jaffle_shop__customers
    columns:
      - name: customer_id
        data_tests:
          - unique
          - not_null
  - name: stg_jaffle_shop__orders
    columns:
      - name: order_id
        data_tests:
          - unique
          - not_null
      - name: order_status
        data_tests:
          - accepted_values:
              values:
                - completed
                - shipped
                - returned
                - placed
                - return_pending
      - name: customer_id
        data_tests:
          - relationships:
              field: customer_id
              to: ref('stg_jaffle_shop__customers')
```
This means that you are testing the primary keys for both `customers` and `orders` to see if they are unique and existent.

For the column `order_status`, dbt will test if the columns only contain the values specified in the list.

For the column `customer_id` in the table `orders`, we are testing if the `customer_id` does exist on the `customers` table since it is its primary key.

3. To execute your data tests, run the command `dbt test`. To specifically execute a test, run the command `dbt test --select stg_jaffle_shop__orders`.
4. Commit and sync your changes.

## Singular Test

To write a singular test, your goal is to write a checking query that asserts that no row should be returned.

We want to create a custom test for `stg_stripe__payment` which is - the sum of the amounts should never be negative.

1. Under the `tests` folder, create an sql file named `assert_stg_stripe__payment_total_positive.sql`.
2. In `assert_stg_stripe__payment_total_positive.sql`, write the ff. lines:
```sql
-- Refunds have a negative amount, so the total amount should always be >= 0.
-- Therefore return records where this isn't true to make the test fail.
select
    order_id,
    sum(amount) as total_amount
from {{ ref('stg_stripe__payments') }}
group by 1
having total_amount < 0
```
3. Run `dbt test --select stg_stripe__payments`
4. Commit and sync your changes.

Executing the command `dbt test --select test_type:generic` will only run generic tests. On the other hand, `dbt test --select test_type:singular` will only run singular tests.

## Testing Sources
Putting assertions in sources is just the same as testing the models. You will put your data tests on your sources' yaml file.

The code looks like this:
```yaml
sources:
  - name: jaffle_shop
    database: raw
    schema: jaffle_shop
    tables:
      - name: customers
        columns:
          - name: id
            description: primary key
            data_tests:
              - unique
              - not_null        
      - name: orders
        config:
          freshness:
            warn_after:
              count: 12
              period: hour
            error_after:
              count: 1
              period: day
          loaded_at_field: _etl_loaded_at
```

To execute data tests on your source, run the command `dbt test --select source:<source name>` or `dbt test --select source:*` if you want all your sources to be trusted.
