## Environment Variables

**Environment Variables** are commonly used in software development to trigger different behaviors based on the context in which code is being run. It is set outside of the main code and specifc logic is then built to read its value to decide of an outcome.

In dbt Cloud, environment variables are parameters that can be set at the project-level, the environment-level, the job-level, or at the personal developer level.

## How to use an environment variable

The variable name need to start with DBT_

and its value can be retrieved with `{{ env_var( 'DBT_MY_ENV' ) }}` 
or `{{ env_var( 'DBT_MY_ENV', '<default_value>' ) }}`

## Order of Precedence

In the case that an environment variable has been set up at different levels in dbt Cloud, the following order is then chosen.

<img width="584" height="333" alt="image" src="https://github.com/user-attachments/assets/8dffd885-2090-4b51-802c-a142f17f594a" />

## Setting Environment Variables

**At the Project/Env Level**

Go to **Orchestration** -> **Environment** -> **Environment variables**.

**At the Job Level**

You can find the env variable configuration inside the job settings.

**At the Developer Level**

Click **Your Name** -> **Your profile** -> **Credentials** -> **Project name**
