## Test configurations

- Similar to models, there are several configurations that you can add to the tests in your dbt project.
    - **severity** allows you to toggle between **warn** and **error** when a test doesn't meet your assertions.
    - **warn_if** and **error_if** allow you to set thresholds for warning or errors for a specific test
    - **where** allows you to filter down to a subset of rows that you want to test
    - **limit** allows you to limit the number of returned failing records.
    - **store_failures** allows you to enable storing of the failing records in your data platform
        - **schema** allows you to specify where you want to store the failing records if you enable store_failures.

- Test configurations can be applied in various places including:
    - yaml configurations where generic tests are applied
    - config blogs in the top of singular tests
    - dbt_project.yml to apply configurations to tests across your project in one place.

## Related resources
- [dbt Docs: Storing test failures](https://learn.getdbt.com/learn/course/advanced-testing/test-configurations-50-min/test-configurations?page=8#:~:text=dbt%20Docs%3A%20Storing,Docs%3A%20Test%20configurations)
- [dbt Docs: Test configurations](https://learn.getdbt.com/learn/course/advanced-testing/test-configurations-50-min/test-configurations?page=8#:~:text=dbt%20Docs%3A%20Storing,Docs%3A%20Test%20configurations)
