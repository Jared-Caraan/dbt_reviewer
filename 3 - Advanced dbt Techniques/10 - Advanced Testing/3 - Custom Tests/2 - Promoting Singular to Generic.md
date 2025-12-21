## Promoting a Singular Test to a Generic Test

```sql
{% test greater_than_five(model, column_name) %}

  select
    {{ column_name }}
  from {{ model }}
  where {{ column_name }} <= 5

{% endtest %}
```
