## In the past

`dbt run` + `dbt test`
- materialize all models first
- then test models
- doesn't include snapshots and seeds
- multiple commands to test sources vs. models

**Risk**
If a test failed, the models have already been materialized.

## dbt build

- run and test all nodes in DAG order
- also includes snapshots and seeds
- skip nodes downstream of a test failure
- supports all command line flags you would expect
