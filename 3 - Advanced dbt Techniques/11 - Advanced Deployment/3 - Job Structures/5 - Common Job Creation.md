## Common job creation

**Creating a Standard job**

1. **Create job** -> **Deploy job**
2. Fill out the configurations necessary to set up a deployment type environment.
    - Job name - Production
    - Environment - Choose production
    - It is recommended to tick **Generate docs on run**
    - Add your commands on the execution settings (e.g. `dbt build`)
    - Configure your desired schedule for your job (e.g. 12 hrs everyday at midnight)
    - On **Advanced settings** -> Target name - prod
3. Hit **Save**
