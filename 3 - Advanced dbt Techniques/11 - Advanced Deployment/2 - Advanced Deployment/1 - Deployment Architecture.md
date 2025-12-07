## Introduction to Deployment Architectures

Deployment architecture refers to the way you organize the automatic execution of your dbt project into different locations in your data platform. This allows us to run and test our dbt project in various stages of development between the time that we've actually written code, all the way through deploying to our production data platform.

Using dbt Cloud environments and dbt Cloud jobs, we can create pipelines that ensure data quality and completeness, and deliver our data artifacts to our customers in a timely manner.

For the purpose of the section, we're going to assume that we have one single data warehouse and a single dbt project that we'd like to deploy. And dbt Cloud is gonna be our deployment strategy.

**Direct Promotion - One Trunk**

<img width="491" height="210" alt="image" src="https://github.com/user-attachments/assets/3c0092ec-c984-470a-a36e-7b90d540e80c" />

This is a scenario in which feature branches in your repository are merged directly into the main branch of your repository.

**Indirect Promotion - Many Trunks**

<img width="443" height="259" alt="image" src="https://github.com/user-attachments/assets/92a6bbb1-2ce8-4760-85f7-857ea109d878" />

The second, slightly more complex git promotion cycle, is indirect promotion or many trunk promotion. In this scenario, feature branches are first merged into an intermediate branch for additional testing before finally promoting that code into your production environment that gets deployed to your data platform.
