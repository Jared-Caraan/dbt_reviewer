## Implementing audit_helper

This is extremely useful when you're making major changes or you're migrating from an on-prem world into dbt. It allows you to compare data models from a different database to your dbt project.

Another use case is when you're making major improvements to the logic of your models, but you would expect them to be the same as your previous version of the dbt model. Audit helper ensures that your values are not changing, even if the logic is.

This is something you would use during your development workflows and include the results in your pull request so your team feels confident and knows that you're not changing the outcome of the data. You're simply improving the logic.

