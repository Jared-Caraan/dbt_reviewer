## Storing Test Failures in the Database

**How to debug test failures**
- Run dbt test
- Test fails
- View logs -> Click into debug logs
- Find the SQL that was run
- Copy the correct part of it
- Paste into a statement tab
- Preview data to see what rows failed

**Is there a better way?**
Enter the --store-failures flag
