## 1 trunk / direct promotion

<img width="882" height="329" alt="image" src="https://github.com/user-attachments/assets/6f9b886c-62a6-4793-8740-bd055d5ff5ae" />

**promotion** approach involves the following:

- Developer branch off of the main branch.
- After developing, they open a pull / merge request.
- This kicks off a CI job that builds and tests the dbt code in a temporary PR schema.
- After code review and CI checks pass, the code can merged into main.

This approach is the recommended approach for most use-cases as it allows changes to code to be quickly moved to production, with confidence that they can be trusted.

## 2+ trunk / indirect promotion

<img width="948" height="430" alt="image" src="https://github.com/user-attachments/assets/f12d5912-4d5e-416f-b3ab-3fa39afa9503" />

The **2+ trunk / indirection promotion** approach involves the following:

- The code owner creates 1 or many qa branches off of main
- Developer branch off of the qa branch
- After developing, they open a pull / merge request against the qa branch
- This kicks off a CI job that builds and tests the dbt code in a temporary PR schema.
- After code review and CI checks pass, the code can merged into qa.
- The core owner then manages the merging of code from qa to the main branch through another CI process.

This approach can be helpful if your team wants to release changes in batches rather than immediately. This provides a middle branch/environment where user acceptance testing can be applied, though might slow down the time for getting new features into production.

**Resources**
- [Adopting CI/CD with dbt Cloud](https://www.getdbt.com/blog/adopting-ci-cd-with-dbt-cloud/)
