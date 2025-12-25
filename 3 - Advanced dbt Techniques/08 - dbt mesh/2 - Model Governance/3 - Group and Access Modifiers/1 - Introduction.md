## Introduction to Model Groups and Access Modifiers

As projects grow, the DAGs grow with them. It can be much more difficult to navigate such large monolithic projects. This can become even more challenging when you are trying to identify which model you should be using for your specific work. Groups and access modifiers can help you navigate this complexity by specifying who can reference specific models from within both centralized and decentralized project structures.

##

### Groups & Access Modifiers Defined

- **Groups:** Nodes that are related to one another and owned by a specific team - a way for a business to organize models based on ownership (e.g. finance, marketing, employee, data, etc.) rather than stage of development (e.g. staging, intermediate, etc.)
- **Access Modifiers:** Which **models** can access (reference) a specific model

##

### Creating Groups
- **Groups** will be designated within a yaml file nested under a **groups:** key
- Under the **groups:** key, you will be able to name the group and add owner information
    - At least name or email is required - additional properties are allowed (slack, github, etc.)
- **Groups** can be defined in your models yaml file or in its own dedicated yaml file.

```yaml
groups:
    - name: Finance
      owner:
          name: Person's Name
          email: TheirEmail@email.com
    - name: Marketing
      owner:
          name: Marketing Group
          email: marketing@jaffle.com
```

##

### Assigning Groups

- To assign **Groups** to a model, add the **group:** property to the model yaml file
- Each model can _only_ belong to one group

```yaml
models:
    - name: stg_customers
      config:
          group: marketing
    - name: stg_orders
      config:
          group: finance
    - name: fct_orders
      config:
          group: finance
```
