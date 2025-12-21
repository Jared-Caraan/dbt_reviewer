## Testing Commands

`dbt test` runs tests defined on models, sources, snapshots, and seeds. It expects that you have already created those resources through the appropriate commands.

The tests to run can be selected using the `--select` flag discussed in the [node select syntax docs](https://docs.getdbt.com/reference/node-selection/syntax).

### `dbt test`

<img width="658" height="641" alt="image" src="https://github.com/user-attachments/assets/8eefc5d3-d395-414f-9c92-fc6abbda15b4" />

So if we run dbt test, we see that all 25 of the tests in the project are run.

##
### `dbt test -s fct_orders`

<img width="666" height="493" alt="image" src="https://github.com/user-attachments/assets/ad884067-65a1-43fa-8802-2b5f18b45490" />

It will simply run the five tests associated with that model.

##
### `dbt test -s marts.*`

<img width="674" height="635" alt="image" src="https://github.com/user-attachments/assets/d0424e82-d6e9-4261-baee-3b68439ad031" />

It will run all of the tests within the `marts` directory.

##
### `dbt test -s test_type:data`

<img width="650" height="633" alt="image" src="https://github.com/user-attachments/assets/fde79f00-429e-46c5-8d1b-65e2420d9923" />

This command runs almost all data tests except the ones that don't hit the database level like - column existence validation, yaml structure validation, etc..

##
### `dbt test -s test_type:unit`

<img width="685" height="644" alt="image" src="https://github.com/user-attachments/assets/89afaef9-01b4-4f5d-bc98-31339757bc92" />

This command runs only dbt unit tests. **Unit tests** are a separate test type in dbt (introduced in dbt v1.6+), and they are not data tests.

**What are included in unit tests?**
- Are defined in `schema.yml`
- Use the `unit_tests:` block
- Test model logic, not warehouse data
- Run against fixtures, not real tables

<details>
<summary>Sample Unit Test</summary>

```yaml
unit_tests:
  - name: orders_calculations
    model: fct_orders
    given:
      - input: ref('stg_orders')
        rows:
          - order_id: 1
            amount: 10
    expect:
      rows:
        - order_id: 1
          total_amount: 10
```
</details>

##
### `dbt test -s source:jaffle_shop`

dbt will run tests defined on the specified source and its tables/columns

##
### `dbt test -s stg_jaffle_shop__customers --store-failures`

<img width="1063" height="619" alt="image" src="https://github.com/user-attachments/assets/a15fb455-1f9c-4b45-be2e-2fe7066ccddf" />

<img width="1532" height="721" alt="image" src="https://github.com/user-attachments/assets/a5d23b96-4223-4b36-bb1f-8a87c5300212" />

What this will do is materialize the results of the test into the data warehouse.

##
### Recommendations
| Good | Better | Best |
| --- | --- | --- |
| `dbt run` <br> `dbt test` | `dbt test -s source:*` <br> `dbt run` <br> `dbt test --exclude source:*`| `dbt build --fail-fast` |

**Good** - traditional run and test of all models \
**Better** - it's better to test all sources first, then run and test the models afterward \
**Best** - immediately cancels dbt run if a failure occurred unlike `dbt build` that will continue to run other unrelated models.

**Resources**
- [dbt node selection syntax](https://docs.getdbt.com/reference/node-selection/syntax)
- [dbt node selector methods](https://docs.getdbt.com/reference/node-selection/methods)
