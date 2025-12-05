## Packages
- Import models and macros that have already been written.
- Leverage modeling of common sources.
- Leverage macros across your dbt project.
- Find packages at [hub.getdbt.com](https://hub.getdbt.com/).

## Installation
1. Navigate to [hub.getdbt.com](https://hub.getdbt.com/).
2. For this example, click on **dbt_utils**, then copy the code to install that package.
3. Copy the code to your `packages.yml`. Create the file if it doesn't exist yet.
4. Go back to dbt hub and copy the code for CodeGen package as well. Codegen is useful for generating SQL code for our staging layer or maybe generating a YAML file to fill out documentation and tests.

    This is what we call the hubsite mechanism for installing packages:
    ```yaml
    packages:
      - package: dbt-labs/dbt_utils
        version: 1.3.2
      - package: dbt-labs/codegen
        version: 0.14.0
    ```

    This one is using the direct source or the github repository:
    1. On the dbt hub website, click on the package, then click on the repository underneath the package name.
    2. Copy the HTTPS/SSH link, then replace `package:dbt-labs/codegen` with `git:<HTTP/SSH>`.
    3. Then replace `version:0.14.0` with `revision:<repo branch you want to use>`.
    ```yaml
    packages:
      - git: https://github.com/dbt-labs/dbt-codegen.git
        revision: main
    ```
    
    Another option is to install local subdirectories as projects.
    ```yaml
    packages:
      local: sub_project
    ```
5. Finally, run the command `dbt deps` to install dependencies.
