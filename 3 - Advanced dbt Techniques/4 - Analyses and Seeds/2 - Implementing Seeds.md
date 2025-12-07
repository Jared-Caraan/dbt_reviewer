## Implementing Seeds

1. Create a file under `data` folder named `employees.csv`.

    **employees.csv**
    
    ```csv
    employee_id, customer_id
    1,1
    2,3
    3,5
    ```

2. Then run the command `dbt seed`. After the command executes, the csv file will materialize in your data platform.
3. After the seed is materialized, you can reference them on your other models.

   For example:

   **customers.sql**

   ```sql
   ...
   ,employees as (
       select * from {{ ref('employees') }}
   )
   ...

   select
       ...
       e.employee_id
   ...
   left join employees e
   ```

4. Next is to create a documentation and tests for your seeds. Under the `data` folder, create a file named `_seeds.yml`.

    **_seeds.yml**
  
    ```yaml
    version: 2
    seeds:
      - name: employees
        description: a csv mapping customer_id to employee_id
        columns:
          - name: employee_id
          - name: customer_id
            tests:
              - unique
              - not_null
    ```
    
5. You can test your seed by running the command `dbt test -s employees`
    
**Resources**
- [seeds](https://docs.getdbt.com/docs/build/seeds)
