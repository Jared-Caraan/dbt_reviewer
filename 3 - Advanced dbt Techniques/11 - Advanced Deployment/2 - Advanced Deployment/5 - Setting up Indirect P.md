## Setting up Indirect Promotion

We're gonna set up the objects in dbt Cloud to support a many trunk Git workflow. 

**Environment**

Make a quick adjustment to your existing development environment.

1. Go to your **Development** environment -> **Edit**.
2. Tick **Only run on a custom branch** -> set the value of **Custom branch** to _qa_ -> **Save**.

Create a QA environment.

1. Go to **Orchestration** -> **Environments** -> **Create environment**.
2. Fill out the configurations necessary to set up a QA environment.
    - Name - QA
    - dbt Version - latest
    - Tick **Only run on a custom branch** -> set the value of **Custom branch** to _qa_
    - For the **Connection** part, choose the connection that was set up when the project was created in the first place.
    - For the **Deployment Credentials**, fill-in the authentication values for your data platform in the QA/production environment, as well as choose your schema for QA. Test your connection to verify that your credentials are correct.
3. Click **Save**.

Create a Production environment.

1. Go to **Orchestration** -> **Environments** -> **Create environment**.
2. Fill out the configurations necessary to set up a deployment type environment.
    - Name - Production
    - dbt Version - latest
    - Leave **Only run on a custom branch** unticked.
    - For the **Connection** part, choose the connection that was set up when the project was created in the first place.
    - For the **Deployment Credentials**, fill-in the authentication values for your data platform in the production environment, as well as choose your schema for production. Test your connection to verify that your credentials are correct.
3. Click **Save**.

**Jobs**

Create the QA job

1. **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a QA environment.
    - Job name - QA
    - Environment - Choose QA
    - Add your commands on the execution settings (e.g. `dbt build`)
    - Configure your desired schedule for your job (e.g. 12 hrs everyday at midnight)
    - On **Advanced settings** -> Target name - qa
3. Hit **Save**

Create the production job

1. **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a deployment type environment.
    - Job name - Production
    - Environment - Choose production
    - It is recommended to tick **Generate docs on run**
    - Add your commands on the execution settings (e.g. `dbt build`)
    - Configure your desired schedule for your job (e.g. 12 hrs everyday at midnight)
    - On **Advanced settings** -> Target name - prod
3. Hit **Save**
