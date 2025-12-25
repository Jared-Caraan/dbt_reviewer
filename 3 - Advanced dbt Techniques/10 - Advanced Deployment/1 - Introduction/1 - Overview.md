## Overview

### Environments

<img width="512" height="436" alt="image" src="https://github.com/user-attachments/assets/509e65a1-06a7-46f1-8216-2ff5383c351b" />

It talks about:
- What version of dbt should I use?
- What branch should I pull from?
- Where do I want to build data?

These are the three things that you configure on an environment level.
<hr>

Getting a little more nuanced here, we have two types of environments that you'll see in dbt cloud - development and deployment.

<img width="1015" height="382" alt="image" src="https://github.com/user-attachments/assets/9698b281-7ffe-4291-b523-9cdd60f49c62" />

**Development**

For development, you only have one development environment for a single dbt Cloud project. And this allows all developers to inherit the same dbt version that you want everyone developing on, however allows them to check out different branches and write to different, development schemas.

In development, you can set the version that you want dbt to run for your development environment, likely the latest version.

And then for each developer, they can jump into their profile setting and set their development schema, whether that's like _dbt_kcoapman_, _dbt_jsmith_, whatever it might be.

And then when they actually get into the ide, that's when they can toggle into the branch that they need.

**Deployment**

On the contrary, deployment environments, you can have as many as you want or need, and then you configure all three of these settings at the environment level.

Usually the dbt deployment version matches the development version. Typically, the branch that deployment environment uses is the `main` branch or `master` branch.

**Actual Example**

<img width="660" height="243" alt="image" src="https://github.com/user-attachments/assets/ffce8f87-1a00-479d-b048-b0a8390a5406" />

### Jobs

Within a deployment environment, you also have jobs. And so a job is essentially a sequence of dbt commands that you want to run on a schedule or trigger through some other means.

It can also be triggered externally through an API call.

**Example**

<img width="671" height="233" alt="image" src="https://github.com/user-attachments/assets/7dc3d839-c4ba-46ba-af79-b80c778b0e69" />

### Run Results

Once you have some jobs running, each job will produce what are called run results. This will show you the results for each of the commands that you decided to run. And you can even set up notifications for when things pass or fail. There's a lot of granularity and control there for where you want notifications to go, whether it's email or whether it is Slack.

Let's say it's been a couple weeks. I have my week one results. I have my week two results, and I can click into those and actually see what passed, what failed, what was successful, how long things took, and a lot of other things for my daily job.
