## Overwriting Native Tests

You can **overwrite any test that dbt ships** with. In fact, you can overwrite any macro that dbt utilizes!

**Why would you do this?**

You may want to test for not-null-ness only under certain circusmtances across your entire project, like when the `column_id` is not your test case, i.e., not equal to `00000`.

### Overwriting Native Tests Example

```sql
# this is the not_null test

{% test not_null(model, column_name) %}

  select *
  from {{ model }}
  where {{ column_name }} is null

{% endtest %}
```

```sql
# this is the not_null test, with a mod!

{% test not_null(model, column_name, column_id) %}

  select *
  from {{ model }}
  where {{ column_name }} is null
    and {{ column_id }} is not in ( '00000' )

{% endtest %}
```
