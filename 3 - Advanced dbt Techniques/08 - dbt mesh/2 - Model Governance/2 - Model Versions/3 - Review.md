In this lesson we learned that:
- Model versions allow you to make breaking changes to a model without actually breaking downstream models.
- Model versions at large organizations are a great way to:
    - Test "prerelease" changes (in production, in downstream systems)
    - Bump the latest version, to be used as the canonical source of truth
    - Offer a migration window off the "old" version

Model versions are configured in yaml files like so:

```yaml
models:
  - name: file_name
    latest_version: 2 #you can specify any version as the latest version
    columns:
      - name: column_name
        data_type: its_data_type
     - name: a_different_column_name
         data_type: that_columns_data_type
    versions:
      - v: 2
      - v: 1
        defined_in: file_name_v1
        config:
          alias: file_name
        columns:
          - include: *
            exclude: a_different_column_name
          - name: a_different_column_name
            data_type: that_columns_data_type
```
