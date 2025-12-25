## What's job completion triggering?

### Cross-Project Orchestration

<img width="1090" height="383" alt="image" src="https://github.com/user-attachments/assets/85bc446b-934e-4652-b320-0d021cc4fb58" />

**Effortlessly handle complex, cross-team orchestration**
- Create workflows that build models _across_ the organization, improving automation and autonomy while reducing unnecessary model execution.
- **Declarative Scheduling**: Cloud's scheduler would trigger models / project subsets to run.

##

### Setting up a job to trigger on completion

1. **Orchestration** -> **Jobs**
2. Fill-up the necessary details
    - Job name -  Daily Finance Job
    - Environment - Production
    - Tick **Generate docs on run**
    - Command is `dbt build`
3. Activate the toggle **Run when another job finishes** then choose the upstream project that it should be dependent on.
4. Then choose the job name of the upstream project, and choose the **Success** status.
5. Hit Save.

##

What it looks like when the upstream job is done as a prerequisite.

<img width="753" height="471" alt="image" src="https://github.com/user-attachments/assets/600a6726-f460-4fbe-81ce-bd551b133d51" />
