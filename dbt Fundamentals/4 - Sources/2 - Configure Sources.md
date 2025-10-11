## Configure Sources

We will configure the sources in our existing demo project *jaffle shop*. Currently, all sources are hardcoded so we want to tweak and change that into something more dynamic.
<img width="656" height="283" alt="image" src="https://github.com/user-attachments/assets/f58102ec-5af9-42bf-9edc-d788fddb8334" />

1. Under `staging/jaffle_shop` directory, create a new YAML file named as `_src_jaffle_shop.yml`.
> [!NOTE]
> The underscore at the front of the source yaml ensures that it always appears at the top of the directory
2. In your `_src_jaffle_shop.yml`, put this following code
```yaml
sources:
  - name: jaffle_shop
    database: raw
    schema: jaffle_shop
    tables:
      - name: customers
      - name: orders
```
