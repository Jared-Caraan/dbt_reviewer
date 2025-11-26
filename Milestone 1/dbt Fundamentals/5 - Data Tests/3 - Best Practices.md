## Data Testing Best Practices

### When do you test your sources?
You should test your sources to validate the quality of your raw data. These tests should be simple and focused on the basics.

### When do you test your models?
You should test your models to validate your transformations.These tests check the integrity of your dbt code and the business logic that you have applied.

> [!NOTE]
> Test sources for data integrity and test models for transformation integrity.

## Using dbt Copilot for testing

### Enabling dbt Copilot
1. Click on your name -> **Your profile** -> **Account** -> Under **Settings** -> Tick **Enable account access to dbt Copilot features**

### Generating tests using dbt Copilot
1. Click on **dbt Copilot** on dbt Studio -> **Generic tests**
2. Then it will generate a yml file by itself.
3. Check its work and make revisions if necessary since it's not perfect.
