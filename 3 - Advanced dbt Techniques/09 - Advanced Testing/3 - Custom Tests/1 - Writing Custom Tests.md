## Types of Custom Tests

**Custom tests** are assertions written in SQL that do not fall under the scope of the native dbt tests.
**Singular tests** are select statements with specific references to a model and relevant columns.
**Generic tests** are select statements that utilize input parameters as variables in order to apply to many models.

## Singular Tests

Singular tests are built when you want to test an assumption about one particular model. The test should return any rows that fail the assumption. All you need is a SELECT statement in a new .sql file stored in the `/data-test/` folder.

<details>
<summary>Sample Singular Test</summary>

```sql
# tests the assertion that the order "amount" is always greater than 5

select
  amount
from {{ ref( 'fct_orders' ) }}
where amount <= 5
```
</details>

## Custom Generic Tests

Custom generic tests are built when you want to **test the same assumption on multiple models**.

We can build a macro-like test, with input parameters, and apply it to any relevant models.

You need a Jinja test tag, test name, parameters, and your SELECT statement in a new .sql file stored in the `/data-test/generic` folder.

**Generic Tests a.k.a dbt tests!**

What are other examples of generic tests? They are native to dbt and you can apply them to any model:
- unique
- not_null
- accepted_values
- relationship

<details>
<summary>Native not_null test</summary>

```sql
# this is the not_null test, under the hood!

{% test not_null(model, column_name) %}

  select *
  from {{ model }}
  where {{ column_name }} is null

{% endtest %}
```
</details>
