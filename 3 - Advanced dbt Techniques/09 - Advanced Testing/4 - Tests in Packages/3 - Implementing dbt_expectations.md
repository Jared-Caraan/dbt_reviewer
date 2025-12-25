## Implementing dbt Expectations

First is to copy the code from the [dbt_expectations page](https://hub.getdbt.com/metaplane/dbt_expectations/latest/) into `packages.yml`.

<img width="655" height="231" alt="image" src="https://github.com/user-attachments/assets/d8b6024d-2d5e-450c-94ee-c537e1b21c80" />

### [expect_column_values_to_be_between](https://github.com/metaplane/dbt-expectations/tree/0.10.10/#expect_column_values_to_be_between)

<details>
<summary>Sample Usage</summary>
  
```yaml
  tests:
  - dbt_expectations.expect_column_values_to_be_between:
      min_value: 0  # (Optional)
      max_value: 10 # (Optional)
      row_condition: "id is not null" # (Optional)
      strictly: false # (Optional. Default is 'false'. Adds an 'or equal to' to the comparison operator for min/max)
```
</details>
