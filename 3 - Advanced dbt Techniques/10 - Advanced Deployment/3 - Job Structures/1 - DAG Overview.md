## DAG Overview

One of the more powerful features of DBT is its ability to render a DAG. In order to see to your DAG for your project, click on **Documentation** and then look for a lineage graph. You can also specifically choose a model, then preview the DAG under Lineage.

**Example DAG**

<img width="1837" height="550" alt="image" src="https://github.com/user-attachments/assets/acc51ba2-d472-4ef2-a3ca-4a0f4c122704" />

Each of these rectangles represents a node. Green nodes are sources, blue nodes are our seeds, snapshots, models, tests, and analyses. And then the orange node represents an exposure. The lines between each node represents our dependencies, so our dependencies are created using the source function, the ref function.

<img width="1821" height="565" alt="image" src="https://github.com/user-attachments/assets/c8c9d999-f07b-4675-8759-5ba0acbf160f" />

When a node is clicked, it turns purple as well as its dependencies. This is to show you the parents it has and the children it has.

<img width="364" height="364" alt="image" src="https://github.com/user-attachments/assets/9f8335a9-7cdc-4b49-9453-9c0ba3691120" />

If a node is right-clicked, several options will appear.

<img width="1707" height="279" alt="image" src="https://github.com/user-attachments/assets/b7a5df78-e1b6-478e-af7f-7e9fb248c4ab" />

If "refocus on the node" is chosen, it will just show the node that is selected. 

<img width="1569" height="776" alt="image" src="https://github.com/user-attachments/assets/acaa3173-e62f-4db2-b748-f3b03c08022e" />

You can select/exclude models by putting its name on the fields below. You can also configure if you want to view its upstream or downstream models. This can be used to practice what commands to use in your dbt jobs in order to avoid redundant model runs.
