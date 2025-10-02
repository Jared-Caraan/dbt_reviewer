## Prerequisite
- A dbt Cloud connected to a data warehouse

## Create a Production Service Account in Snowflake
Sample Query:
```sql
CREATE OR REPLACE USER PROD_SERVICE_ACCOUNT_USER
PASSWORD = 'YhcLoFPt7mi!thtD'
COMMENT = 'For prod deployment'
DEFAULT_WAREHOUSE = transforming_prod
DEFAULT_ROLE = transfomer_prod
MUST_CHANGE_PASSWORD = FALSE;
```
- Make sure that the production warehouse, database, and role is created.
- Grant the production role to your production service account.

Sample Query:
```sql
GRANT ROLE transfomer_prod TO USER PROD_SERVICE_ACCOUNT_USER;
```

## Configure Environments in dbt Cloud
1. On dbt Cloud homepage, navigate to the side menu -> **Orchestration** -> **Environments**
2. Click on **Create environment**
3. Fill-in the details for the **General Settings**:
   - **Environment name** - *Production*
   - Accept the default for **dbt version**, it is recommended to use the latest one. Multiple environments must have the same version too.
   - Tick **Only run on a custom branch** if you want, but dbt is smart enough to pull from the Github default branch
4. Choose a **Connection**. For this example, the previously created **Snowflake** is chosen. This will automatically fill-up the **Connection Settings** area.
5. Overwrite the values in your **Role**, **Database**, and **Warehouse**. They should not be the same as the development environment.
6. In the **Deployment credentials**, use *Username and password* for the **Auth method**. Your username is your service account name, in this example, it's *PROD_SERVICE_ACCOUNT_USER* from the query above. Then the password would be the *YhcLoFPt7mi!thtD*. Just put an arbitrary name for the schema, because it will be overriden by the models eventually.
7. Test your connection. Then click **Save**
