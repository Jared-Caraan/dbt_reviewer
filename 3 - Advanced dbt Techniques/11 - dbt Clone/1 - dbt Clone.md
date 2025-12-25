## dbt Clone
- Create a copy of a database object without copying the underlying data
- Quick, lightweight copies of datasets for testing, development, or experimentation without duplicating data storage or incurring additional costs
- By default, dbt clone will not recreate pre-existing relations in the current target

##

### Requirements
- Successful job run in your production environment
- Enable Defer to production
- Invoke `dbt clone` from the command bar

##

### Use Cases
- blue/green continuous deployment (on data warehouses that support zero-copy cloning tables - Snowflake, Databricks, or BigQuery)
- cloning current production state into development schema(s)
- handling incremental models in dbt Cloud CI jobs
- testing code changes on downstream dependencies in your BI tool
