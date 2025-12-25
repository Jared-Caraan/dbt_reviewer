## Store Failures Config for Tests

Instead of passing `--store-failures` every time we run dbt on the command line, we want to automatically store failures, we can add this configuration into our tests.

So if this was the case, we could add the store_failures configuration in our yaml file.

```yaml
  - name: amount
    columns:
      - name: order_id
        data_tests:
          - dbt_utils.expression_is_true:
              expression: "<= 5"
              config:
                limit: 5
                store_failures: true
```

Now we can rerun without passing the CLI flag. And if we expand, it will show us that it has been materialized into our data warehouse.

<img width="890" height="337" alt="image" src="https://github.com/user-attachments/assets/1712c2fb-7000-434b-969d-02e610dc50aa" />

##

Let's say our team has decided that we should store failures for every test we run. If that's the case, we can remove the configuration from the model yaml file and navigate to our `dbt_project.yml`.

```yaml
tests:
  jaffle_shop:
    +store_failures: true
```
