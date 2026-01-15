## Common job creation

**Creating a Standard job**

1. **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a deployment type environment.
    - Job name - Standard Job
    - Environment - Choose production
    - Target name - depends on the situation
    - It is recommended to tick **Generate docs on run** and **Run source freshness**
    - Add your commands on the execution settings (e.g. `dbt build`)
    - Configure your desired schedule for your job (e.g. 12 hrs everyday at midnight)
3. Hit **Save**

> [!NOTE]
> If you tick the **Run source freshness** and something fails in the freshness test, it will still continue downstream. But if you add freshness validation as a command and it fails, the pipeline will not continue.

**Creating a full refresh job**

1. **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a deployment type environment.
    - Job name - Full refresh
    - Same setup with standard job except for commands and scheduling
    - Put the flag `--full-refresh` on the commands (`dbt build --full-refresh`)
    - Schedule it once a week only
3. Hit **Save**

**Creating a time-sensitive job**

1. **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a deployment type environment.
    - Job name - Fct Orders Hourly
    - Same setup with standard job except for run timeout, commands and scheduling
    - Provide a **Run Timeout** value in seconds (e.g. 3550 seconds)
    - Put the flag `--select` on the commands (`dbt build --select +fct_orders+`)
    - You can schedule it hourly on business days
3. Hit **Save**

**Creating a fresher rebuild job**

1. **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a deployment type environment.
    - Job name - Fresher Rebuild
    - Same setup with standard job except for commands and scheduling
    - In **Defer to a previous run state?**, you can choose and defer perhaps to your standard run if it's ran in the middle of the day and want to check the source freshness data from the standard run in the morning.
    - In the commands, you can put something like `dbt build --select source_status:fresher+`
    - You can schedule it once a day on business days
3. Hit **Save**
