## Understanding State

**dbt by design is idempotent and stateless _by default_**

**Idempotent:** When you execute a dbt build command multiple times with the same underlying data sources, you get the same results.

**Stateless:** Each dbt build command runs independently of the results of the previous build, i.e. the results of the previous build do not inform / impact future runs.

##

<img width="594" height="372" alt="image" src="https://github.com/user-attachments/assets/515df5dd-0b43-49d4-ac52-8ffb3206ee99" />

Each build has the same results and row count assuming that the green node, the source, has gone unchanged.

##

### State

dbt does store **"state"** - a detailed, point-in-time view of project resources (also referred to as nodes), database objects, and invocation results - in the form of its artifacts.

Concretely, dbt will store the following each time you execute dbt build:
- manifest.json - _state_ of the resource files (models, sources, tests, etc.) in your project
- run_results.json - _state of the results_ of a command that was run

##

### What if we _could_ leverage state?

What could we do if we were _aware_ of the previous command **results**?

What could we do if we were _aware_ of the models that we **modified** after the last command?

### What can we do with state?

Two common use cases:
1. Building only new or modified models
2. Troubleshooting failures in the DAG
Note: This becomes particularly more powerful when you are working on larger DAGs. We will look at simple 3-node DAGs for simplicity.

##

### Building only new of modified models

Let's say we opened a new branch I'm working on. Models A, B, and C and we just run `dbt run` and they all build successfully.

<img width="451" height="133" alt="image" src="https://github.com/user-attachments/assets/8ae7c17b-bde2-4b26-97de-05c71f97b571" />

Then, we modified model B. So the typical step would be to only run models B and C.

<img width="451" height="95" alt="image" src="https://github.com/user-attachments/assets/3f1d5c8c-20d5-426d-a367-fdb4094648a5" />

Alternatively, you can utilize the state in the command. This is a very simplified version of the command `dbt run --select state:modified+`. The `state:modified` will look at the previous run. See what was changed between our current state of our project and the prior version of the project when we ran it last. Compare those and just choose what was modified. The plus then, as we've seen in the past, we'll choose everything downstream of that.

<img width="443" height="87" alt="image" src="https://github.com/user-attachments/assets/1f9d4c69-f0bf-490f-88ad-4a82163cb16b" />

##

### Troubleshooting failures in the DAG

Let's say we opened a separate branch working on a different part of the DAG and it models A, B, and C. When we run `dbt run`, A builds successfully, B failed, and then model C skips.

<img width="455" height="105" alt="image" src="https://github.com/user-attachments/assets/68670789-f552-4438-a207-0b050077e095" />

So one thing we could do; very similar logic to before is `dbt run --select model_b+` and everything downstream. Again, as the DAG gets larger, that gets more cumbersome to write out. So what if there was a command that knew what failed last time and rebuilt from the point of failure.

<img width="449" height="85" alt="image" src="https://github.com/user-attachments/assets/7d010bfd-7cec-4631-a233-e8b7baaf2084" />

This is the `dbt retry` command. This allows you to automatically look at your previous execution of a command. And retry that command from the points of failure and of course not rerunning the models or resources that were successful.

<img width="451" height="101" alt="image" src="https://github.com/user-attachments/assets/e95514a0-011c-4785-88bd-6a497dd89542" />
