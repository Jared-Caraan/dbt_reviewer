## Why is Documentation Important?

In analytics, good documentation allows users and developers to answer their own questions. Things like "what does this data mean?" or "how is this field calculated?"

The goal of documentation in dbt is to make your project and data understandable to everyone on your team. It's an essential part of creating a single source of truth for your data.

## dbt Documentation
dbt brings documentation right into your development workflow. In dbt, you create documentation in the same YAML files you're configuring your models and your tests.

Once you've documented your project, dbt can serve up a user friendly website and connect your data to dbt Catalog.

## Components

dbt automatically builds a visual map of your project. This map, known as the Directed Acyclic Graph (DAG), shows all the dependencies between your sources and models. This is incredibly powerful because dbt builds this lineage for you based on the `{{ ref( ) }}` and `{{ source( ) }}` macros you've used. You don't have to manually draw or update anything, so lineage is always accurate and up-to-date with your latest code. 

While the DAG shows the relationships, you still need to explain what your data means. This is done by adding descriptions directly into your YAML files. You can document your project at three different levels, providing a layer of detail for every resource. At the model level, you can write a high-level description for an entire table or view. "What is its purpose?", "What is the grain of the table?" These are good things to document. At the source level, you can document your raw source tables. At the column level, provide a description for each individual field. This is where you can explain complex calculations, define what specific values mean, or clarify what a column represents.
