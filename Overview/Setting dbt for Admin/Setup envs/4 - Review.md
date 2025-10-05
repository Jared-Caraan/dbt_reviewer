## Set Up a Production Environment
- Deployment environments are used for running code on a schedule and development environments are used for developing code
- A production environment is a deployment environment where developers can run jobs
- Data teams use production environments to create a production deployment pipeline for testing and deploying to production
- dbt recommends creating a service account with a role that has access to read from raw data but not write
- The connection detail values for a production environment should always differ from the values in your development environment
## Schedule a Job
- dbt Cloud Administrators can configure when and how jobs run in a production environment
- Administrators can set up daily jobs and select the days, and intervals for those jobs
- Running a simple daily job is one way to quickly test your data platform connection
- The audit log will maintain a record of who scheduled a job, when it was scheduled, and the status of the job
## Set Up Folders by Data Maturity
- dbt Cloud Aministrators can create folder structures to optimize dbt Cloud projects
- The maturity model is one structure used by some teams
- You must create a new branch each time you create a new folder structure
- Staging folders are used to organize source conformed logic and store data before it's transformed
- Marts folders are used to organize business confirmed logic and combine staging models to roll up into key business concepts
- Use a file named .gitkeep for each folder to help Git recognize an empty directory
- Update the dbt_project.yml file and README file to align with the maturity model
- Commit changes to the folder structure with a descriptive message and a pull request
- Once the pull request has been reviewed, merge the pull request and make sure the changes are reflected in the code and in the dbt Cloud IDE
## Set Up Folders by Domain
- dbt Cloud Administrators can set folders up by domain
- Domains lay the groundwork for different teams to build future models
- Create a new branch each time you create a new folder structure
- Create team folders using folder names that apply to your business
Add a .gitkeep file to each folder
Update the dbt_project.yml file and README file to align with the model
Commit changes to the folder structure with a descriptive message and a pull request
Once the pull request has been reviewed, merge the pull request and make sure the changes are reflected in the code and in the dbt Cloud IDE
