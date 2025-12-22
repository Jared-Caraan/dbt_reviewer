## Configuring Exposures

**fct_orders.sql**

```sql
with orders as  (
    select * from {{ ref ('stg_jaffle_shop__orders' )}}
),

payments as (
    select * from {{ ref ('stg_stripe__payments') }}
),

order_payments as (
    select
        order_id,
        sum (case when status = 'success' then amount end) as amount

    from payments
    group by 1
),

 final as (

    select
        orders.order_id,
        orders.customer_id,
        orders.order_date,
        coalesce (order_payments.amount, 0) as amount

    from orders
    left join order_payments using (order_id)
)

select * from final
```

So we want to create an exposure that will bring our dbt project and our dashboard together.

##
Let's start off by creating an `exposures` folder under the `models` folder.

Then create a file named `jaffle_exposures.yml`.

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
    owner:
      name: John Doe
      email: data@jaffleshop.com
```

You'll also see the lineage graph being updated.

<img width="1295" height="349" alt="image" src="https://github.com/user-attachments/assets/dea4fcf7-ad18-4b6b-a0a9-17274fe4695d" />

##

I want to make sure the data my exposures are using is up to date, so I have a really great command I can use. And that command is `dbt run -s +exposure:orders_data`. And what this command will do is it will run everything upstream of my exposure named orders data.

If I wanted to run everyting upstream of every exposure, I'd use this command instead - `dbt run -s +exposure:*`
