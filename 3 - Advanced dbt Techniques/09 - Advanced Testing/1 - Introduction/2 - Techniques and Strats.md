## Testing Techniques

1. **interactive / ad hoc queries** - Example query to test the primary key in a statement tab.

    <details>
    <summary>Sample ad hoc query</summary>
    
    ```sql
    select customer_id
    from analytics.customers
    group by customer_id
    having count(*) > 1
    ```
    </details>

2. **Standalone saved query** - Example of a standalone test. Add the previous statement to a sql file and it will run when you want to check the results.

3. **Expected results** - Example of a standalone test with expected results. This adds contet and information to your tests.

    <details>
    <summary>Sample expected results query</summary>

    **assert_unique_customers_customer_id.sql**
    ```sql
    # only surface # of failures
    select
      count(*) as failures
    from (
      select
        customer_id as unique_field,
        count(*) as n_records
      from analytics.customers
      group by customer_id
      having count(*) > 1
    ) dbt_internal_test
    ```
    </details>

## Testing Strategies
**Test on a Schedule** \
The ultimate goal is a standalone test w/ expected results running automatically on a schedule.

**Take Action!** \
Failures should be fixed immediately or silenced. If there is too much noise, tests become meaningless.

## What makes a good test?
**Automated** - low effort / repeatable \
**Fast** - if testing takes too long, no one will do it \
**Reliable** - believe them when they say something doesn't work \
**Informative** - leaves you clues about what to fix based on the error \
**Focused** - every test should validate one assumption
