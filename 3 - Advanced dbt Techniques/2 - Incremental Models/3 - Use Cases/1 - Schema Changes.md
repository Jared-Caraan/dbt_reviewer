## Dealing with Schema Changes

What if we want to have additional control over our incremental models when columns change?

You can deal with it in two ways - via `dbt-project.yml` and via model-level configurations.

**dbt-project.yml**

```yaml
models:
  +on_schema_change: "sync_all_columns"
```

**Model-level configuration**
