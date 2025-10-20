## Create a job
1. On dbt Cloud homepage, navigate to the side menu -> **Orchestration** -> **Jobs**
2. Click on **Create job** -> **Deploy job**
3. Choose which environment your job will live in.
4. Concisely name your job, accept the defaults on the **Execution settings** section. Modify some triggers according to your desired schedule. CRONs are accepted as well. Then click **Save**.

## Review a dbt job
Once the job runs, you can click on the Run details. You will see the execution steps that have ran or is running.

One detail that you'll see is the branch that it's cloning from. Next is you'll see the connection to the data platform and dbt needs to execute any dependencies. These first three steps always happen for every job - `clone git repository`, `creating connection to data platforms`, and running `dbt deps`. The remaining jobs are dependent on job settings.

One detail you will also see is the job status if it succeeds or not and its runtime. You can also see the Model Timing which is a swimlane of how different things are executed.

Inside the `dbt build` log, you will see what models and tests are executed on this specific run. You can also see their respective statuses and runtimes. You will also see how many objects have passed, how many warnings and errors have been generated, and how many were skipped.
