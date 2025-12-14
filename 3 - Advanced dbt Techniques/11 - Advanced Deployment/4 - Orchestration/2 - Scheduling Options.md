## Scheduling Options

### Schedule

When you create a job, the schedule section is going to be activated by default. We can deactivate it if you don't want the run the job on a schedule.

<img width="765" height="365" alt="image" src="https://github.com/user-attachments/assets/87abcda3-41c9-489a-b9bf-4adb7401577f" />

The example above shows that the job runs on specific intervals - every 12 hrs UTC time on business days.

##
<img width="751" height="317" alt="image" src="https://github.com/user-attachments/assets/c5f4ebc7-1f6b-464c-a7a8-364920402eb2" />

The example above shows a more customized run time - the job will run at 2 AM, 6 AM, and 7 PM UTC time on business days.

##
**Cron**
To configure a cron job, you are expected to provide five different values.
<img width="336" height="151" alt="image" src="https://github.com/user-attachments/assets/860fd335-4e7c-48cf-8ee5-2d18fe7e3b16" />

For each of those values, we can provide different parameters.
<img width="231" height="169" alt="image" src="https://github.com/user-attachments/assets/ea855c8a-b4d3-481d-9e45-2b352700ccd0" />

If we provide a star, it means that this is going to run for every occurrence of the parameter. The other option is to use comma to provide a list of values - `2,6` means 2 and 6. Meanwhile, dash represents a range of values  - `2-6` means 2,3,4,5,6. The slash parameter means at _regular intervals_.

**Example**

<img width="336" height="126" alt="image" src="https://github.com/user-attachments/assets/87d4a9e9-a657-46fe-b6f7-b496d438e9a9" />

Translation: Runs every 30 minutes, between 6 AM and 11 PM UTC, every day, every month, from Monday to Friday.

### Web hooks

This is extremely useful for slim CI. This means that whenever a pull request is created in the Git provider, there will be a job automatically triggered in dbt Cloud, and get results of this job showing in the git provider.

We also have the abilitym if we use a custom branch to say that we only want to trigger a job when a PR is created to merge into a custom branch.

### API

An API can be called from a script locally, it can be called as part of a CI/CD steps in a git provider. To trigger this job, we just need to provide our account ID, job ID, and token. We can use either a service token or a user token to trigger this job. Using these information, you can trigger jobs on a third-party orchestrator.
