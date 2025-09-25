## DBT Free Trial
https://www.getdbt.com/signup

1. Set up your project name
<img width="1919" height="864" alt="image" src="https://github.com/user-attachments/assets/90093df0-b6ff-4d28-aea2-9d0c2abd0e1d" />

2. Add a connection which is Databricks, then fill-up the account fields
- The account would be your account number in your Snowflake account
<img width="1480" height="777" alt="image" src="https://github.com/user-attachments/assets/eab48142-b10f-44fc-ad49-9c91dcc5b9ee" />

3. Fill-up the **Server Hostname** and **HTTP Path** 
- Please refer to the previous wiki page to learn how to get these credentials
<img width="1244" height="442" alt="image" src="https://github.com/user-attachments/assets/d5bac4c9-c584-4f49-9e3c-9be3ca2993ee" />

Next is to choose your repository
- For this tutorial, we use Managed. This is a repository that dbt Labs manages. It will store your code but won't have any access to this repository.
<img width="989" height="518" alt="image" src="https://github.com/user-attachments/assets/36a7b26d-64bd-4a3d-bfb7-993085953375" />

Once that's done. You can start developing in dbt Studio.
<img width="1919" height="871" alt="image" src="https://github.com/user-attachments/assets/3137b467-1845-48a0-9be5-70cf6385eb9e" />

Next is to initialize a dbt project by clicking on **Initialize dbt project**. This will create the necessary folders under your managed repository.
<img width="369" height="799" alt="image" src="https://github.com/user-attachments/assets/072066bc-b510-48f0-aa1a-3238217b4c66" />

Commit your changes by clicking on **Commit**

To be able to materialize dbt models in Snowflake, we need to ensure that our role privileges is set up
- Click on your name on lower-left corner -> **Your profile** -> **Connections** -> **Optional settings**
<img width="1431" height="288" alt="image" src="https://github.com/user-attachments/assets/21e0e337-4b05-4872-b2b4-a885ce6dff7c" />

Once you're on the studio, execute the comamnd ``dbt run``

<img width="555" height="598" alt="image" src="https://github.com/user-attachments/assets/b63f4832-cd47-4841-aa1d-1d52f2ce4285" />

