## Source Freshness

Source freshness is a health check for your data. It's a dbt powered test that tells you if your source data is up-to-date. You can specify what "fresh" means to you e.g. no more than 24 hrs old. Then dbt checks this, letting you know if the data is getting old.

You can add freshness check in your source YAML file. You can either add it on source level or model level.

To apply freshness check in `_src_jaffle_shop.yml`, do the following change to the code:
```yml
sources:
  - name: jaffle_shop
    database: raw
    schema: jaffle_shop
    tables:
      - name: customers
      - name: orders
        config:
          freshness:
            warn_after:
              count: 6
              period: hour
            error_after:
              count: 12
              period: hour
          loaded_at_field: _etl_loaded_at
```
The freshness configuration means that if the data is 6 hrs old, dbt will send a warning. But if the data is 12 hrs old, then dbt will throw an error. The freshness check above happens on model level.

To apply freshness check on a source level, do the following change to the code:
```yml
sources:
  - name: jaffle_shop
    database: raw
    schema: jaffle_shop
    freshness:
      warn_after:
        count: 6
        period: hour
      error_after:
        count: 12
        period: hour
    loaded_at_field: _etl_loaded_at
    tables:
      - name: customers
        freshness: null
      - name: orders
```
The `freshness: null` under customers is added because `_etl_loaded_at` column doesn't exist on the `customers` table. So, this tells dbt to skip the freshness check on `customers` table.

> [!TIP]
> To avoid typing everything on freshness configuration, you can type `__freshness`.

You can run `dbt source freshness` to check staleness of your data.

`warn_after:` - This is when dbt will issue a warning that the data is getting stale.
`error_after:` - This is when dbt will throw an error indicating that the data is critically outdated.\
`loaded_at_field:` - This is the column in your table the dbt will use to check the last load time. A common convention in a field is like `_etl_loaded_at`.
