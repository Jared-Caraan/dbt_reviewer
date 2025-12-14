## Scheduling options in dbt Cloud

There are 3 major ways to trigger a job in dbt Cloud:

- **Schedule** - you can configure a schedule for a job to run directly within the dbt Cloud UI. You can set this through a user friendly UI or in a more customizable way with cron syntax.
- **Webhook** - you can trigger a job with a webhook from your git provider. Currently dbt Cloud supports GitHub, Gitlab, and Azure Devops.
- **API Call** - If you are using an external orchestrator such as Airflow, you can call dbt Cloud directly to initiate an job through an API call. This will require either a service token or user token.

## Reviewing past runs

When a run completes, you can view several things about that particular run

- Model timing
- Run logs
- Artifacts including json files and compiled SQL
- Documentation (if configured)
- Source freshness (if configured)

## Coordinating different jobs

There are cases where you may have jobs that run concurrently on shared models. In these cases, you likely want to account for those conflicts. This can be difficult to achieve with the user friendly scheduling options. To avoid these conflict, consider using cron syntax or API calls to avoid the overlapping jobs.

## Related Resources
- [dbt guides: Airflow and dbt Cloud](https://learn.getdbt.com/learn/course/advanced-deployment/orchestration-35-min/what-is-orchestration?page=8#:~:text=dbt%20guides%3A%20Airflow%20and%20dbt%20Cloud)
