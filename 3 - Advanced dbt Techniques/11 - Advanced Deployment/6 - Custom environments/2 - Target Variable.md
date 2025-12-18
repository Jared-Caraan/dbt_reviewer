## What is the target variable in dbt?

**Target** is a variable accessible in any Jinja macro or code block that contains information about the active connection to your warehouse, like the type of warehouse dbt is connecting to, the credentials used to connect to the warehouse, etc.

**target.name**
dbt Cloud gives us the ability to configure what value will be stored in `target.name`. The target name is configured for each developer and for each job, and can be accessed in a Jinja block of any dbt code by reading the variable target.name

At the job level, the target name can be configured by navigating to the job settings in **Orchestration** --> **Jobs**. As mentioned, each developer also has a target name defined for their development environment in the dbt Cloud IDE. It can be configured by navigating to **_Your Name_** -> **Your profile** -> **Credentials**
