## Promoting a Singular Test to a Generic Test

Convert this singular test:

```sql
# tests the assertion that the order "amount" is always greater than 5

select
  amount
from {{ ref( 'fct_orders' ) }}
where amount <= 5
```

Into a Generic Test:
```sql
{% test greater_than_five(model, column_name) %}

  select
    {{ column_name }}
  from {{ model }}
  where {{ column_name }} <= 5

{% endtest %}
```

Adding the Generic Test into a yaml file
```yaml
...
- name: amount
  description: rounded dollar amount of order
  data_tests:
    - greater_than_five
...
```
