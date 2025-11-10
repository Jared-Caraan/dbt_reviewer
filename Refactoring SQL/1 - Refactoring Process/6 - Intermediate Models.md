## CTEs or Intermediate Models

**Continue to reorganize code**

1. Move the filter for `payment_status` found in the `customer_order_history` and `final` CTEs to the import CTE for payments, so we are working on a limited data set before our calculations and transformations.

2. Remove the filter on order_status - this doesn't actually filter out anything.

3. In `fct_customer_orders`, create a new CTE above the customer_order_history CTE. Call this CTE order_totals. From the payments table, get the order_id, payment_status, and the total amount of the order - the final result of this CTE should be at the order_id grain.
