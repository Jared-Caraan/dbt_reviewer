## Measuring and Enforcing Test Coverage

### Sample dbt Project Repo

<img width="335" height="336" alt="image" src="https://github.com/user-attachments/assets/6afedf96-26db-49e0-bf41-a911a8a86cbb" />

### Generic Tests
**What**
- Defined in yml 🟥
- Act on columns in raw data or dbt models 🟦

**How**
 `dbt test`
- `dbt build`

**When**
- Adhoc in Development
- Scheduled in Production

**Where**

<img width="325" height="335" alt="image" src="https://github.com/user-attachments/assets/a5883788-aa1d-4bd9-94ce-2e836c08ec7a" />

### Custom Tests

**What**
- Defined in test/*.sql files 🟥
- Act on any model or field specifically mentioned 🟦

**How**
- `dbt test`
- `dbt build`

**When**
- Adhoc in Development
- Scheduled in Production

**Where**

<img width="306" height="343" alt="image" src="https://github.com/user-attachments/assets/5f555951-3b60-4eb6-99c7-7509836a4515" />

### Source Freshness Test

**What**
- Defined in staging/*_sources.yml files 🟥
- Act on a timestamp columns from the raw data source 🟦

**How**
- `dbt source freshness`

**When**
- Scheduled in Production

**Where**

<img width="359" height="340" alt="image" src="https://github.com/user-attachments/assets/56377797-27d4-4e5a-ad30-ed900c22dfcc" />

### dbt_meta_testing package
**Steps:**
- Install external package
- Add suggested configuration to the dbt_project.yml file
- Run dbt `run-operation required_tests`
