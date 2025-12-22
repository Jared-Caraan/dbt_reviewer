## Referencing Metrics with Exposures

Below is a sample semantic file:

**sem_fct_orders.yml**

<img width="642" height="718" alt="image" src="https://github.com/user-attachments/assets/26d75fa8-61fa-431e-8a9c-e0f9b40054d1" />

A command to query metrics - `dbt sl query --metrics order_total`.

So, we use these three metrics in a downstream dashboard, so we will reference them in our orders exposure.

**jaffle_exposures.yml**

```yaml
exposures:
  - name: orders_data
    label: orders_data
    type: notebook
    maturity: high
    url: https://app.hex.tech/fishtown/app/7aebeaf4-8fc4-4894-8f06-86c9ba8e8a62/latest?
    depends_on:
      - ref('fct_orders')
      - metric('order_total')
      - metric('large_orders')
      - metric('cumulative_order_amount_mtd')
    owner:
      name: John Doe
      email: data@jaffleshop.com
```
