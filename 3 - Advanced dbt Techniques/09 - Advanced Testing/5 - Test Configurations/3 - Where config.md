## Where Config for Tests

Another test configuration in dbt is the `where` config.

```yaml
  - name: amount
    columns:
      - name: order_id
        data_tests:
          - dbt_utils.expression_is_true:
              expression: "<= 5"
              config:
                where: "ordered_at = current_date"
```

The config above dictates that we will only fail this test for amounts greater than 5 for today's orders.

Under the hood, this is what the test looks like:

<img width="1028" height="319" alt="image" src="https://github.com/user-attachments/assets/e3656e43-9622-4e38-bc7f-0576084efbfa" />

> [!NOTE]
> This can also be applied to singular tests
