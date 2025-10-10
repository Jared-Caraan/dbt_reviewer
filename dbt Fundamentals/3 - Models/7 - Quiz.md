You are working in the dbt Studio. How do you ensure the model you have created is built in your data platform?

a. You must save the model\
b. You must use the `dbt run` command\
c. You must commit your changes to your branch\
d. You must create a sql file containing a select statement

Answer: b

##
What are two functions of a staging model in dbt?

a. Perform light transformations on your data set\
b. Connect to upstream sources using the source macro\
c. Connect to upstream models using the ref macro\
d. Perform aggregations that apply business logic

Answer: a, b

##
What are two functions of a marts model in dbt?

a. Reference upstream sources using the source macro\
b. Perform light transformations on the raw data set\
c. Apply business logic for stakeholders\
d. Reference upstream models using the ref macro

Answer: c, d

##
You just finished developing your first model that directly references and transforms customers source data. Where in your file tree should this model live?

a. models/stg_customers.sql\
b. models/staging/stg_customers.sql\
c. models/marts/stg_customers.sql\
d. models/sources/stg_customers.sql

Answer: b

##
You want all models in a folder to be materialized as tables.

Where can you accomplish this?

a. In the model itself\
b. in the dbt_project.yml file\
c. in the sources.yml file\
d. in the models.yml file

Answer: b

##
You have just built a `dim_customers.sql` model that relies on data from the upstream model stg_customers.

How would you reference this model in dim_customers?

a. select * from {{ ref('stg_customers.sql') }}\
b. select * from {{ ref('stg_customers') }}\
c. select * from {{ source(stg_customers.sql) }}\
d. select * from {{ source(stg_customers) }}

Answer: b

##
Which command will only materialize `dim_customers.sql` and its downstream models?

a. dbt run --select dim_customer\
b. dbt run --select dim_customers\
c. dbt run --select dim_customers+\
d. dbt run --select +dim_customer+

Answer: c

##
Which of the following is a benefit of using subdirectories in your models directory?

a. Subdirectories allow you to configure materializations at the folder level for a collection of models
b. Subdirectories allow you to include multiple dbt projects in a single project
c. Subdirectories allow you to explicitly build dependencies between models based on the naming of the folders
d. Subdirectories will automatically change the schema where a model is built based on the name of the folder the model is located in

Answer: a
