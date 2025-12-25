## Groups
- A group in dbt is a set of resources in your project owned by a person or a team: It’s a set of models that are all related to each other in some way. Each model can only belong to one group.

- Each group has an owner, either one person or a group of people.

Groups are configured like so:

```yaml
groups:
  - name: finance_group
    owner:
      name: Person’s Name
      email: TheirEmail@email.com
  - name: Marketing 
    owner:
      name: Marketing Group
      email: marketing@jaffle.com
```

## Access Modifiers
- Access modifiers determine which models can access (reference) a specific model. There are three levels of model access that can be granted.

- Private:
    - Can only be accessed by those in the same group
    - Upstream models that need to be further transformed before they’re ready for downstream consumption
- Protected:
    - Can only be accessed by those in the same project/package (by default, all models are ‘protected’. This means that other models in the same project can reference them.)
    - Also upstream models.
- Public:
    - Anyone can access
    - Will enable multi-project collaboration.
    - Ready for downstream consumption
    - Probably a marts model or a staging model referenced in other projects.

Access modifiers are configured like so:

```yaml
models:
    - name: model_name
         group: group_name
         access: access_modifer #public, private, or protected
```
