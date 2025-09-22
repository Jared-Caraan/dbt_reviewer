## DBT Free Trial
https://www.getdbt.com/signup

Set up your project name
<img width="1919" height="864" alt="image" src="https://github.com/user-attachments/assets/90093df0-b6ff-4d28-aea2-9d0c2abd0e1d" />

Add a connection which is Snowflake, then fill-up the account fields
- The account would be your account number in your Snowflake account
<img width="1480" height="777" alt="image" src="https://github.com/user-attachments/assets/eab48142-b10f-44fc-ad49-9c91dcc5b9ee" />

Fill-up the development credentials and test your Snowflake connection to see if your credentials are correct
- For this tutorial, we opt on using Username and Password. Key pair option can be used if you have an enterprise account that uses SSO.
- Your username and password is your login credentials to Snowflake
<img width="1417" height="857" alt="image" src="https://github.com/user-attachments/assets/09e55010-a421-4691-85a3-651e67690cea" />

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

