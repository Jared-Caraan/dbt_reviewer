## Definition

- Python-based templating language
- brings functional aspects to SQL
- e.g. `{{ ref('stg_orders') }}`
- enables better collaboration
- write SQL faster with less lines of code
- sets foundation for macros

## Syntax
`{% %}` - This indicates some sort of operation is happening inside of the Jinja context. It will be invisible to the end user after the code is compiled into whatever you are outputting.

`{{ }}` - This indicates that we are pulling something out of the Jinja context and actually printing it into the file that we're interacting with in order to produce some sort of written material.

## Setting a Variable
```jinja
{% set temperature = 80.0 %}
```

## If Statements
```jinja
{% set temperature = 80.0 %}

 On a day like this, I especially like
{% if temperature > 70 %}
a refreshing lemon sorbet

{% else %}
a decadent chocolate cake
    
{% endif %}
```
The example if statement above has a compiled code of:

<img width="464" height="176" alt="image" src="https://github.com/user-attachments/assets/562a343e-76f7-4aef-8825-faa92684a316" />

> [!TIP]
> A shortcut to create if-condition blocks is to type two underscores (__) followed by the *if* keyword

## For-loop statements
```jinja
{% for j in range(26) %}
    select {{ j }} as number {% if not loop.last %} union all {% endif %}
{% endfor %}
```
The jinja above is compiled into the ff. SQL query:
<details>
<summary>SQL Query Result</summary>
  
```sql
select 0 as number  union all 

  select 1 as number  union all 

  select 2 as number  union all 

  select 3 as number  union all 

  select 4 as number  union all 

  select 5 as number  union all 

  select 6 as number  union all 

  select 7 as number  union all 

  select 8 as number  union all 

  select 9 as number  union all 

  select 10 as number  union all 

  select 11 as number  union all 

  select 12 as number  union all 

  select 13 as number  union all 

  select 14 as number  union all 

  select 15 as number  union all 

  select 16 as number  union all 

  select 17 as number  union all 

  select 18 as number  union all 

  select 19 as number  union all 

  select 20 as number  union all 

  select 21 as number  union all 

  select 22 as number  union all 

  select 23 as number  union all 

  select 24 as number  union all 

  select 25 as number
```
</details>

> [!TIP]
> A shortcut to create for-loops is to type two underscores (__) followed by the *for* keyword

## More Variables
Example:
```jinja
{% set cool_string = 'Wow cool beans!' %}

{{ cool_string }}
```
```jinja
{% set cool_string = 'Wow cool beans!' %}
{% set my_second_cool_string = 'This is jinja!' %}
{% set my_fave_num = 26 %}

{{ cool_string }} {{ my_second_cool_string }} I want to write jinja for {{ my_fave_num }} years!
```
```jinja
{% set animals = ['lemur', 'dingo', 'rhino', 'dog'] %}

{{ animals[0] }}
{{ animals[1] }}
{{ animals[2] }}
{{ animals[3] }}
```
```jinja
{% for animal in animals %}
    my favorite animal is the {{ animal }}
{% endfor %}
```
> [!TIP]
> A shortcut to set variables is to type two underscores (__) followed by the *set* keyword
## Comments
`{# #}` - Anything between this hashtags would not compile
