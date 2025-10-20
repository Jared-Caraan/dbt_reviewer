## Configure Deployment Environment

1. On dbt Cloud homepage, navigate to the side menu -> **Orchestration** -> **Environments**
2. Click on **Create environment**
3. Fill-in the details for the **General Settings**:
   - **Environment name** - *Production*
   - **Environment type** - *Deployment*
   - **Set deployment type** - *Production*
   - Accept the default for **dbt version**, it is recommended to use the latest one. Multiple environments must have the same version too.
   - Tick **Only run on a custom branch** if you want, but dbt is smart enough to pull from the Github default branch
4. Choose a **Connection**. For this example, the previously created **Snowflake** is chosen. This will automatically fill-up the **Connection Settings** area.
5. Overwrite the values in your **Role**, **Database**, and **Warehouse**. They should not be the same as the development environment.
6. In the **Deployment credentials**, use *Username and password* for the **Auth method**. Your username is your service account name. Be mindful of your password as well.
7. Test your connection. Then click **Save**

## Create a job
1. On dbt Cloud homepage, navigate to the side menu -> **Orchestration** -> **Jobs**
2. Click on **Create job** -> **Deploy job**
3. Choose which environment your job will live in.
4. Concisely name your job, accept the defaults on the **Execution settings** section. Modify some triggers according to your desired schedule. CRONs are accepted as well. Then click **Save**.
