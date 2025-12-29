Which is not a feature of data testing in dbt?

a. Identify errors in my data pipelines when they occur.\
b. Create trust in the data products we share with stakeholders.\
c. Determine if the sql we wrote has done what we intended.\
d. Enable stakeholders to self-serve and understand how a model was built

Answer: d

##
Consider the YAML configuration below. Assume this is the only YAML file in the models directory.
```yaml
sources:
  - name: salesforce
    tables:
      - name: accounts
        columns:
          - name: account_id
            data_tests:
              - unique
```
What data tests will be run in your project?

a. A unique test will be run on the accounts source table.\
b. A unique test will be run on the salesforce source table.\
c. A unique test will be run on the salesforce model\
d. A unique test will be run on the accounts model

Answer: a

##
When a data test is run, what is happening under the hood in dbt?

a. dbt will compile python to run against models or sources\
b. dbt will compile SQL to run against models or sources\
c. dbt will enforce a constraint on the column of the models or sources\
d. dbt will scan the SQL of your data models to ensure the data materializes correctly

Answer: b

##
On Monday, you are working in development and run dbt build. Your entire project materializes and tests successfully. You have only accepted values tests on your sources and models.

On Tuesday, you log back in and run dbt run and your models all run. You then run dbt test and find that 5 tests failed.

What is most likely the reason for the tests failing?

a. The SQL in your models resulted in a compilation error.\
b. The column name in one of your sources that changed.\
c. A new value was introduced on a column you were testing.\
d. A column you were testing now has a duplicate.

Answer: c

##
Consider the YAML block below
```yaml
sources:
  - name: salesforce
    tables:
      - name: accounts
        loaded_at_field: _updated_at
        freshness:
          warn_after: {count: 1, period: day}
          error_after: {count: 7, period: day}
        columns:
          - name: account_id
             tests:
               - unique
               - not_null
```
When running `dbt source freshness` what will cause a warning to be flagged?

a. A duplicate in the account_id column will cause a warning.\
b. A null value in the account_id column will cause a warning.\
c. The greatest value of the _updated_at column is more than 7 days before the current time\
d. The greatest value of the _updated_at column is between 1 and 7 days before the current time.

Answer: d

##
What is the dbt best practice for testing your primary keys?

a. Apply a unique test to your primary keys.\
b. Apply a not_null test to your primary keys.\
c. Apply a unique and not_null test to your primary keys.\
d. Apply a relationships test to your primary keys to ensure referential integrity to a foreign key.

Answer: c

##
Assume your project only has models and sources and data tests configured on models and sources. (i.e. there are not snapshots or seeds -- these are beyond the scope of this quiz)

How does the dbt build command work?

a. dbt build will first test your sources, then materialize all your models, and then test all your models.\
b. dbt build will first test your sources, then materialize and test each model in DAG order.\
c. dbt build will first materialize your models, then test your sources, and then test your models.

Answer: b

##
Which command will run data tests only on sources?

a. dbt test --select source:*\
b. dbt test --select _sources.yml\
c. dbt test --select staging/\
d. dbt source test

Answer: a
