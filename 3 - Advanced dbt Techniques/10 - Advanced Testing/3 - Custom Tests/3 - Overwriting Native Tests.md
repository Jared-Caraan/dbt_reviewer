## Overwriting Native Tests

You can **overwrite any test that dbt ships** with. In fact, you can overwrite any macro that dbt utilizes!

**Why would you do this?**

You may want to test for not-null-ness only under certain circusmtances across your entire project, like when the `column_id` is not your test case, i.e., not equal to `00000`.
