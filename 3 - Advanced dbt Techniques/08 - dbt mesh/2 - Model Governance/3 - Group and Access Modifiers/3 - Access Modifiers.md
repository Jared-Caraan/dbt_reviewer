## Access Modifiers
- Which models can access (reference) a specific model
- There are 3 different levels of model acces that can be granted
    - **public** - can be accessed by models in any group, package, or project
    - **protected** - can be accessed by models in same project or group
    - **private** - can only be accessed by models in same group
- All models default to **protected**

##

### Quick notes
1. Access modifiers are not meant to govern user access to the dbt platform, and it will not override users' access level to a project in the dbt platform.
2. Access modifiers do not automatically execute a grant statement, and you still maintain control on who can actually access the table in the data warehouse. This means that it is possible for you to declare a model to be a public model, but a downstream project team does not actually have access to that model in the data warehouse. What happens in this scenario is that the downstream model's ref will parse correctly in the dbt project, but the model built will fail.

##

### So, which models should have which access modifiers?

- If everyone's in the same project, there's functionally not really a difference between protected and public models.
- A **public** model or a **protected** models should be one that is guaranteed to be **ready for final use**.
- A **private** model should be one that you don't really want other people pulling from. For whatever reason, the data is a private implementation detail reserve for use only by the team represented by the group, and **there are probably downstream models better suited to be pulled by others**

##

### Apply Access Modifiers
- To assign **Access Modifiers** to a model, add the **access:** property to the model yaml file
- Indicate the level of access you want to assign this model
    - private / protected / public

```yaml
model
```
## Related Resources
- [Groups](https://docs.getdbt.com/docs/build/groups#:~:text=By%20default%2C%20all%20models%20within,its%20group%20can%20reference%20it.)
- [Access modifiers](https://docs.getdbt.com/docs/collaborate/govern/model-access#access-modifiers)
