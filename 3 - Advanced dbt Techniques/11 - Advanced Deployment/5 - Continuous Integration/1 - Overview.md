## Continuous Integration

It's a practice used in software engineering where you build in automated builds and test to your code base before you merge it into your deployment branch. It is really important for avoiding breaking things in production.

**Example CI**

<img width="400" height="314" alt="image" src="https://github.com/user-attachments/assets/e1cd913c-489c-48fc-b28c-67368a0efb45" />

The context of the image above is:
- **Main branch**
  - with a code base
  - a DAG that runs daily at 4:00 AM
  - Commands that run are `dbt run` and `dbt test`
- **Development branch**
  - Modified one model and added an additional model
  - DAG nodes are updated

Before you open a PR, it's a good practice to make sure that everything builds with `dbt run` and that everything passes tests with `dbt test` - these are all manual without CI.

But with CI, it would be much better if there's an automated process for that.

<img width="321" height="116" alt="image" src="https://github.com/user-attachments/assets/6fa69f38-c418-4e50-b1f5-15d49d3c2eed" />

So what can be done is set up a continuous integration environment where you have a job that doesn't run on schedule but runs on pull requests.

<img width="218" height="179" alt="image" src="https://github.com/user-attachments/assets/6f4dccbb-387a-47e1-90f2-2f6a8e8516b1" />

What it does is when a PR is opened, it's gonna run a set of commands on this code base in a PR schema separate from the development schema that is dedicated solely for this CI workflow. If the commands doesn't pass, the PR can't be merged.

##
**Challenging Case**

The challenging case is where you have not only six nodes, but hundreds or thousands of nodes. Every time you open a PR, it would build every node in your DAG. And then also with CI, every time you make a new commit to that PR, it is going to rebuild the whole DAG.

And so, this is where a new concept called **Slim CI** comes into play.

It's still gonna be configured to run on PRs. Except, we will tell dbt Cloud to look at the two code bases and identify what has changed and let's only build that and the things downstream from that.

From six nodes, dbt will only create three nodes which is a 50% improvement.

<img width="241" height="257" alt="image" src="https://github.com/user-attachments/assets/50c385fa-144d-42df-98f2-4915002be988" />

The nodes that will not be build will defer to the last production run where those are built.
