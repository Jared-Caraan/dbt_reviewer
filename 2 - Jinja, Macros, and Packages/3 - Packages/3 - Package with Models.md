## Package with Models
Packages are not just limited to macros that you can reuse in your project. They can have all sorts of things like models, seeds, analyses, etc. In this case, we are going to try installing a package that has Models, specifically models about Snowflake spending.

### snowflake_spend package

To see details about the package: [snowflake_spend package](https://hub.getdbt.com/gitlabhq/snowflake_spend/latest/)

1. Copy and paste the code into your `packages.yml` and hit **save**.
2. Run the `dbt deps` command.
3. Skim through the readme file because there might be dependencies that the package demands.
   - In this example, we need to refer to a specific [csv file](https://gitlab.com/gitlab-data/analytics/-/blob/master/transform/snowflake-dbt/seeds/seed_data/snowflake_contract_rates.csv) and add it to our `seeds` directory.
   - Run `dbt seed` to load CSV files into your data warehouse as tables so they can be referenced in your dbt models.
   - You will also need to configure `dbt_project.yml` and add this code under the model name part.

     ```yaml
     snowflake_spend:
      enabled: true
     ```
4. Run `dbt build` to materialize everything.
5. All the new models from `snowflake_spend` package are found under `dbt_packages/snowflake_spend/models` or you can read the code through their [repo](https://github.com/gitlabhq/snowflake_spend/tree/master/models).
6. Run `dbt docs generate` to learn the metadata of the `snowflake_spend` package and their models. You will see their lineage, columns, data types, etc.
7. If you want to run only the models inside a specific package, you can run the command - `dbt build --select package:snowflake_spend`
