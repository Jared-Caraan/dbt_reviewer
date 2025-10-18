## `dbt build`
`dbt build` is a command that executes `dbt run` and `dbt test` in that order and in a smart, integrated way. It processes your project in a logical step-by-step sequence.

First, it runs any tests on your sources. If those pass, it moves to the first layer of our models, for example, our staging models. It will run a model and then immediately test it. If that model's test passes, it proceeds to the next layer of models following the same pattern.

At any moment, if a test were to fail, it would halt in that spot and anything downstream of that model would not be built. It would be skipped in our `dbt run` command on the next step.

### `dbt build command`
- `dbt run`
  - Transforms and builds models in your warehouse
- `dbt test`
  - Validates your data for quality issues
- `dbt seed`
  - Loads CSV data into your warehouse tables
- `dbt snapshot`
  -  Tracks slowly changing dimensions in your data
