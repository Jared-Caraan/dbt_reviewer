## Continuous Integration and Slim CI

**Continuous integration** traditionally is a devops practice for running automated checks on your code changes before merging into another branch. In the context of dbt, you can leverage CI to ensure that you models build and pass your assertions before merging them into your main branch.

**Slim CI** refers to smart way of running a CI build by only building and testing models that have been updated and those downstream of them.

## Resources
- [dbt docs: dbt Cloud CI Job](https://docs.getdbt.com/docs/deploy/cloud-ci-job#understanding-dbt-cloud-slim-ci)
