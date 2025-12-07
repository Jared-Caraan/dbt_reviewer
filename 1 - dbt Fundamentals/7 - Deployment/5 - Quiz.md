How do you indicate a deployment environment as a production environment?

a. Add a flag to the job execution settings.\
b. Select `production` in the deployment environment settings.\
c. Select `production` in the development environment settings.\
d. Enter a service account's credentials in the deployment environment settings.

Answer: b

##
What is the function of a job in dbt?

a. the execution of dbt commands in development environments\
b. the execution of dbt commands in deployment environments\
c. configure the settings for where code should be run in production.\
d. investigate the data assets in your production environment

Answer: b

##
Which one of the following are true about running your dbt project in production?

a. Running dbt in production should use a different repository than I used in development\
b. Running dbt in production requires the re-configuration of sources to refer to production data.\
c. Running dbt in production should use a different database schema than I used in development\
d. Running dbt in production only supports the `dbt run` command - it does not support `dbt test`

Answer: c

##
When does a dbt job run?

a. Every morning at 9 am, in the time zone of your choosing\
b. At whatever cadence you set up for the job\
c. When developing in the dbt studio and the command “dbt run” is entered in the command bar\
d. Only when you open a pull request

Answer: b

##
The following commands are configured for a production job in dbt.

dbt seed

dbt test --select source:*

dbt run

dbt test --exclude source:*

If any of the tests on sources fails, how will dbt handle the rest of the commands?

a. dbt will still execute dbt run AND dbt test --exclude source:* \
b. dbt will still execute dbt run BUT will not execute dbt test --exclude source:* \
c. dbt will still execute dbt test --exclude source:* BUT will not execute dbt run\
d. dbt will not execute any further commands

Answer: d
