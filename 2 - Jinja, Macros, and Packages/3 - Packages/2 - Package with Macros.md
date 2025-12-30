## Package with Macros

### date_spine macro
In this example, we will be working with `dbt_utils` package.

1. Import `dbt_utils` package by copying the code in `packages.yml`. Then, run the command `dbt deps`.
2. Let's say we want to utilize the macro `date_spine` within `dbt_utils` package.
3. You can find the `date_spine` macro within the package, then copy the [sample code](https://github.com/dbt-labs/dbt-utils/tree/1.3.2/#date_spine-source) from the repository.
   <details>
   <summary>Macro Link in dbt hub page</summary>
   <img width="520" height="688" alt="image" src="https://github.com/user-attachments/assets/407228ed-9661-4e90-a6b3-d8d62cf302e1" />
   </details>
   <details>
   <summary>Sample date_spine code</summary>
   
   ```jinja
   {{ dbt_utils.date_spine(
        datepart="day",
        start_date="cast('2019-01-01' as date)",
        end_date="cast('2020-01-01' as date)"
       )
   }}
   ```
   </details>
4. Create a new file under `models` directory and name it `date_spine.sql`. Copy the sample code into the file and click **Preview**.
5. You can click **Compile** to see the under-the-hood SQL query of the macro.
6. To see the macro in detail, you can navigate to the [macro page](https://github.com/dbt-labs/dbt-utils/blob/1.3.2/macros/sql/date_spine.sql) in the repository.

##

### generate_surrogate_key macro
In this another example, we will be working with `generate_surrogate_key` macro under `dbt_utils` package.

This sample model shows the `customer_id` and `order_date` and their occurrence at the same time.
<details>
<summary>Sample Model without the macro</summary>

```sql
select
    customer_id,
    order_date,
    count(*) as c
from {{ ref('stg_orders') }}
group by 1,2
```
</details>

<details>
<summary>Sample Model with the macro</summary>

```sql
select
    customer_id,
    order_date,
    {{ dbt_utils.generate_surrogate_key('customer_id', 'order_date') }} as primary_key
    count(*) as c
from {{ ref('stg_orders') }}
group by 1,2
```
</details>

To see the macro description: [generate_surrogate_key description](https://github.com/dbt-labs/dbt-utils/tree/1.3.2/?tab=readme-ov-file#generate_surrogate_key-source)

To see the code in detail: [generate_surrogate_key macro](https://github.com/dbt-labs/dbt-utils/blob/1.3.2/macros/sql/generate_surrogate_key.sql)
