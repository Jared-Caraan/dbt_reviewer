## Exposures Syntax

### Configuring Exposures

Dbt exposures let you define and describe how your models are used. So how do we configure exposures?

Exposures are defined in YAML files under the exposures key. They can be in your source YAML file, or a model YAML file, or in a completely separate exposures YAML file. Just make sure that this file is nested somewhere in the model's directory.

<details>
<summary>Sample Exposure</summary>

```yaml
exposures:
  - name: weekly_jaffle_metrics
    label: Jaffles by the Week
    type: dashboard
    maturity: high
    url: https://bi.tool/dashboards/1
    description: Did someone say "exponential growth"?

    depends_on:
        - ref('dim_jaffles')

    owner:
        name: Michelle Baird
        email: Michelle@jaffleshop.com
```
</details>

The example exposure is named `weekly_jaffle_metrics` but it's labeled `Jaffles by the Week`. These labels are mostly for organizational purposes on the docs site or in Explorer.

Exposures have different types: **Dashboard**, **Notebook**, **Analysis**, **ML**, or **Application**. We also have this maturity parameter, which will let you know if the maturity of an exposure is **low**, **medium**, or **high**. The higher it is, the more well-established and trusted the dashboard is.

The owner parameter lets you know who owns this exposure. Who do you check in with if you have any questions or if something's wrong? It is required to put either the name of the owner or their email address here.

**Resources**
- [Exposures](https://docs.getdbt.com/docs/build/exposures)
