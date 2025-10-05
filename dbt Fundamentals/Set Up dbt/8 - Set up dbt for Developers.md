## Get the Right Role in Snowflake
- Each developer needs to have the right permissions on authorized projects to develop in dbt Cloud
- Contact the Snowflake administrator at your company to get the unique URL for Snowflake access
- Log into Snowflake, create a new worksheet, and check your role
- If you only have the public role, contact your Snowflake administrator again
- Ask the Snowflake administrator for the role designated for dbt developers
- At dbt Labs we use the role name Transformer and the warehouse name Transforming
- These roles have been created by an admin and granted specific permissions
- The names at your company may differ so maintain contact with your Snowflake administrator
- If you are the one setting this up for your company, watch dbt Cloud and Snowflake for Admins
## Connect Your Github Account to dbt Cloud
- Each developer needs access to their organization's Github account and the Git repository for dbt Cloud
- As a developer, create a Github account if you don't already have one
- Contact the Github administrator at your company and request access to your organization's repository
- Associate your Github account with you organization's account
- You should be able to toggle between your Github account and your organization's Github account
- Find the associated internal dbt project repository to verify you have access
- If you cannot find the dbt project repository, ask your Github administrator to add you to the organization's Github repository
## Access the Project and Enter Credentials
- Each developer needs to integrate Github and enter Snowflake credentials in their profile to develop in dbt Cloud
- As a developer, log in to Github, and Snowflake in separate tabs
- Log in to dbt Cloud in a third tab
- Navigate to Profile Settings in dbt Cloud and connect your Github account to your profile
- Make sure Github is linked to dbt Cloud in Linked Accounts
- Next navigate to Credentials and select the project you want to join
- Edit and enter your Snowflake username and password as Development Credentials in dbt Cloud
- Navigate to Develop and get into the IDE
The last step is to make sure you can query Snowflake from dbt Cloud
Click create new file in the center of the screen to open a new statement tab
Execute arbitrary SQL code as a test
