## Configure Snowflake for dbt Cloud
- Admins and developers need to have permissions on authorized projects to peform certain actions
- Snowflake administrators need ACCOUNTADMIN access in Snowflake to set dbt developers up properly
- As a Snowflake admin log into a Snowflake account using credentials or SSO
- Confirm the role of ACCOUNTADMIN or reach out to an administrator to get the role
- dbt recommends setting up two databases for developers, one for raw data and one where you plan to transform data
- Run admin commands to create a database for 'Analytics'
- Run the create warehouse command to create a warehouse called 'Transforming' for developers
- Create the role called 'Transformer' to give developers access to these objects
- Grant usage on the `snowflake_sample_data` database, as well as the schema of interest, and all tables within that schema to read but not modify anything in the sample database
- Grant multiple privileges on the 'Analytics' database to the role 'Transformer' so developers can build models
- Any developers who want to transform data in dbt Cloud will need the role called 'Transformer'

## Configure Github for dbt Cloud and Snowflake
- Each admin and developer needs access to their company's Github account and Git repository used for dbt Cloud
- As an admin, make sure you have a Github account and have been invited to your team’s Github organization
- Create a new repo using a name like `internal-analytics` or `dbt-project`
- Provide a quick description like “A dbt project for managing data transformations”
- Set the repo to private (you can make it public later)
- It is critical that you do not add a README file at this stage. This will be covered when you initialize your project later
- Leave other settings blank for now

## Set Up a New dbt Cloud Project
- As an admin, you may be creating the first dbt Cloud project for your team and adding developers to the project
- Login to Snowflake and Github in separate browser tabs before you begin
- In a third tab login to dbt Cloud
- Most people will login to dbt Cloud at cloud.getdbt.com. If you are on a virtual private cloud or based outside of the U.S., this will be a different link provided by your dbt account team
- In dbt Cloud, follow the Complete project setup flow
- Name the project 'Analytics' and select Snowflake as the warehouse
- Enter four settings for Snowflake: Snowflake account, database, warehouse, and role
- Make sure to allow traffic from the noted IPs in your firewall, if the need applies to your organization
- Enter development credentials. These will be the username and password associated with Snowflake
- Test your connection
- Connect your Github account by giving dbt access and selecting the specific repositories you want to use
- Initialize the project, commit and push
- Execute dbt run with the example models
- Review the logs
Toggle into Snowflake to make sure the models persisted as tables/views in the dev schema
