What is the primary advantage of using the `dbt build` command over separate `dbt run` and `dbt test` commands?

a. It allows for faster deployment without any testing.\
b. It materializes and tests nodes in dependency order, skipping downstream dependencies if a test fails.\
c. It automatically skips nodes that do not contain any new code changes.\
d. It prevents jobs from running in parallel, reducing the risk of overloading the system

Answer: b

##
When would you typically choose to run a full refresh job in dbt Cloud?

a. When a critical bug is identified in the DAG structure.\
b. When you need the most up-to-date information across all models and can tolerate rebuilding large tables.\
c. Every time new code is deployed to production, regardless of data updates.\
d. When you need to minimize the number of incremental updates processed in production.

Answer: b

##
Which situation is best handled by using a time-sensitive job in dbt Cloud?

a. You need to ensure that data for a specific dashboard is updated every hour.\
b. You need to perform a one-time refresh of all data in production.\
c. Your team is working on testing new models and you need to update them regularly in a staging environment.\
d. You are deploying a full DAG to capture all changes made during development.

Answer: a

##
What is the benefit of using the union model selector syntax in dbt Cloud?

a. It merges multiple jobs into one for faster execution.
b. It ensures that jobs run independently of each other, reducing risks of errors.
c. It allows you to select and run all parent nodes of multiple models in one command.
d. It ensures that only one model is run at a time, reducing compute strain.
