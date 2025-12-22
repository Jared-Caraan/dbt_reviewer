What are some benefits of using exposures?

a. Exposures expose data quality and organizational issues in your dbt Cloud project.\
b. Exposures optimize the performance of SQL queries by caching frequently used data.\
c. Exposures create custom SQL queries that automate the data transformation process.\
d. Exposures make it possible to define and describe downstream uses of your dbt project.

Answer: d

##
An exposure named exposure_name is configured for a certain dashboard. What's the quickest way to make sure the dashboard's data is up to date?

a. Run the exposure using the command "dbt run --select exposure_name".\
b. Run all models and metrics upstream of this exposure using the command " dbt run --select +exposure:exposure_name".\
c. Run the exposure using the command "dbt exposure:exposure_name".\
d. Run all models and metrics downstream of this exposure using the command " dbt run --select +exposure:*".

Answer: b

##
Which of the following needs to be done before viewing exposures in the dbt Catalog (formerly known as dbt Explorer)? Select all that apply.

a. You must have a Teams dbt Cloud plan.\
b. A production job needs to have been run.\
c. You must configure your metrics in a semantic model.\
d. Exposures must be configured in a yml file.

Answer: b,d
