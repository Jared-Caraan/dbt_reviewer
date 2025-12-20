### dbt_meta_testing package
**Steps:**
- Install external [package](https://hub.getdbt.com/tnightengale/dbt_meta_testing/latest/)
    - Follow the instruction provided in the dbt hub
- Add suggested configuration to the dbt_project.yml file
    - Add `+required_tests: {"unique.*|not_null": 1}` in the `models:` section.
    - You can add any other type of tests.
- Run dbt `run-operation required_tests`
    - It will fail if you haven't provided any `unique` or `not null` tests or whatever type of test you specified.

You can override its configuration on the model-level by:

<img width="291" height="131" alt="image" src="https://github.com/user-attachments/assets/8a145fab-829b-44d6-b925-f411b8e51457" />
