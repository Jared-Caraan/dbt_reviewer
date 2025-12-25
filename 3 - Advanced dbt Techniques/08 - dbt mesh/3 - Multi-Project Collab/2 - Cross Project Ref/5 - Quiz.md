You are in a downstream project trying to reference a model named fct_orders from an upstream project named base_project . Select the correct cross-project ref statement.

a. {{ ref('base_project', 'fct_orders') }}\
b. {{ ref(base_project, fct_orders) }}\
c. {{ ref('fct_orders', 'base_project') }}\
d. {{ ref(fct_orders, base_project) }}

Answer: a

##
Cross-project lineage is enabled by what?

a. The dependencies.yml file.\
b. Successfully using the cross-project ref macro.\
c. running the command `dbt docs generate`.\
d. running the command `dbt build`.

Answer: b

##
An analytics engineer has set up two dbt Cloud projects. They’re referencing a model in one project in the other project using this code.

{{ ref(‘base_project’, ‘fct_customer_orders’) }}

Which of the following is NOT a potential reason why they could be getting an error message?

a. Their downstream project needs to have a production job run successfully.\
b. The other project being referenced isn’t named `base_project`.\
c. They didn’t set up a dependencies.yml file in both projects.\
d. They only set up a dependencies.yml file in one project.

Answer: a
