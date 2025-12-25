## Direct Promotion

<img width="475" height="202" alt="image" src="https://github.com/user-attachments/assets/83eb3d49-51d4-491b-8ffd-a3ce4c342e68" />

The development workflow in a direct promotion set up is fairly straightforward. Developers will create new feature branches directly from the main branch with the latest version of the code base at the time that they branch. Developers will then make changes on that feature branch, test them locally, and when ready, they'll open a PR in their repo to merge those changes back into the main branch.

If using CI, this PR event may trigger some automated testing to ensure that those changes are of high quality before merging them in. After a colleague is able to review and approve the changes, which usually happens after a few rounds of discussion and revision, the code is then merged into the main branch. 

In the case of dbt projects, when that happens, the next scheduled job that pulls from the main branch after one of those features is merged in, will include those changes and those changes will be reflected in your production data platform.

This process will then repeat for as many features as you'd like to introduce.

**Possible Risk**

- If there are missed tests in the development phase or overlooked issues in the review process, you run the risk of merging bad code directly into production and causing a data outage in your platform.
