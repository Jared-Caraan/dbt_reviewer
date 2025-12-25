## dbt Mesh

**dbt Mesh** is a really great framework that helps organizations scale their teams and data assets effectively by promoting model governance best practices and by breaking projects down into manageable sections using a multi-project structure. 

##

### Monolithic data structure vs dbt Mesh

In a monolithic project architecture, your team will interact with single dbt project. This approach is perfectly fine when the dbt project is relatively small, or when the same data team members are working to support many different functions at the same time.

However, as the project and the data team scales, your file list and DAG can look like this:

<img width="598" height="300" alt="image" src="https://github.com/user-attachments/assets/ee48e951-eb48-4970-bd6a-db1b42f226c6" />

And problems can manifest in different ways.

This is when you should consider adopting dbt Mesh. dbt Mesh is a pattern that enables domain level ownership of your data assets without creating silos. This is made possible through a combination of governance and collaboration features that enable teams to ship with velocity and confidence at scale.

##

### Why adopt a dbt Mesh pattern

Enable domain level ownership of data - without compromising governance

| Domain teams get: | Central data teams get |
| --- | --- |
| <ul><li>autonomy to ship data products faster</li><li>ability to share with and reference from other teams</li><li>confidence that nothing breaks unexpectedly</li></ul> | <ul><li>visibility into the full lineage of transformations</li><li>running in a single platform (dbt)</li><li>without acting as a bottleneck for every domain team</li></ul> |

##

### Manage interfaces with model governance
- Every model can have a **contract** that define guarantees around data shape.
- Models can have **private** or **public access levels**, as well as be **grouped**. Public models can be reused across projects.
- When a model's contract changes in a way that's backwards incompatible, it should be reflected with new a **version**.

<img width="725" height="372" alt="image" src="https://github.com/user-attachments/assets/3e04415d-4e6a-43e9-8f72-edc59f1e0076" />

##

### Discover assets and collaborate across multiple projects
- As a model producer: Share **public models** for use by others in the organization.
- As a model consumer: Reference models from another team's project, just by writing ref. No need to share source code or surface any additional complexity.

<img width="1144" height="385" alt="image" src="https://github.com/user-attachments/assets/0d23f4fb-44a5-4769-a577-0ed812dbfbc9" />
