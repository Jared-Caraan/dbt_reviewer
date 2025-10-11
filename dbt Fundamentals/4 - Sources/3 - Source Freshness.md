## Source Freshness

Source freshness is a health check for your data. It's a dbt powered test that tells you if your source data is up-to-date. You can specify what "fresh" means to you e.g. no more than 24 hrs old. Then dbt checks this, letting you know if the data is getting old.

You can add freshness check in your source YAML file. You can either add it on source level or model level.

To apply freshness check in _src_
