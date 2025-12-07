What is the key benefit of using incremental models in dbt?

a. Processes entire data sets on every run.\
b. Quickest materialization to reference.\
c. Reduces build time by only processing new records.\
d. No configuration required.

Answer: c

##
Which of the following is not one of the three required configurations for incremental models?

a. A materialized='incremental' setting in the model file.\
b. A unique key defined for the table.\
c. An is_incremental() conditional block.\
d. An incremental_strategy defined in the configuration block.

Answer: b

##
What is a potential strategy for handling late-arriving data in incremental models?

a. Adding a secondary model to handle late-arriving data exclusively.\
b. Including logic to rebuild the entire table every run, even if it’s incremental.\
c. Creating conditional logic in the is_incremental() block to update rows for overlapping time periods.\
d. Partitioning data by year to ignore late-arriving records.\

Answer: c
