## Grants

Grants are a great way that we can enable permissions for specific resources in our dbt project. Whether that's models, seeds, snapshots; we can ensure that our developers have the right access to those resources as they're created.

Two key components to creating our grants are the privilege and the grantees. Privileges are the specific permission sets that we are granting, and the grantees are the people or the roles that we are granting those permission sets to.

##

### Sample yaml

```yaml
seeds:
    - name: country_codes
      config:
          grants:
              select: ['transformer', 'role']
```

##

### What it looks like under the hood

<img width="1005" height="246" alt="image" src="https://github.com/user-attachments/assets/e3dea6e4-d032-4ea9-99b1-cc5f65f9e6b7" />

First is it checks all grants on the object, then it revokes privileges on unmentioned roles, then grants privileges on the roles.

**Related Resources**
- [Grants](https://docs.getdbt.com/reference/resource-configs/grants)
