## Python Models

### What's a python model?
- Reads in dbt sources / models
- Applies transformations
- Returns transformed dataset

##

### Why include Python Models?
- Great supplement (not a replacement) to .sql models
- Perform analysis using tools from open-source Python ecosystem
- Single infrastructure and orchestration to run Python transformations

##

### Python model syntax

```python
import ...

def model( dbt, session ):

    my_sql_model_df = dbt.ref("my_sql_model")

    final_df = ... # stuff you can't write in SQL!

    return final_df
```

##

You can specify configs with the model via:

```python
dbt.config(
    materialized = "table",
    packages = ['pandas', 'holidays']
)
```

You can also configure materializations for Python models in your `dbt_project.yml` file. Or, of course, in a dedicated YAML file within the model's directory.

Table is going to be the default materialization for each Python model.

You can also import packages in two places - inside the config block, or at the very top outside the python function.
