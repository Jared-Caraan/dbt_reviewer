## What to Test & Why

### Test on One Database Object

| What/Why | Example Tests |
| --- | --- |
| <ul><li>Assert something about the data that you think is true</li><li>Contents of the data</li><li>Constraints of the table</li><li>The grain of the table</li></ul> | <ul><li>`unique`</li><li>`not_null`</li><li>`accepted_values`</li><li>Imported package tests:<ul><li>`dbt_expectations.expect_column_proportion_of_unique_values_to_be_between`</li></ul></li></ul> |

### Test How One Object Refers to Another

| What/Why | Example Tests |
| --- | --- |
| <ul><li>Compare values in one model to a source of truth in another model</li><li>Ensure data has neither been erroneously added or removed</li></ul> | <ul><li>`relationships`</li><li>Imported package tests:<ul><li>`dbt_utils.equality`</li><li>`dbt_expectations.expect_table_row_count_to_equal_other_table`</li></ul></li></ul> |

### Test Something Unique About Your Data

| What/Why | Example Tests |
| --- | --- |
| <ul><li>Tests usually involve some business logic, edge case, or rare event</li></ul> | <ul><li>Orders should have `payments` >= 0</li><li>Billing total should equal the sum of all parts: `subtotal + tax + credits ... = Total`</li></ul> |

### Test the Freshness of Your Raw Source Data

| What/Why | Example Tests |
| --- | --- |
| <ul><li>See if you're loading tool has added raw data to your source table in the last X hours</li><li>Get notified if your underlying raw source data is not up to date.</li><li>Consider as the first step in your job to prevent models from running if data is delayed.</li></ul> | <ul><li>`Freshness` tests</li><li>run by `dbt source freshness` command</li></ul> |

### Temporary Testing While Refactoring

| What/Why | Example Tests |
| --- | --- |
| <ul><li>Create confidence</li><li>Efficiently refactoring</li><li>Auditing your changes while in development</li></ul> | <ul><li>`audit_helper` package to compare your new refactored model to your existing legacy model</li></ul> |

### Path to a well-tested dbt project

| | | |
| --- | --- | --- |
| **L1** | **Infancy** | No tests |
| **L2** | **Toddlerhood** | Primary key testing on your final models |
| **L3** | **Childhood** | Tests per model |
| **L4** | **Adolescence** | Add advanced tests from packages |
| **L5** | **Adulthood** | High test coverage; advanced testing strategies |
