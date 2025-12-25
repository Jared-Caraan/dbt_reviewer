## Orchestration

In dbt Cloud context, orchestration refers to how and when the different jobs we have created get triggered to provide data to end users.

dbt Cloud provides three different way to automatically trigger jobs:

1. on a schedule - relates to time
2. via webhooks - trigger a job when a PR is created in Github, Gitlab, or Azure DevOps
3. via the dbt Cloud API

On top of triggering jobs, dbt Cloud also stores information for each run that has been executed independent from the way it was triggered.

**Information stored about jobs**
- status of a run
- run logs and debug logs
- artifacts
