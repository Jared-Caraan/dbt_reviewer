## Dealing with schema changes

Incremental models can be configured to include an optional `on_schema_change` parameter to enable additional control when incremental model columns change. These options enable dbt to continue running incremental models in the presence of schema changes, resulting in fewer `--full-refresh` scenarios and saving query costs.

The possible values for `on_schema_change` are:

- `ignore:` Default behavior.
- `fail:` Triggers an error message when the source and target schemas diverge
- `append_new_columns:` Append new columns to the existing table. Note that this setting does _not_ remove columns from the existing table that are not present in the new data.
- `sync_all_columns:` Adds any new columns to the existing table, and removes any columns that are now missing. Note that this is inclusive of data type changes. On BigQuery, changing column types requires a full table scan; be mindful of the trade-offs when implementing.

## Configuring CI jobs when your project has incremental models

Because your CI job is building modified models into a PR-specific schema, on the first execution of `dbt build --select state:modified+`, the modified incremental model will be built in its entirety _because it does not yet exist in the PR-specific schema_ and is_incremental will be false. You're running in full-refresh mode: This wastes time and compute.

You'll have two commands for your dbt Cloud CI check to execute:

1. Clone all of the pre-existing incremental models that have been modified or are downstream of another model that has been modified:

`dbt clone --select state:modified+,config.materialized:incremental,state:old`

2. Build all of the models that have been modified and their downstream dependencies:

`dbt build --select state:modified+`
Because of your first clone step, the incremental models selected in your dbt build on the second step will run in incremental mode.
