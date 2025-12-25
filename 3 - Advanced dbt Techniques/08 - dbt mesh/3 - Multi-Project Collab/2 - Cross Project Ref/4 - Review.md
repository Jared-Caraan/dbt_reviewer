Contracts, versions, and access levels all serve the purpose of helping data teams collaborate well even in larger, more complex projects. But even with these in place, there are still other problems introduced by large scale that are unsolved: it's hard for any contributor to have an intimate understanding of the entire dbt DAG, it's hard to find the right models to work on, and it's hard to empower teams to work autonomously.

An enterprise dbt Cloud account is required to create multiple dbt projects. 

To reference a model in another project, make sure to include a dependencies.yml in the downstream project listing the upstream project as a dependency.

```yaml
projects:
- name: name_of_project
```

To reference a model in the other project, use the cross project ref macro, like so:
`{{ ref(‘project_name’, ‘model_name’) }}`

Using a cross project ref macro enables multi-project lineage, which is viewable in the Explorer tab. Multi-project lineage enables you to switch between lineages graphs of your projects.

<img width="792" height="314" alt="image" src="https://github.com/user-attachments/assets/a0dcd339-0f6e-4376-8e6a-1c21a8f2821e" />
