## Environments, jobs, and runs

**Environments** encompass a collection of settings for how you want to run your dbt project. This includes:

- dbt version
- git branch
- data location (target schema)

The **development environment** applies the same settings for all developers working in dbt Cloud. **Deployment environments** can be set up to support various different deployment strategies and architectures (more on that later in the course.)

**Jobs** are a set of dbt commands that you run within an environment. This can include commands like **dbt build** with any selection syntax / flags that you may want. These jobs can then be kicked off through a variety of means covered in the rest of this course.

**Runs** are the implementation of a specific job that you have configured that was triggered. While a job is running, you can see that status of that job in real time. Once the job is finished, you can see the run results and view artifacts from that particular run.

**Resources**
- [dbt docs: Environments](https://docs.getdbt.com/docs/collaborate/environments)
