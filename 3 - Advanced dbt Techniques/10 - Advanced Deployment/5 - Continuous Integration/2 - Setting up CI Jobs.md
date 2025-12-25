## Setting up CI Jobs

It is recommended to create a new CI environment for CI jobs.

**Creating a new environment**

1. **Orchestration** -> **Environments** -> **Create environment**
2. Fill-in the necessary details:
    - Environment Name - CI
    - dbt Version - Latest (match your other environments)
    - Connection - Accept your default setup to your data platform
    - Fulfill your credentials to your data platform
3. Hit save

**Creating a new job**

1. **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a deployment type environment.
    - Job name - CI Job
    - Environment - CI
    - Add your commands on the execution settings (e.g. `dbt build`)
    - Configure trigger on webhooks - tick **Run on Pull Request**
3. Hit **Save**
