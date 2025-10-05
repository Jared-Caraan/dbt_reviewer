## DBT Dashboard
- The homepage of the dbt website

## DBT Project (Select a Project)
- Lists all the projects tied to the account and lets you pick a specific project.

## DBT Catalog
- The place to store metadata of the project.

#### Lineage
- Track the data lineage of the models
- Resource type could be any of the ff:
  - Sources (SRC)
  - Models (MDL)
  - Exposures (EXP)
  - Metrics (MET)
  - Project (PRJ)
  - Semantics (SEM)

#### Model Overview
- Description of the model
- Columns of the model
  - Transformation of the column per stage
- Performance
  - Build Time, Build Count, Test Results, Consumption Queries
- Last run status
- Test results
- Upstream sources
- Model-level lineage
- Metadata
  - Project, Owner, Tags, etc.
  - Relationships

## DBT Orchestration

#### Environments
<p> A way in dbt to separate jobs and execution in development and production. Two main types of env: **DEV** and **PROD**. Only one **DEV** environment exists on a project. The other types of environments are deployment environments and you can have as many as you want on a project. These deployment environments are often linked to a branch. </p>
Functionalities:
- Scheduled jobs
- Job runs
- Models

## DBT Studio
<p>This is the workspace area where the development occurs.</p>
Functionalities:
- File explorer
  - dbt_packages and target folder doesn't show up on the git repository unlike any other folder.
- Version Control
- Coding area
- Model lineage
- Preview data model (limit to 500 records)
- Compile (transform non-SQL script to SQL e.g. sources)
- Build (actually build a data object)
- Run status

## Things to note
- Always work on a separate and personal schema when working on development environment.
- ``dbt build`` runs the model including its associated tests.
- ``description:`` in yaml file documents the columns which can be seen on **dbt catalog**.
