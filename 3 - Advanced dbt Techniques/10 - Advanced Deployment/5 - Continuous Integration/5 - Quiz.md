What is the primary benefit of implementing continuous integration (CI) in dbt Cloud?

a. Reducing database storage requirements.\
b. Automating code builds and tests to prevent errors before merging.\
c. Generating database documentation.\
d. Increasing the frequency of production deployments.

Answer: b

##
In dbt Cloud, what is the function of a CI job set up with “run on pull request”?

a. To automatically deploy changes to production.\
b. To trigger a job only when a pull request is merged.\
c. To run build and test processes in a separate PR schema when a pull request is opened.\
d. To schedule routine daily builds of the production database.

Answer: c

##
What distinguishes Slim CI from standard CI in dbt Cloud?

a. Slim CI runs builds only on modified nodes and their downstream dependencies.\
b. Slim CI requires more compute resources than standard CI.\
c. Slim CI runs builds on all nodes in the database, regardless of changes.\
d. Slim CI automates documentation updates.

Answer: a

##
Which command syntax is used in Slim CI to select only modified nodes and their downstream dependencies?

a. `dbt run`\
b. `state: modified +`\
c. `dbt test +`\
d. `dbt build`

Answer: b
