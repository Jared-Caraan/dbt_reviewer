## DBT Free Trial
https://www.getdbt.com/signup

1. Set up your project name.
<img width="1919" height="864" alt="image" src="https://github.com/user-attachments/assets/90093df0-b6ff-4d28-aea2-9d0c2abd0e1d" />
<hr>

2. Add a connection which is Databricks. Fill-up the **Server Hostname** and **HTTP Path**, then click **Save**.
- Please refer to the previous wiki page to learn how to get these credentials
<img width="1244" height="442" alt="image" src="https://github.com/user-attachments/assets/d5bac4c9-c584-4f49-9e3c-9be3ca2993ee" />
<hr>

3. Go back to **Account Settings**. Answer the fields in the **Development credentials** section.
- For **Auth method**, use *token*.
- For **Token**, use the token that was generated from your Databricks account. Please refer to the previous wiki page to learn more.
- Accept the defaults for the remaining fields
- Test your connection
- Save
<img width="1397" height="749" alt="image" src="https://github.com/user-attachments/assets/b3afee48-0490-4bfa-81ac-4a7cdb968eae" />
<hr>

4. Next is to choose your repository
- For this tutorial, we use Managed. This is a repository that dbt Labs manages. It will store your code but won't have any access to this repository.
<img width="989" height="518" alt="image" src="https://github.com/user-attachments/assets/36a7b26d-64bd-4a3d-bfb7-993085953375" />
<hr>

5. Once that's done. You can start developing in dbt Studio.
<img width="1919" height="871" alt="image" src="https://github.com/user-attachments/assets/3137b467-1845-48a0-9be5-70cf6385eb9e" />
<hr>

6. Next is to initialize a dbt project by clicking on **Initialize dbt project**. This will create the necessary folders under your managed repository.
<img width="369" height="799" alt="image" src="https://github.com/user-attachments/assets/072066bc-b510-48f0-aa1a-3238217b4c66" />
<hr>

7. Commit your changes by clicking on **Commit**
<hr>

8. To test your connection, execute the comamnd ``dbt run``
<img width="555" height="598" alt="image" src="https://github.com/user-attachments/assets/b63f4832-cd47-4841-aa1d-1d52f2ce4285" />

