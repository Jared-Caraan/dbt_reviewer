## Combined Logic

```jinja
{% set foods = ['radish', 'cucumber', 'chicken nugget', 'avocado'] %}

{%- for food in foods -%}

    {% if food == 'chicken nugget' %}
        {%- set food_type = 'snack' -%}
    {% else %}
        {%- set food_type = 'vegetable' -%}
    {% endif %}
    The delicious {{ food }} is my favorite {{ food_type }}

{% endfor %}
```

> [!TIP]
> The minus signs adjacent to the curly percent signs are used to manage whitespaces

## Dictionary
```jinja
{% set sample_dictionary = {
    'word': 'data',
    'part_of_speech': 'noun',
    'definition': 'the building block of life'
} %}

{{ sample_dictionary['word'] }}

{{ sample_dictionary['word'] }} ({{ sample_dictionary['part_of_speech'] }}): defined as "{{ sample_dictionary['definition'] }}"
```
