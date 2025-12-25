In this lesson we learned that:

- Model contracts guarantee the number of columns, their names and data types for a given table
- With model contracts you can:
    - Ensure the data types of your columns
    - Ensure a model will have a desired shape
    - Apply constraints to your model. (When applying constraints, your data platform will perform additional validations on data as it is being populated. Check our [docs](https://docs.getdbt.com/reference/resource-properties/constraints) to see which constraints your data platform supports.)

Model contracts are configured like so:

```yaml
models:
  - name: model_name
    config:
      contract:
        enforced: true
    columns:
      - name: column_name
        data_type: int
        constraints:
          - type: not_null
      - name: another_column_name
        data_type: string
      ...
```
