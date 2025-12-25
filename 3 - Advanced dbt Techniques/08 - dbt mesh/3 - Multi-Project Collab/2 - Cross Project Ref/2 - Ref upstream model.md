## Referencing an upstream model in your downstream project

In order to be able to add project dependencies so we can reference models from other projects in our dbt account, we need to make sure the models we want to reference are public.

We also need to make sure that we have had at least one successful run in our production job upstream after the models have been defined as public models.

Lastly, we also need to make sure the name of each project in our account is unique. Again, just a reminder that the project name here is the name that is defined in your `dbt_project.yml` and not what is written in the dbt platform.
