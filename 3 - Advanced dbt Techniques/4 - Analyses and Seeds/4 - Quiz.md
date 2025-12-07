What is the primary purpose of an analysis in dbt?

a. To transform raw data into a final model for production.\
b. To run one-off queries or audit data without affecting production models.\
c. To automatically test the integrity of data models.\
d. To serve as a staging area for building models.

Answer: b

##
How are seeds different from models in dbt?

a. Seeds are stored as SQL files, while models are stored as YAML files.\
b. Seeds are built into the data warehouse using the `dbt run` command.\
c. Seeds are CSV files materialized into tables using the `dbt seed` command, while models are SQL queries that transform data.\
d. Seeds are used for frequently changing data, while models are for static data.

Answer: c

##
Which of the following is an ideal use case for a seed in dbt?

a. Loading large datasets that change frequently.\
b. Storing country codes or static lookup tables.\
c. Performing data transformations using Jinja.\
d. Creating automated tests for models.

Answer: b

##
What command can you use to compile an analysis in dbt and check the SQL it generates?

a. `dbt run`\
b. `dbt test`\
c. `dbt seed`\
d. `dbt compile`

Answer: d
