## Model Contracts

**Thought Experiment**

You have a rather large dbt Cloud project (1000+ models). There are several teams working inside of this project, referencing models built by one another, and becoming dependent on the data.
- What happens when someone, say, changes the datatype of a column in an upstream model? Or removes a column from an upstream model that you were selecting from?

##

### Model Contracts Defined
- Allow you to _guarantee_ the shape of your model
    - The column names that exist in the model
    - The data type of each column
- If the model doesn't have those exact columns with those exact data types, you'll get an error message when you try to do a dbt run.

##

### Creating Model Contracts
- To create a **Model Contract**, add a `contract:` configuration to the model yaml
- List each expected column, along with its data type
- Add a constraints property to create an even stricter contract*

    <details>
    <summary>Sample YAML</summary>
    
    ```yaml
    models:
      - name: best_trilogy
        group: Legions_of_the_Southlands
        config:
            contract:
                enforced: true
        columns:
            - name: number_in_trilogy
              data_type: float
              constraints:
                  - type: not_null
            - name: film_name
              data_type: string
        ...
    ```
    </details>

##

### Isn't this sort of like testing?
- **Model contracts** check up on the _shape of a dataset_, while **tests** check up on the _content of a data set_.
- **Tests are a more flexible way to validate the content of a model**
    - As long as you can write the query, you can run the test.
    - Tests are also more configurable in terms of severity, and custom thresholds are easier to debug after finding failures.
    - But:
        - constraints are a pre-flight check; if a particular constraint is enforced by your platform, the "bad data" won't even be able to get into your model
        - dbt data tests are post-hoc checks; bad data can get into your model and the tests lets you know about it

## Related Resources
- [model contracts](https://docs.getdbt.com/docs/collaborate/govern/model-contracts)
- [constraints](https://docs.getdbt.com/reference/resource-properties/constraints)
