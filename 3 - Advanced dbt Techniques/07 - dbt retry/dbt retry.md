## Rebuild from the point of failure with dbt retry

**dbt retry** is a command to re-execute the last dbt command from the point of failure.

So let's say we have a DAG like this:

<img width="498" height="304" alt="image" src="https://github.com/user-attachments/assets/685853f2-f6bc-49ba-9a7d-55a43ff09dc2" />

The first time we tried to run this, let's say we did a `dbt run`, our first two staging models in green, those were successful, and then our region staging model failed. Because our region's model failed, `dim_customers` will get skipped.

<img width="503" height="288" alt="image" src="https://github.com/user-attachments/assets/8abbbcd1-de0e-4593-b376-9e0e8789b8ca" />

And so what `dbt retry` allows you to do is just rebuild whatever dbt failed last time in those things downstream, continue trying to build the rest of your DAG.

<img width="503" height="325" alt="image" src="https://github.com/user-attachments/assets/3f07bf72-9381-43d8-a06a-7af8ab1ed98d" />

##

### Why `dbt retry`?
- `dbt retry` abstracts away the cumbersome step trying to build a new command to just run the parts of the DAG that failed
- This is helpful in:
    - Development while iterating on the DAG
    - In production when re-running a job after a failure and pushing a fix

##

### dbt retry
- The `run_results.json` is used to inform what was pass/failed
- The same `selectors` of the prior command will be passed through

`dbt retry` can be applied to the following dbt commands:
- `build`
- `compile`
- `clone`
- `docs generate`
- `seed`
- `snapshot`
- `test`
- `run`
- `run-operation`
