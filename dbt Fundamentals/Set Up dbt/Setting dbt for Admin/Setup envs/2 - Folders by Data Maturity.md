## Set up Folder Structure by Data Maturity

#### Set up a staging folder
The staging folder will organize all the source-conformed logic. This is where you'll do some simple cleaning on raw data that has been imported into Snowflake. Usually, teams will prefix these models with ``stg_``.
- Under the **models** directory, create a **staging** folder.
- Create an empty file (e.g. *.gitkeep* file)
- Commit your changes

#### Set up a marts folder
The marts folder will organize all your business-conformed logic. This is where you'll combine your staging models to roll-up to your key business concepts. Usually, teams will prefix these models with ``dim_`` or ``fct_``.
- Under the **models** directory, create a **marts** folder.
- Create an empty file (e.g. *.gitkeep* file)
- Commit your changes

#### Configure dbt_project.yml and README.md
1. Change the value of ``name:`` key
2. Change ``my_new_project:`` to the given value in the previous step.
3. Delete unused model configurations.
4. Update the **README.md file**. This will help other developers get started on the project.
5. Commit your changes.
