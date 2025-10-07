# Analytics Development LifeCycle
## The Framework
1. **Plan** - This is the phase where the team scope up the work, clarify priorities, and get shared expectations. It's all about intentionality where you work on the right things at the right time.
2. **Development** - This is the phase where you write code to transform raw data into something useful.
3. **Testing** - Along with development phase is the testing phase. In DBT, this could be checking nulls or writing custom tests to validate unique business logic. Testing ensures that your data is trustworthy before it reaches production, and they can help your team catches issues early on.
4. **Deploy** - This is where changes go live.
5. **Operate** - Once the code goes live, it needs to run consistently. The operate phase is where you manage production pipelines. In DBT, this means scheduling jobs, monitoring run times, and setting up alerts for when things go wrong. Operations are about reliability.
6. **Observe** - After pipelines run, we observe them. This is about tracking what happened. Observability tools like DBT's run history, logs, test alerts, and more helps, data teams stay proactive and avoid surprises.
7. **Discover** - This is where data consumers explore models, understand the logic, and find answers. Thanks to DBT's documentation, metadata, and lineage, people can trace metrics back to their source and build trust in the data. This phase is especially powerful when combined with tools like DBT catalog.
8. **Analyze** - This might happen in a BI tool or in a notebook or the DBT semantic layer. This is where your work delivers value. And often the questions that surface during analysis, lead you right back to planning.
