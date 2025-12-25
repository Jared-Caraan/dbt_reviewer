## Customizing dbt Behavior in Different Environments

There are occasions when you might want dbt to behave differently based on what environmnt being used. A good example is wanting a different behavior for the schemas used when leveraging the custom schema configuration.

Other examples:
- limiting the number of rows
- using different databases or schemas for the dbt sources
- changing the severity of a test

Mechanisms to achieve these behaviors:
1. using the **target** Jinja variable
2. leveraging **environment variables**
