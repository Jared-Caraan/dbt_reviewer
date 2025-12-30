## Model Versions - Syntaxes

<img width="1342" height="730" alt="image" src="https://github.com/user-attachments/assets/704f732d-3895-4af1-a137-c2e734e0e290" />

The version on the left is what we call diff only. It is the recommended option for most users. This option allows users to only specify the changes each time a new version is created.

The other option is what we call fully specified, where you need to specify all the configurations and properties for each version of the same model.

##

### Adding Model Versions
**Step 1:** Create file `<model>_v2.sql`. Add a **latest_version:** property to your models' contract. (Now we have two versions of `dim_customers.sql`: `dim_customers.sql` and `dim_customers_v2.sql`). 

latest_version will tell dbt which version of the model you're using when you reference dim_customers

```yaml
models:
    - name: dim_customers
      latest_version: 2
      columns:
          - name: customer_id
            data_type: number
```

**Step 2:** Add a **versions:** key to your model's yaml

This will allow us to list out old and current versions of the model.

```yaml
models:
    - name: dim_customers
      latest_version: 2
      columns:
          - name: customer_id
            data_type: number

      versions:
```

**Step 3:** Add a **-v:** property for each version under your **versions:** key

*Notice we have 2 listed - one for the new version 2, and one for the original version 1

```yaml
models:
    - name: dim_customers
      latest_version: 2
      columns:
          - name: customer_id
            data_type: number

      versions:
          - v: 1
          - v: 2
```

**Step 4:** Add a **columns:** property, where you will define the following:
- **include:**
    - Which columns from v1 are in v2 of my model
- **exclude:**
    - Which columns from v1 columns changed
- **old column configs**
    - What was the original config of the changed column

```yaml
models:
    - name: dim_customers
      latest_version: 2
      columns:
          - name: customer_id
            data_type: number

      versions:
          - v: 1
          - v: 2
            columns:
                - include: all
                  exclude: [number_of_orders]
                - name: number_of_orders
                  data_type: text
```

**Step 5:** Setting an alias

How are they materialized?
Where are they materialized?

- Each model version will actually create a database relation with alias <model_name>_v<v>.
- If you want a version of a model to have a different alias, you can specify in your model contract.

```yaml
models:
    - name: dim_customers
      latest_version: 2
      columns:
          - name: customer_id
            data_type: number

      versions:
          - v: 1
            config:
                alias: dim_customers
          - v: 2
            columns:
                - include: all
                  exclude: [number_of_orders]
                - name: number_of_orders
                  data_type: text
```

> [!WARNING]
> A common pattern is to let `v1` keep its versioned name (`orders_v1`) while aliasing only the `latest_version` to the clean name (`orders`) once it's ready for production.

##

### Ref-ing & running a model version
- **Ref a version:** `select * from {{ ref('dim_customers', v=2) }}`
    - If you don't identify a version in your ref, it will default to the latest version
- **Run a version:**
    - To run all versions: `dbt run -select dim_customers`
    - To run a specific versions: `dbt run -select dim_customers_v2`
    - To run a the latest versions: `dbt run -select dim_customers version:latest`

##

### Deprecation date

It is introduced to help data teams communicate when a specific model (or a version of a model) is no longer recommended for use and will eventually be removed.

```yaml
# models/schema.yml
models:
  - name: orders
    latest_version: 2
    versions:
      - v: 1
        # Users calling {{ ref('orders', version=1) }} will see a warning
        deprecation_date: 2024-12-31 
      - v: 2
```
