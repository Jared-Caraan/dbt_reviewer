## Snapshots

Snapshots implement Type 2 - Slowly Changing Dimensions over mutable source tables. This SCDs identify how a row has changed over time.

### Creating Snapshots

- Snapshots are defined in YML files under the snapshots directly of your dbt project.
- Need to configure snapshot to tell dbt how to detect record changes.

**Snapshot Example**
```yaml
snapshots:
  - name: string
    relation: relation # source('my_source', 'my_table') or ref('my_model')
    description:  markdown_string
    config:
      database: string
      schema: string
      alias: string
      strategy: timestamp | check
      unique_key: column_name_or_expression
      check_cols: [column_name] | all
      updated_at: column_name
      snapshot_meta_column_names: dictionary
      dbt_valid_to_current: string
      hard_deletes: ignore | invalidate | new_record
```

Because snapshots can't be rebuilt, it's a good idea to put your snapshots in a separate schema so end users know they're special. From there, you might want to set different privileges on your snapshots compared to your models and maybe even run them as a different user or role. So this way, it'll be very difficult to drop a snapshot unless you're very sure that you want to.

##

### Snapshot Strategies

Snapshot "strategies" define how dbt knows if a row has changed: dbt supports two snapshot update strategies:
- Timestamp Strategy: Uses a timestamp column to identify changes in the source data - **preferred, and more efficient**
- Check Strategy:
  - Useful for tables which do not have a reliable **updated_at** column.
  - Re-evaluates the entire snapshot query on each run to detect changes.

### How do I run my snapshots?
- Execute the dbt snapshot command

**dbt snapshot**

**On first run:**
- create initial snapshot table
- all columns from select statement
- dbt meta-fields added
- dbt_valid_to = null

**On subsequent runs:**
- check for changed records
- update dbt_valid_to column on changed records
- insert updated record(s) into snapshot table
- dbt_valid_to = null on new records

### When does snapshotting get complex? When _shouldn't_ I snapshot a model?
- Snapshots are incredibly useful, but they do add a bit of complexity for joining tables downstream because you've added multiple rows of history per id.
  - What happens when you have 10 snapshots that you want to join together, and you want to capture the history of all the datasets?
- If you find a bug and need to change your modelling code, you can find yourself with inaccurate results and no way of recalculating the correct data.
  - By contrast, if you snapshot the source data and build on top of that, you can always recalculate everything from first principles if/when you need to.
- **Rule of thumb**: Always snapshot sources! Sometimes snapshot fact and dim models.

### How often should I snapshot my snapshots?

Capturing history can be dependent on how your job is scheduled.

<img width="1403" height="357" alt="image" src="https://github.com/user-attachments/assets/470c1ce3-1ae4-4a5c-b63a-22b620956a6c" />

The solution for this is to run your snapshot as often as your source data changes!

**Resource**
- [Snapshot](https://docs.getdbt.com/docs/build/snapshots#what-are-snapshots)
