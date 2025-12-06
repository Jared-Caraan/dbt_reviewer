Why might a full-refresh of incremental models during a slim CI job be problematic?

a. It introduces schema drift in the production environment.\
b. Incremental models can fail CI jobs due to missing dependencies.\
c. Full-refresh builds for large incremental models are slow and expensive.\
d. Full-refresh builds cause all downstream models to skip execution.

Answer: c

##
Which of the following is NOT a possible value for the on_schema_change key?

a. fail\
b. ignore\
c. sync_all_columns\
d. warn

Answer: d

##
How can you avoid full-refresh builds for incremental models in a slim CI job?

a. Use the dbt build command without the state:modified selector.\
b. Clone pre-existing incremental models into the PR-specific schema using the dbt clone command.\
c. Modify the incremental model configurations to disable full-refresh builds.\
d. Set the is_incremental flag to false for all modified models.

Answer: b

##
Why might someone set the on_schema_change config to 'fail' in an incremental model?

a. To prevent incremental models from being rebuilt during CI jobs.\
b. To ensure schema changes are explicitly addressed before the incremental model is rebuilt.\
c. To disable schema validation checks for faster performance.\
d. To allow schema changes to propagate automatically to downstream models.

Answer: b
