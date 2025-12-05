## Writing Documentation

The code below covers documentation for our `_stg__jaffle_shop.yml`.

```yaml
models:
  - name: stg_jaffle_shop__customers
    description: one unique customer per row
    columns:
      - name: customer_id
        description: the primary key
        data_tests:
          - unique
          - not_null

  - name: stg_jaffle_shop__orders
    columns:
      - name: order_id
        data_tests:
          - unique
          - not_null
      - name: status
        description: "{{ doc('order_status') }}"
        data_tests:
          - accepted_values:
              arguments:
                values: ['placed', 'shipped', 'completed', 'returned', 'return_pending']
      - name: customer_id
        data_tests:
          - relationships:
              arguments:
                to: ref('stg_jaffle_shop__customers')
                field: customer_id
```
In line 23, a doc block is created. This is for documentation that consists of multiple explanations. A doc block can be defined by a markdown file.

Under `staging/jaffle_shop`, create a new file called `jaffle_shop_docs.md`. Then write the code below. This markdown file is what's being referenced by the line 23 above.

```markdown
{% docs order_status %}
    
One of the following values: 

| status         | definition                                       |
|----------------|--------------------------------------------------|
| placed         | Order placed, not yet shipped                    |
| shipped        | Order has been shipped, not yet been delivered   |
| completed      | Order has been received by customers             |
| return pending | Customer indicated they want to return this item |
| returned       | Item has been returned                           |

{% enddocs %}
```

> [!TIP]
> You can click on **Markdown Preview** in dbt Studio to see if your markdown file turned out okay.

## Documenting Sources

The code below is an example of documenting sources

```yaml
sources:
  - name: jaffle_shop
    description: A clone of a Postgres database
    database: raw
    schema: jaffle_shop
    tables:
      - name: customers
        description: Raw customers data
        columns:
          - name: id
            description: primary key
            data_tests:
              - unique
              - not_null        
      - name: orders
        description: Raw orders data
        columns:
          - name: id
            description: primary key
            data_tests:
              - unique
              - not_null  
        config:
          freshness:
            warn_after:
              count: 12
              period: hour
            error_after:
              count: 1
              period: day
          loaded_at_field: _etl_loaded_at
```

> [!TIP]
> Adding "raw" on the source table documentation is best practice so that it signifies that the data is original and untransformed.

## Using dbt Copilot to Generate Documentation

We can also use dbt Copilot to give us a head start. It's great for generating initial documentation, but remember you are the data expert, so you should review and refine its work.

1. Start by making sure your dbt Copilot is enabled in your settings.
2. Click on one of the models (not YAML files).
3. Click on dbt Copilot -> Documentation
4. If the YAML file already exists, it's going to find that and update it. Otherwise, it will create a new one.
