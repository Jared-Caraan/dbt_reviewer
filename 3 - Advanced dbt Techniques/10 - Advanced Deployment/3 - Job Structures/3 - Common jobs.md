## Common deployment jobs

What kind of job should I build? How often should I run? How complex should my jobs be?

1. Standard job
    - build entire project
    - leverage incremental logic
    - typically daily
2. Full refresh job
    - build entire project
    - rebuild incremental models from scratch
    - typically weekly
3. Time sensitive job
    - build a subset of your DAG
    - helpful to refresh models for specific parts of the business
4. Fresh rebuild
    - requires dbt version 1.1+
    - check if sources is updated
    - if yes, build downstream models
