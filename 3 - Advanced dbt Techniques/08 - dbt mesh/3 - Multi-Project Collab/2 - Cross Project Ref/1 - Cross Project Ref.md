## How to reference models across projects

- Once you **set up your dependencies.yml files**, if you know which model they want to use from the upstream project, **the relation name** is all you need to resolve references.
- A big goal is **scaling collaboration** which requires us to improve **model discoverability**.
- dbt Explorer will help us with this!

The main difference of `packages.yml` file with `dependencies.yml` file is that the `packages.yml` file only supports installing other dbt projects as packages, while the `dependencies.yml` file also supports declaring another dbt project as a dependency, which is the behavior that we want here.

You can choose to maintain both files or consolidate them into a single `dependencies.yml` file. Next, you'll use a cross-project ref macro to reference the model from another project, in this case, our core platform project.

##

**dependencies.yml**

```yaml
projects:
    - name: core_platform
```

You declare the project dependencies in the `dependencies.yml` file which is located at the root of your project directory. The entry to this file is basically the upstream project's name.

It's really important to note that the project name must be the name that is declared in the upstream project's `dbt_project.yml` file and not the project's name in the dbt platform.

##

Syntax: `{{ ref('project_name', 'model_name') }}`

Once the project is defined in the `dependencies.yml` file, you are ready to use the cross-project ref macro.
