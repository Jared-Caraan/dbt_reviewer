## Sources
Tables of raw data that were loaded into your data warehouse

## Staging
Make the data look like what you wished it looked like. This involves things like renaming columns, casting data types, or currency conversions.

## Intermediate
Joins and aggregations will occur. These should not depend directly on sources. Instead, they should depend on the staging models.

## Fact
Real-world processes that have occurred or are occurring. Usually an immutable event stream; sessions, transactions, orders, stories, votes.

## Dimensions
Each row is a person, place, or thing; Mutable, though slowly changing: customers, products, candidates, buildings, employees.
