## Model Versions

**Thought Experiment**

You have a rather large dbt Cloud project (1000+ models). There are several teams working inside of this project, referencing models built by one another, and becoming dependent on the data. To avoid beraking changes being made to upstream models, you've implemented contracts!
- What if I need to make a change to a model that could affect downstream models (e.g. convert a data_type)?

##

When model contracts are in place, we have a mechanism to prevent a developer from accidentally implementing a breaking change. However, considering that changes over time will inevitably become necessary, we need to make an update that results in a planned breaking change.

A model version is, like the name suggests, a different version of a model. It's a separate SQL file that contains an edited version of an existing model. This is where model versions can help us implement a transition period. We may need to ultimately rename, remove, or change the data type for a column.

If we implement model versions, we can test pre-release changes in production in downstream systems. We can also bump the latest version to be used as the canonical source of truth. And finally, we can offer a migration window off of the old version.

Versioning your models will ensure that if you are making a breaking change, you let everyone know and give people time to adjust. This will add a layer of friction to your workflow. But it's a good friction. It will force communication with stakeholders while still giving you the flexibility to implement needed updates and improvements to your models.

Model versions will require a healthy amount of human judgement to decide when to increment a version, but unlike contracts, won't require ongoing human judgement to be enforced.

## Related Resources
- [Model Versions](https://docs.getdbt.com/docs/mesh/govern/model-versions)
