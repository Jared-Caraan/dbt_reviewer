## Setting Up Direct Promotion

We're gonna set up the objects in dbt Cloud necessary to support a one trunk Git workflow. In order to do this, we'll need an environment to run our production jobs that will pull from the main branch of the repo. We'll also wanna set up a CI environment as well as a CI job to check the 
changes in the development branches to make sure that they don't break our production environment before they are merged into the main branch.

**Environment**
1. To create environments, go to **Orchestration** -> **Environments** -> **Create environment**.
2. Fill out the configurations necessary to set up a deployment type environment.
    - Name - Production
    - dbt Version - latest
    - Untick **Only run on a custom branch** - this means that it will only pull from the main/master branch
    - For the **Connection** part, choose the connection that was set up when the project was created in the first place.
    - For the **Deployment Credentials**, fill-in the authentication values for your data platform in the production environment, as well as choose your schema for production. Test your connection to verify that your credentials are correct.

**Jobs**
1. Now that your environment is created, you can now create jobs. Click on your production environment, scroll down and click **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a deployment type environment.
    - Job name - Production
    - Environment - Choose production
    - It is recommended to tick **Generate docs on run**
    - Add your commands on the execution settings (e.g. `dbt build`)
    - Configure your desired schedule for your job (e.g. 12 hrs everyday at midnight)
    - On **Advanced settings** -> Target name - prod
3. Hit **Save**
