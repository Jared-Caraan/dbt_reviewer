## Coordinating Different Jobs

In this section, we will be covering how to define the different schedules for our jobs while avoiding conflicts between them.

In dbt Cloud, a job can only have one active run at a time, which means that if a second run is triggered while another one is still running, it'll be queued and triggered only after the initial run is finished.

But while runs of a given job born overlap, it is possible to have multiple runs, different jobs running at the same time.

And in that case, we want to avoid having multiple jobs running on the same models at the same time to prevent conflicts on the same database object.

### Simple Orchestration

Example: Incremental run from Monday to Saturday, and a full-refresh on Sunday.

**Incremental job**
1. Go to job settings.
2. Command is `dbt build`.
3. Configure to schedule it to run every 5 am except Sunday.

<img width="668" height="326" alt="image" src="https://github.com/user-attachments/assets/65861d1b-2e20-4f06-8ce5-5f53108c10f1" />

**Full-refresh job**
1. Go to job settings.
2. Command is `dbt build --full-refresh`
3. Configure to schedule it to run every 5 am on Sunday only.

<img width="707" height="462" alt="image" src="https://github.com/user-attachments/assets/1d6d6adb-d1af-4cc7-b2d7-b9c626f48fb8" />

### Complex Orchestration

Example: Subset of models that we want to run every 30 minutes with an overlap with the full-refresh.

<img width="728" height="172" alt="image" src="https://github.com/user-attachments/assets/2d73031a-d07b-43d1-bcd9-2316712aa310" />

To avoid any conflict and overlaps, a revision will be made to produce the orchestration below.

<img width="711" height="124" alt="image" src="https://github.com/user-attachments/assets/8ccf3658-b4e4-4c54-bb45-a911ff4caafd" />

Plan: Split the incremental agenda into two different jobs. One is running at every 30 mins. at 15 and 45-minute mark, Monday to Saturday. And then on Sunday, we'll run it before 5 AM and then after 8 AM.

**The every 30-minute job**

1. Go to job settings.
2. Command is `dbt build --select +fct_orders+`
3. Configure to schedule it to run every 15 and 45 minutes. Monday till Saturday.

<img width="688" height="325" alt="image" src="https://github.com/user-attachments/assets/f3281d65-a257-4230-a28e-cfc090afdb8c" />

Use CRON schedule for the minutes part.
<img width="508" height="392" alt="image" src="https://github.com/user-attachments/assets/44d999f6-bdf2-4425-a73e-9577b1b8c391" />

**The every 30-minute job on Sunday**

1. Go to job settings.
2. Command is `dbt build --select +fct_orders+`
3. Configure to schedule it only on Sunday. Then avoid the full-refresh schedule and start again at 8 am for every 15 and 45-minute mark. (Refer to the plan above).

Use CRON schedule to configure the schedule
<img width="506" height="352" alt="image" src="https://github.com/user-attachments/assets/6a0f2b0b-97bc-47e3-b970-2a52e2b6f79c" />

