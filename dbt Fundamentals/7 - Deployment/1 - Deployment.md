## Deployment

Deploying dbt involves running dbt commands on a schedule. This will allow dbt to build models on whatever cadence you need them to. You can run dbt nightly or on the weekends without needing to log into the dbt site.

When we deploy dbt, all of our models will be built into a production schema. This is a schema that we can then point a BI tool at. This production schema can then be referenced as the single source of truth.

When we deploy dbt, dbt will use the main branch for building models. That's why all of the work we've done so far has been in a different branch, our development branch.
