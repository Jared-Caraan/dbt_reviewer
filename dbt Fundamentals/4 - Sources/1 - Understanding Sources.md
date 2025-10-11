## Sources

#### Definition
Sources allow you to document the raw tables that live in your data warehouse in a YAML file. These are set by referencing the database they are in, the schema, and the string of their name. You can even add aliases in that YAML file. Once your YAML file is configured with your sources, instead of writing something like `raw.stripe.payments` in your models, you can use what is called the `source` function or also known as the source macro. This works a lot like the `ref` function that is used in the other models. It looks something like `{{ source('stripe', 'payments') }}` where it references `raw.stripe.payments`.

Think of sources as a virtual handshake between dbt and your raw data in your data platform. It's the key to creating a clear, understandable map of where your data comes from.

#### Benefits
- For any source changes, you can go straight to the YAML file and make the change in one spot and it will tweak everyting downstream.
- They will show up in your lineage
