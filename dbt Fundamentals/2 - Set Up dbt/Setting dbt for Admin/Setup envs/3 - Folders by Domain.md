## Set up Folder Structure by Domain

In this example, let's set up the folder structure for three teams or domains - Finance, Sales, and Marketing.

#### Creating folders per team
The staging folder will organize all the source-conformed logic. This is where you'll do some simple cleaning on raw data that has been imported into Snowflake. Usually, teams will prefix these models with ``stg_``.
1. Under the **models** directory, create a **finance** folder.
2. Create an empty file (e.g. *.gitkeep* file) under the **finance** folder.
3. Then, under the **models** directory, create a **marketing** folder.
4. Create an empty file (e.g. *.gitkeep* file) under the **marketing** folder.
5. Then, under the **models** directory, create a **sales** folder.
6. Create an empty file (e.g. *.gitkeep* file) under the **sales** folder.
7. Commit your changes

#### Configure dbt_project.yml and README.md
1. Change the value of ``name:`` key
2. Change ``my_new_project:`` to the given value in the previous step.
3. Delete unused model configurations.
4. Update the **README.md file**. This will help other developers get started on the project.
5. Commit your changes.
