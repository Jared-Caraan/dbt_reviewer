There are three packages that are must-haves for any dbt project: [dbt_utils](https://hub.getdbt.com/dbt-labs/dbt_utils/latest/), [dbt_expectations](https://hub.getdbt.com/calogica/dbt_expectations/latest/), and [audit_helper](https://hub.getdbt.com/dbt-labs/audit_helper/latest/). Here are the steps to use any package:

1. Import the package that you want in your packages.yml file
2. Run `dbt deps`
3. Add the name of the package and the name of the test to your .yml file

## `dbt_utils`

dbt_utils is a one-stop-shop for several key functions and tests that you’ll use every day in your project.

Here are some useful tests in [dbt_utils](https://hub.getdbt.com/dbt-labs/dbt_utils/latest/):

- expression_is_true
- cardinality_equality
- unique_where
- not_null_where
- not_null_proportion
- unique_combination_of_columns

## `dbt_expectations`

dbt_expectations contains a large number of tests that you may not find native to dbt or dbt_utils. If you are familiar with Python’s great_expectations, this package might be for you!

Here are some useful tests in [dbt_expectations](https://hub.getdbt.com/calogica/dbt_expectations/latest/):

- expect_column_values_to_be_between
- expect_row_values_to_have_data_for_every_n_datepart
- expect_column_values_to_be_within_n_moving_stdevs
- expect_column_median_to_be_between
- expect_column_values_to_match_regex_list
- expect_column_values_to_be_increasing

## `audit_helper`

This package is utilized when you are making significant changes to your models, and you want to be sure the updates do not change the resulting data. The audit helper functions will only be run in the IDE, rather than a test performed in deployment.

Here are some useful tools in [audit_helper](https://hub.getdbt.com/dbt-labs/audit_helper/latest/):

- compare_relations
- compare_queries
- compare_column_values
- compare_relation_columns
- compare_all_columns
- compare_column_values_verbose

## Related Resources
- [Package Hub](https://learn.getdbt.com/learn/course/advanced-testing/tests-in-packages-45-min/tests-in-packages?page=11#:~:text=Package%20Hub,audit_helper)
- [dbt_utils](https://learn.getdbt.com/learn/course/advanced-testing/tests-in-packages-45-min/tests-in-packages?page=11#:~:text=Package%20Hub,audit_helper)
- [dbt_expectations](https://learn.getdbt.com/learn/course/advanced-testing/tests-in-packages-45-min/tests-in-packages?page=11#:~:text=Package%20Hub,audit_helper)
- [audit_helper](https://learn.getdbt.com/learn/course/advanced-testing/tests-in-packages-45-min/tests-in-packages?page=11#:~:text=Package%20Hub,audit_helper)
