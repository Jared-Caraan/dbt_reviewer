## Implementing dbt_utils

First is to copy the code from the [dbt_utils page](https://hub.getdbt.com/dbt-labs/dbt_utils/latest/) into `packages.yml`.

<img width="658" height="313" alt="image" src="https://github.com/user-attachments/assets/85ffc56f-6659-4c60-af98-ee5260470766" />

### [expression_is_true](https://github.com/dbt-labs/dbt-utils/tree/1.3.3/#expression_is_true-source)

<details>
<summary>Sample Usage</summary>

```yaml
version: 2

models:
  - name: model_name
    tests:
      - dbt_utils.expression_is_true:
          arguments:
            expression: "col_a + col_b = total"
```
</details>

To utilize this generic test in the previous use case of asserting whether the order amount is greater the 5 dollars:

```yaml
version: 2

models:
  - name: model_name
    tests:
      - dbt_utils.expression_is_true:
          arguments:
            expression: "<=5"
```

### [cardinality_equality](https://github.com/dbt-labs/dbt-utils/tree/1.3.3/#cardinality_equality-source)

This generic test is used to assert that a number of elements in a column is similar to the number of elements in another column on another model

<details>
<summary>Sample Usage</summary>

```yaml
version: 2

models:
  - name: model_name
    columns:
      - name: from_column
        tests:
          - dbt_utils.cardinality_equality:
              arguments:
                field: other_column_name
                to: ref('other_model_name')
```
</details>
