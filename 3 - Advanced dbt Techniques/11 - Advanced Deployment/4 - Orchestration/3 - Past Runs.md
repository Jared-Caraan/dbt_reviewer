## Review Past Runs

There are a few different ways to look at previous runs of our jobs.

1. Run history - it will preview jobs runs and can be filtered out by environment and status.
2. Via jobs - At a specific job, it will show all the previous runs for that job.

**Information on the Runs**
1. Status
2. Job name
3. Environment of the job
4. Run Triggered
5. Run Duration
6. Run Completion
7. Run Steps
    - In each of the step, we are able to have a look at different logs.
        - Console Logs - summarized details
        - Debug logs - truncated by defaut, but can view in full if downloaded
8. Model Timing - it is extremely useful when you want to identify which models are taking the longest in your run to make sure that you optimize those.
9. Artifacts - different files generated during the run.
    - The files show the DDLs and queries used during the model run
10. View Documentation - this only shows up if you tick the option `Generate docs on run`.
    - Lineage
    - Tables
11. View Sources - this only shows up if you tick the option `Run source freshness`.
    -  Provide us a quick snapshot of how the data looked from a source freshnesss point of view, so that when we run our job, we can see the sources freshness was correct as per our requirements.

<img width="1479" height="746" alt="image" src="https://github.com/user-attachments/assets/942eabe1-43bd-4198-99aa-8c6e8d11e683" />
