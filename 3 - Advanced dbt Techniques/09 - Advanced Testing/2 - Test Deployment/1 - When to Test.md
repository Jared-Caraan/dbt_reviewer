## Testing with Intention: When to Test?

### When to Test?
- Test **in development** to ensure what you're building doesn't break pre-existing assertions and satisfies your requirements.
- Run tests automatically as an approval / **CI check** in your PR.
- Do you want the outcome of your tests to prevent a pipeline from running if they discover an error? If so, test **in production** and add notifications for failures.

### Run Tests
**Manual**
- When you first run a project
- During development

**Automated**
- When you run a dbt on a schedule (deployment jobs)
- When you want to merge your code (git CI checks)

### Scenarios
**#1: Test while adding or modifying dbt code**

<img width="662" height="185" alt="image" src="https://github.com/user-attachments/assets/17b7c33e-0300-492c-b996-cae7d2d54d64" />

**#2: Test while deploying your data to production**

<img width="662" height="228" alt="image" src="https://github.com/user-attachments/assets/04fd4802-e227-413c-b4d5-273f475b7c83" />

**#3: Test while opening pull requests (CI)**

<img width="673" height="234" alt="image" src="https://github.com/user-attachments/assets/edae12f5-51f0-4c00-b981-4d8b5ded27b8" />

**#4: Test in QA branch before your dbt code reaches main**

<img width="669" height="378" alt="image" src="https://github.com/user-attachments/assets/8b26202b-b027-45dc-8bdc-e700abca7e56" />

### Quick Refresher
**What is dbt build anyway?**

- run models
- test tests
- snapshot snapshots
- seed seeds

**In DAG order**, for selected resources or an entire project.
