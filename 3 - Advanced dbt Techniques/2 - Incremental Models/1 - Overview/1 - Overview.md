## Incremental Models

Incremental models in dbt are a materialization strategy designed to efficiently update your data warehouse tables by only transforming and loading new or changed data since your last run.

Instead of processing your entire data set every single time, incremental models update only these new rows, significantly reducing the time and resources required for your data transformations.