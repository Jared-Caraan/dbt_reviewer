## Promoting a Singular Test to a Generic Test


{% test greater_than_five(model, column_name) %}

  select *
  from {{ model }}
  where {{ column_name }} is null

{% endtest %}
