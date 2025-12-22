## Limit Config for Tests

```yaml
  - name: amount
    columns:
      - name: order_id
        data_tests:
          - dbt_utils.expression_is_true:
              expression: "<= 5"
              config:
                limit: 5
```

This configuration is typically used on very large tables. This ensures that your query executes much more efficiently so that you're not wasting compute once you have a failed record.

<img width="731" height="541" alt="image" src="https://github.com/user-attachments/assets/3db6ee76-bc4c-409b-8ac2-a50b55db2415" />
