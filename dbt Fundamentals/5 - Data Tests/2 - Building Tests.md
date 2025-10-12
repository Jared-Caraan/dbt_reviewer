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

## Singular Test
