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

> [!INFO]
> If you tick the **Run source freshness** and something fails in the freshness test, it will still continue downstream. But if you add freshness validation as a command and it fails, the pipeline will not continue.

**Creating a full refresh job**

1. **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a deployment type environment.
    - Job name - Full refresh
    - Same setup with standard job except for commands and scheduling
    - Put the flag `--full-refresh` on the commands (`dbt build --full-refresh`)
    - Schedule it once a week only
3. Hit **Save**
