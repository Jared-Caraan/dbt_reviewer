## Implementing audit_helper

This is extremely useful when you're making major changes or you're migrating from an on-prem world into dbt. It allows you to compare data models from a different database to your dbt project.

Another use case is when you're making major improvements to the logic of your models, but you would expect them to be the same as your previous version of the dbt model. Audit helper ensures that your values are not changing, even if the logic is.

This is something you would use during your development workflows and include the results in your pull request so your team feels confident and knows that you're not changing the outcome of the data. You're simply improving the logic.

##

Copy the code from the [audit_helper page](https://hub.getdbt.com/dbt-labs/audit_helper/latest/) into `packages.yml`.

<img width="645" height="233" alt="image" src="https://github.com/user-attachments/assets/0f5e0f57-b900-4339-9a47-ca443552256f" />

### [quick_are_relations_identical](https://github.com/dbt-labs/dbt-audit-helper/tree/0.12.2/#quick_are_relations_identical-source)

Let's say the team wants to refactor `fct_orders` to make it more optimal. Then they want to validate if the new version of the `fct_orders` has still the same relation to the older one despite the logic change.

