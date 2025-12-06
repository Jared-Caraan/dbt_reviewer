## Using Snapshots

Let's say we want a snapshot of this model `stg_jaffle_shop__orders`

**stg_jaffle_shop__orders**

```sql
select
    id as order_id,
    user_id as customer_id,
    order_date,
    status as order_status
from {{ source('jaffle_shop', 'orders') }}
```

For this, we need to use the check strategy since order_date timestamp doesn't really change if there are revisions.

Next is to create a new snapshot in the `snapshots` folder and name it `orders_snapshot.yml`.

**orders_snapshot.yml**

```yaml
snapshots:
  - name: orders_snapshot
    relation: source('jaffle_shop', 'orders')
    config:
      schema: snapshots
      database: analytics
      unique_key: id
      strategy: check
      check_cols: ('id', 'user_id', 'order_date', 'status')
      hard_delete: ignore
      dbt_valid_to_current: "to_date('9999-12-31')"
```

Build the snapshot by running the command `dbt build`.

Snapshot tables' metadata columns are only actually going to get updated the second time a snapshot is ran if there's an update to the data.

For testing purposes, you can deliberately change your data, then build your data again through `dbt build`.

> [!NOTE]
> You can build snapshots by executing the comamnd `dbt build` or `dbt snapshot`.

### Under the Hood SQL - Check Strategy

<img width="998" height="648" alt="image" src="https://github.com/user-attachments/assets/cf120256-9d54-472f-a143-269f2d435fe5" />

So what we're actually doing here is we're checking to see where each column specified is null or different from a different existing value with the unique key. So that's how the check strategy makes sure the data is new.

### Previewing the snapshot

Open a new workspace, then query from the new snapshot that has been generated.

```sql
select * from {{ ref( 'orders_snapshot' ) }}
order by id
```

<img width="1464" height="469" alt="image" src="https://github.com/user-attachments/assets/2e497010-2872-4830-8a65-66b5453fb157" />

### Switching to timestamp strategy

To switch to timestamp strategy, just change the snapshot yaml file and change the `strategy` key to `timestamp`. Then add an `updated_at` key with your date column.

```yaml
snapshots:
  ...
      strategy: timestamp
      updated_at: order_date
      ...
```

Then run `dbt snapshot`.

### Under the Hood SQL - Timestamp Strategy

<img width="717" height="562" alt="image" src="https://github.com/user-attachments/assets/5b22f20c-66fe-4388-8782-61608226dcbb" />

**Resource**
- [Snapshot](https://docs.getdbt.com/docs/build/snapshots#what-are-snapshots)
