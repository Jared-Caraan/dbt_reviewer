## Severity Config for Tests

Before test configuration, the run failed for the column `amount`.

<img width="1024" height="652" alt="image" src="https://github.com/user-attachments/assets/ea9229ec-cf83-441f-a1ec-1aeebb32e3b6" />

Let's try adding some severity configuration to the yaml file:

```yaml
  - name: amount
    columns:
      - name: order_id
        data_tests:
          - dbt_utils.expression_is_true:
              expression: "<= 5"
              config:
                severity: warn
```

After you run your dbt test, the result now looks like this:

<img width="1058" height="586" alt="image" src="https://github.com/user-attachments/assets/b656f3df-05bc-4f97-aa6c-981884e17ed4" />

##

Let's say we want to produce an error if the defective rows go up to a hundred. We can modify the yaml file like this:

```yaml
  - name: amount
    columns:
      - name: order_id
        data_tests:
          - dbt_utils.expression_is_true:
              expression: "<= 5"
              config:
                error_if: ">=100"
```

Once again, the test failed because the number of defective rows passed the threshold of 100.

<img width="860" height="316" alt="image" src="https://github.com/user-attachments/assets/d4c7921a-f609-474d-a249-7c4f69e13ba1" />

##

If we tried to increase the threshold:

```yaml
  - name: amount
    columns:
      - name: order_id
        data_tests:
          - dbt_utils.expression_is_true:
              expression: "<= 5"
              config:
                error_if: ">=60000"
```

We will only receive a warning on the test column.

<img width="878" height="312" alt="image" src="https://github.com/user-attachments/assets/40762ee3-4388-438a-8ecf-85cbb23cfe86" />

##

We can also apply severity configurations to singular tests.

**assert_amount_is_greater_than_five.sql**
```sql
{{
    config(
        severity="warn"
    )
}}

select
  amount
from {{ ref( 'fct_orders' ) }}
where amount <= 5
```

And it will give us a warn as a result.

<img width="831" height="616" alt="image" src="https://github.com/user-attachments/assets/8c25c47f-fc2c-45e9-882c-32353d2e2f22" />
