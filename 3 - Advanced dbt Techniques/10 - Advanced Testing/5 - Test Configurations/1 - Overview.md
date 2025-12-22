## What are Test Configurations?

**fct_orders.yml**

```yaml
models:
  - name: fct_orders
    columns:
      - name: order_id
        data_tests:
          - unique
          - not_null
```

Here we have a not null test on the order ID of fact orders. If there is a single null order id, the test will fail. Depending on your context, you might want that test to contain some logic to return a warning instead of a failure. 

A warning will simply raise a flag that says - "hey, you wanted me to let you know about this.". But it won't mark the test command overall as failed and further steps will continue to run, test, or build. To do this, we add a config with severity set to warn under our not null test.

<details>
<summary>Modified yaml file</summary>

```yaml
models:
  - name: fct_orders
    columns:
      - name: order_id
        data_tests:
          - unique
          - not_null:
              config:
                severity: warn
```
</details>

Or perhaps you have a tolerance for some nulls in a specified column, but only up to 100. You can declare that as well without having to rewrite the test.

<details>
<summary>Modified yaml file</summary>

```yaml
models:
  - name: fct_orders
    columns:
      - name: order_id
        data_tests:
          - unique
          - not_null:
              config:
                severity: warn
                error_if: ">=100"
```
</details>

##
### Test Configurations
- severity and threshold
- where - can be used to apply a filter to the data that you're scanning with a test.
- limit - allows you to limit the number of records that are returned by a test. If you're working with large data, this is really helpful to reduce the unnecessary processing of records if you already know there's a failure within the first tests.
- store failures - enable the storage of failing records in your data platform.

##
### Where to Configure Tests?
- yml files where you configure generic tests
- config blocks for singular tests
- Generic test definitions in your macros or `tests/generic` folder
- `dbt_project.yml` for project/package level
