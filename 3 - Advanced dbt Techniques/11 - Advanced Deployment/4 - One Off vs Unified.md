## One Off Jobs vs. Unified Jobs

One common pitfall in deploying dbt is having a large number of very specific jobs. Running all of your marketing models in one job, your sales models in a second, and your product models in a third might seem like a good way to ensure that you aren't using more compute resources than you need to.

But if there's overlap in the different sections of the DAG with these jobs and then you run the risk of rebuilding tables multiple times with very little benefit. It is recommended to start with your incremental job in the morning and then decide what needs to be built more than once a day.

There are multiple ways to build these selective runs. The first one is **tags**, tag models with the frequency in which they need to be built, such as hourly, 30 minutes, or twice a day. Then you can set up a dbt cloud job to run these models with their tags on the appropriate schedule.

The second one is **exposures**. Build out the models a particular exposure depends on. This allows you to keep a specific dashboard up-to-date.

The third one is **sources**. Build everything out from source data onward if a specific source is updated frequently.

The last one is **folder structure**. Build out a particular subdirectory in order to get all finance data, for example, up-to-date.

> [!TIP]
> Do not run one selected section of your DAG in a single command, and then in a separate command run a second section of your DAG. Instead, you can take one of two built in approaches, unions and intersections.

**Unioning** dbt command is denoted by a space such as `dbt build --select +fct_orders +fct_payments__pivoted`. This will run the upstream nodes of both of these models and check for shared parents so that they are only run once.

An **intersection** is denoted by a comma, such as `dbt build --select +fct_orders, +fct_payments__pivoted`. This will run only the shared parents between these two models.
