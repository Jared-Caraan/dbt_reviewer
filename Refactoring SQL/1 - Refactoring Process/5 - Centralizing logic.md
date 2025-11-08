## Centralizing Logic in Staging Models

**Move 1:1 transformations to CTEs**
1. Ignoring the import CTEs, identify where the staging CTEs are. These CTEs don't conduct any joins - notate above this section of CTEs with a comment that says -- staging.

2. Identify where the marts CTEs are. These CTEs conduct joins - notate above this section of CTEs with a comment that says -- marts.

3. Remove any redundant CTEs that conduct the same transformations on the same data sets. Replace all references to any removed CTEs with the proper references.
