## Analyses

- SQL files in the `analyses` folder
- supports Jinja
- can be compiled with `dbt compile`
- one off queries
- training queries
- auditing/refactoring
- they're not models and they're not tests

> [!NOTE]
> No relation will be materialized in the database as this is an analysis, not a model.

## Seeds

- csv files in the `data` folder
- build a table from a small amount of data in a csv file
- build these tables with `dbt seed`
- reference a seed in your model through the `ref` function
- could be used as a lookup table for:
  - country codes
  - employee id/emails

> [!NOTE]
> Seeds are not designed for large and frequently changing data

**Resources**
- [Analyses](https://docs.getdbt.com/docs/build/analyses#overview)
