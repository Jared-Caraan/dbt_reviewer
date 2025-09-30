## Configure Snowflake for dbt

1. Login to your Snowflake account. It may be through username and password or SSO.
2. Make sure that you have the right role to grant privileges. That role is being an **ACCOUNTADMIN**. You can verify your role by looking underneath your profile name on the side menu.
<img width="300" height="119" alt="image" src="https://github.com/user-attachments/assets/5211ac03-a5b5-4af9-9f02-7aa34cd75189" />

3. Create your databases and warehouses using your role.
4. Setup a role for dbt developers to access these objects. You can name your own role.

Sample Query:
```sql
CREATE ROLE transformer;
```

5. Grant privileges to the roles.

Sample Query:
```sql
GRANT IMPORTED PRIVILEGES ON DATABASE SNOWFLAKE_SAMPLE_DATA TO ROLE transformer;
GRANT USAGE ON SCHEMA SNOWFLAKE_SAMPLE_DATA.TPCH_SF10 TO ROLE transformer;
GRANT SELECT ON ALL TABLES IN SCHEMA SNOWFLAKE_SAMPLE_DATA.TPCH_SF10 TO ROLE transformer;
```

6. Other grant permissions on the analytics database.

Sample Query:
```sql
GRANT USAGE ON DATABASE analytics TO ROLE transfomer;
GRANT MODIFY ON DATABASE analytics TO ROLE transfomer;
GRANT MONITOR ON DATABASE analytics TO ROLE transfomer;
GRANT CREATE SCHEMA ON DATABASE analytics TO ROLE transfomer;
```

7. Grant some warehouse permissions.

Sample Query:
```sql
GRANT OPERATE ON WAREHOUSE transforming TO ROLE transfomer;
GRANT USAGE ON WAREHOUSE transforming TO ROLE transfomer;
```

8. Grant role to yourself.

Sample Query:
```sql
GRANT ROLE transformer TO USER JARGOLASTIK;
```

9. Grant role to another developer.

Sample Query:
```sql
GRANT ROLE transformer TO USER JAREDSENPAI;
```

10. Grant role to service user account. This will be helpful when creating jobs in dbt Cloud.

Sample Query:
```sql
GRANT ROLE transformer TO USER dbt_cloud;
```

11. Verify permission by switching to the role and select tables.
