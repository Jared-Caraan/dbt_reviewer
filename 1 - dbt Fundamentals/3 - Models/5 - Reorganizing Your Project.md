## Reorganizing dbt Project
1. Delete unused or unneeded folders/files.
2. Rename files according to their naming convention e.g. `stg_`, `fct_`, `dim_`, `int_`, etc.
3. Create folders according to their maturity e.g. staging, marts, etc.
4. Move your models to their respective folders.
<img width="367" height="370" alt="image" src="https://github.com/user-attachments/assets/ae28ff0e-98a6-4110-97ad-aad7c3fc0dcb" />

5. For the branch name, you can prefix it by `feat/` then a brief working title.
6. In `dbt_project.yml`, ensure that the project name in Line 5 and its corresponding value under `models:` are descriptive enough.
7. In `dbt_project.yml`, remove any configurations that pertains to deleted folders.
8. Staging models as a best practice should be a view.
<img width="824" height="373" alt="image" src="https://github.com/user-attachments/assets/54f73038-9a02-4b43-99f0-c277881ccc40" />

9. Marts models are typically materialized as tables. These are frequently being queried by the BI tool.
<img width="363" height="95" alt="image" src="https://github.com/user-attachments/assets/362bf1a0-09d1-445f-847c-4ef3f70898ca" />


> [!NOTE]
> The plus sign in front of the *materialization* indicates that it's a property instead of a folder

10. Split out the subfolders in *staging* connected to a specific source.
11. Split out the subfolders in *marts* to what business entity is consuming those models.

> [!NOTE]
> Snowflake will not drop a table if it's been renamed. It will just create or materialize a new table.
