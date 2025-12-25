## Groups

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
