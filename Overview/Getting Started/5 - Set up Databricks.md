## Databricks Setup

1. Create an account on https://www.databricks.com/
<hr>

2. Once you complete the registration, you will be redirected to the homepage. On the side menu -> **SQL Warehouses**. Create a SQL Warehouse and fill-in the details. If unable to create, then Databricks may have already provided a warehouse for you.
<img width="1919" height="868" alt="image" src="https://github.com/user-attachments/assets/e5c4c521-a441-41cf-b924-8b5760895816" />
<hr>

3. Then, on the side menu -> **New +** -> **Add or upload data** -> **Create or modify table**. Then upload the ff. files:
- [stripe_payments.csv](https://github.com/user-attachments/files/22522303/stripe_payments.csv)
- [jaffle_shop_orders.csv](https://github.com/user-attachments/files/22522310/jaffle_shop_orders.csv)
- [jaffle_shop_customers.csv](https://github.com/user-attachments/files/22522313/jaffle_shop_customers.csv)
<img width="1919" height="853" alt="image" src="https://github.com/user-attachments/assets/a5edf744-2007-4820-bc1f-dc7c55135da6" />

Notes:
- Option should be *Create new table*.
- Change the schema to *jaffle_shop* for customers and orders; *stripes* for payment. If already existing, opt for another name, then just rename later.
- Upload one at a time.
<hr>

4. Rename your workspace catalog to *raw*
<img width="1676" height="857" alt="image" src="https://github.com/user-attachments/assets/be6ccc5b-e3f6-4fdd-a3f5-d200f14bcc6f" />
<hr>

5. Create a new catalog by clicking on the plus sign on top of the catalog menu. Name it *analytics*. This is where dbt transformed models will live or considered as the target database.
<img width="1673" height="817" alt="image" src="https://github.com/user-attachments/assets/df81d866-5b13-4069-bbf5-87e69f98e030" />
<hr>

6. Next is to set up a user token. Click on your profile at top-right corner -> **Settings** -> **Developer** -> **Manage** -> **Generate new token** -> Name the token *dbt* -> **Generate** -> Copy your token somewhere.
<img width="1670" height="864" alt="image" src="https://github.com/user-attachments/assets/291484c2-6af2-4dc4-a575-188fc70ac5da" />

7. Next thing we need is the server host name. This can be seen on the URL.
<img width="936" height="61" alt="image" src="https://github.com/user-attachments/assets/b749325e-4539-4200-b779-45f7166a4efe" />

8. Finally, we need to retrieve our HTTP path. Click on **SQL Warehouses** -> Click on your warehouse -> Get the last portion of your URL starting with **\sql**
 <img width="1919" height="945" alt="image" src="https://github.com/user-attachments/assets/5a77367c-060c-4aa2-a10f-f6d987156f53" />
