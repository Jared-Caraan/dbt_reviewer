## Data Testing

Data Testing is your quality control team and your detective toolkit. It allows you to build a series of automated checks into your dbt project to verify your data is exactly what you expect it to be every single time.

dbt offers two types of tests, generic tests and singular tests.

**Generic Tests** - These are reusable tests built into dbt that you can apply to the columns and models. Think of checks like ensuring a column has unique values or is not null. They are defined in a YAML file and can be applied to many different models and columns. Think of them like a library of pre-built quality checks.

dbt comes in with 4 built-in generic tests that are incredibly useful.
1. `unique` - This test ensures that every value in a column is unique.
2. `not_null` - This ensures a column contains no null values.
3. `accepted_values` - This checks that a column's values are of one of the specified list of values.
4. `relationships` - This validates that all values in one column have a corresponding value in a parent table's primary key column ensuring referential data integrity.

**Singular Tests** - These are custom tests that you can write using a SQL query in a separate SQL file stored in your `tests` folder. They're perfect for more complex business rules, like ensuring a customer's total order value is always greater than zero. They are for specific one-off assertions.

Using these tests, you can make sure that your data is telling the truth.

When you run `dbt test` dbt checks all the tests in your project against the latest version of your models.

You can check [dbt hub](https://hub.getdbt.com/) for lists of singular tests that have already been written, specifically the `dbt_utils` package.
