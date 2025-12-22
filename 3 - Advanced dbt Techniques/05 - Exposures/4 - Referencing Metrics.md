## Referencing Metrics with Exposures

Below is a sample semantic file:

**sem_fct_orders.yml**

<img width="642" height="718" alt="image" src="https://github.com/user-attachments/assets/26d75fa8-61fa-431e-8a9c-e0f9b40054d1" />

A command to query metrics - `dbt sl query --metrics order_total`.

So, we use these three metrics in a downstream dashboard, so we will reference them in our orders exposure.
