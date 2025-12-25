What problem are model versions meant to solve?

a.
With model versions, every team can have their own slightly different version of a model that suits their particular needs.\
b.
With model versions, breaking changes to upstream models no longer result in immediate run failure. Model versions provide a migration pathway as breaking changes are made.\
c.
With model versions, you can get away with ignoring your model contracts by creating a different version of the model.

Answer: b

##
There are two versions of a model in a dbt project: and old version and a new version. What version of a model will dbt default to if a specific model version is not defined in a ref function?

a. Neither. If you don’t specify which model to default to you’ll get an error message.\
b. Both will run.\
c. The old version of the model.\
d. The new version of the model.

Answer: d
