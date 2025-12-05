Where should macros be defined in a dbt project?

a. In the `models` folder.\
b. In the `analysis` folder.\
c. In the `macros` folder.\
d. In the `seeds` folder.

Answer: c

##
Consider the following macro definition:

```jinja

{% macro cents_to_dollars(column_name, decimal_places=2) %}

round({{ column_name }} / 100.0, {{ decimal_places }})

{% endmacro %}

```

How would you call this macro in a model to convert the `amount` column from cents to dollars with 4 decimal places? Select all answers that apply.

a. `{{ cents_to_dollars('amount', 4) }}`\
b. `{% cents_to_dollars('amount', 4) %}`\
c. `{% cents_to_dollars(amount, 4) %}`\
d. `{{ cents_to_dollars('amount', decimal_places=4) }}`

Answer: a,d

##
What is a potential drawback of using too many macros in a dbt project?

a. It can drastically slow down query performance.\
b. It can make the code difficult to maintain.\
c. It can lead to duplication of logic across models.\
d. It can cause SQL syntax errors during compilation.

Answer: b
