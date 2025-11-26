## Installation of dbt Fusion Engine and VS Code Extension

The dbt fusion engine is the underlying machine that is powering the dbt VS Code extension. The installation process is provided in the link below.

[Installation of dbt Fusion Engine and VS Code Extension](https://docs.getdbt.com/guides/fusion?installation=windows&step=3)

## Starting a project

One option to start a project is to initialize one.
> `dbtf` is the prefix of most dbt commands we'll use in the VS Code extension.

To initialize a project, follow the steps in the link below:

[Initialize a dbt project](https://docs.getdbt.com/guides/fusion?installation=windows&step=4).

Another option is to clone an existing repository.
You can use `git clone` on this [sample repo](https://github.com/dbt-labs/dbt-learn-gt-init).

## Profiles.yml

When you have cloned a project, you might encounter an error due to a missing `profile.yml` file.

A `profile.yml` file is where it has the connection to your data platform.

1. Since you have cloned a project, the assumption is you already have the correct folder setup. Given this, you can now run the command `dbtf init`.
2. You will be prompted to choose which data platform to connect to. In this example, let's say that we'll choose Snowflake.
3. Next is you need to enter your account number in Snowflake.
4. Next is to enter your username.
5. Next is to choose authentication method. In this example, we'll choose password.
6. Enter your password as well.
7. Next is you can have the option to enable MFA, which is a yes or no question.
> [!WARNING]
> In the future, Snowflake will require MFA for all username and password.
8. Enter your snowflake role.
9. Enter your database, warehouse, and schema.

## Ensure your data platform is connected

To verify connectivity, execute the command `dbtf compile` and `dbtf run`.

## Benefits of the dbt Fusion Engine

1. There's a functionality called **Preview CTE** to visualize and debug CTEs.
2. `dbt: Show Column Lineage` -> *Column* - You can see the lineage and transformation of the selected column.
3. Hovering over column names shows a tooltip with its data type and origin.
4. Faster compile times.
5. Quick error alerts.
