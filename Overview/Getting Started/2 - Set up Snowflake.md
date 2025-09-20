## Snowflake Free Trial
https://signup.snowflake.com/?utm_cta=trial-en-www-homepage-top-right-nav-ss-evg&_ga=2.74406678.547897382.1657561304-1006975775.1656432605&_gac=1.254279162.1656541671.Cj0KCQjw8O-VBhCpARIsACMvVLPE7vSFoPt6gqlowxPDlHT6waZ2_Kd3-4926XLVs0QvlzvTvIKg7pgaAqd2EALw_wcB

Once you finish signing up and activating your account, you will be redirected to the homepage.
<img width="1919" height="835" alt="image" src="https://github.com/user-attachments/assets/53ba3414-c5be-4787-b74a-6e377508116d" />

On the left-side panel, click on **+** which is the Create button, then click **SQL File**.
Create the following database objects
```sql
CREATE WAREHOUSE transforming;
CREATE DATABASE raw;
CREATE DATABASE analytics;
CREATE SCHEMA raw.jaffle_shop;
CREATE SCHEMA raw.stripe;
```

Then, followed by the *customers* table
```sql
CREATE TABLE raw.jaffle_shop.customers 
( 
    id INTEGER,
    first_name VARCHAR,
    last_name VARCHAR
);
```

Load some data into the *customers* table
```sql
COPY INTO raw.jaffle_shop.customers (id, first_name, last_name)
FROM 's3://dbt-tutorial-public/jaffle_shop_customers.csv'
file_format = (
    TYPE = 'CSV'
    field_delimiter = ','
    skip_header = 1
);
```

Check if your data has been loaded by selecting from the table
```sql
SELECT * FROM RAW.JAFFLE_SHOP.CUSTOMERS;
```
<img width="1431" height="504" alt="image" src="https://github.com/user-attachments/assets/c86d4ea3-01fd-494e-9707-120b0cc71ec4" />

Create the *orders* table
```sql
CREATE TABLE raw.jaffle_shop.orders
( 
    id INTEGER,
    user_id INTEGER,
    order_date DATE,
    status VARCHAR,
    _etl_loaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Then load some data into the *orders* table
```sql
COPY INTO raw.jaffle_shop.orders (id, user_id, order_date, status)
FROM 's3://dbt-tutorial-public/jaffle_shop_orders.csv'
file_format = (
    TYPE = 'CSV'
    field_delimiter = ','
    skip_header = 1
);
```

Check if your data has been loaded by selecting from the table
```sql
SELECT * FROM RAW.JAFFLE_SHOP.ORDERS;
```
<img width="1430" height="541" alt="image" src="https://github.com/user-attachments/assets/8c989fa0-02a5-4d7c-b31b-29bdcb9e6274" />

Then, create the *payment* table
```sql
CREATE TABLE raw.stripe.payment 
( 
    id INTEGER,
    orderid INTEGER,
    paymentmethod VARCHAR,
    status VARCHAR,
    amount INTEGER,
    created DATE,
    _batched_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Then load some data into the *payment* table
```sql
COPY INTO raw.stripe.payment (id, orderid, paymentmethod, status, amount, created)
FROM 's3://dbt-tutorial-public/stripe_payments.csv'
file_format = (
    TYPE = 'CSV'
    field_delimiter = ','
    skip_header = 1
);
```

Check if your data has been loaded by selecting from the table
```sql
SELECT * FROM RAW.STRIPE.PAYMENT;
```
<img width="1417" height="509" alt="image" src="https://github.com/user-attachments/assets/62c77470-744f-427a-a1e0-7b6b7b9d18c4" />

To find your account number, there are two ways:
1. URL (highlighted)
<img width="890" height="57" alt="image" src="https://github.com/user-attachments/assets/784104bb-9e59-49f0-82bc-a50aee6221f8" />

2. Profile on the left-side tab
<img width="752" height="701" alt="image" src="https://github.com/user-attachments/assets/26ef2682-94f0-445c-8bb8-e8521fb42801" />

