## Tradeoffs and Tactics

Incremental models introduce tradeoffs.

- Most incremental models are “approximately correct”
- They introduce a level of code complexity (i.e. how easy it is for someone to understand your code)
- Prioritizing correctness can negate performance gains from incrementality.

**How do I choose which models to materialize as incrementals?**

Good candidates:

- Immutable event streams: tall and skinny tables, append-only, no updates
- If there are any updates, a reliable updated_at field

Not-so-good candidates:

- A small table
- Data changes constantly: new columns, renamed columns, etc.
- Data is updated in unpredictable ways

## Incremental Strategies

[Incremental strategies](https://docs.getdbt.com/docs/build/incremental-strategy) for materializations optimize performance by defining how to handle new and changed data.

There are various strategies to implement the concept of incremental materializations. The value of each strategy depends on:
- The volume of data.
- The reliability of your `unique_key`.
- The support of certain features in your data platform.

<img width="1343" height="576" alt="image" src="https://github.com/user-attachments/assets/59390442-b10d-4129-b6f6-ac4bbe0b9869" />

### Append:

- **Adds** new rows to target table **only**
- Does not check for duplicates
- Does not check for updates
- **Best used for:** Truly immutable event streams
- **SQL used: insert into** to add new rows

### Merge:

- Updates records that already exist using primary key
- Inserts new records based on primary key
- Runs full table scan (can cause performance issues at scale)
- **Best used for:**
  - Models that are getting new data added, BUT they could also be updating existing records. This is a good way to address the duplicate records issue that something like append doesn't address.
  - Best for tables with a small number of updates each run.
- **SQL Used:** merge into with matching on primary key

### Delete+insert

- Grabs all selected records, deletes old version of those records if they exist in the target table.
- Inserts new records and the new version of the records deleted above based on primary key
- Requires full table scan (unless you configure incremental predicates)
- **Best used for:** Models are getting new data and updates to old rows, but the data platform does not support MERGE.
- **SQL used:** delete from and then insert into with matching on primary key

### Insert_overwrite
- Replaces entire partitions in a destination table.
- Does not require scanning entire source table–will only scan the partitions you configure.
- **Much more efficient than merge on BigQuery**.
- **Best used for:** Models that are partitioned getting new data and updates to old rows, but merge is too slow and costly. insert_overwrite is more complex, & most useful on BigQuery.
- **SQL used:**
  - In BigQuery: creates temp table, declares partitions to replace, then merge into.
  - In other databases: DELETE FROM then INSERT INTO

### Microbatch
- Divides data into atomic, time-bound units (ex: day)
- Splits large models into multiple time-bounded queries: batches! dbt takes those queries and inserts them into your target table.
- **Best used for:**
  - Very large time-series data sets
  - Time series with regular updates.
- **SQL used:**
  - Time-bound SELECT query to construct batch.
  - To insert batch, dbt will use insert/overwrite or delete + insert depending on data platform.
