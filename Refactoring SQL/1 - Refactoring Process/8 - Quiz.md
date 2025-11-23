What is the primary benefit of refactoring SQL code using Common Table Expressions (CTEs)?

a. CTEs allow for faster execution of SQL queries\
b. CTEs automatically optimize SQL queries for different databases\
c. CTEs improve the readability and maintainability of SQL code\
d. CTEs eliminate the need for SQL indexes

Answer: c

##
Which is recommended for organizing your CTEs when refactoring SQL code in dbt?

a. Grouping all SELECT statements at the end of the query\
b. Organizing CTEs by functionality, starting with import CTEs, then logical CTEs, followed by final CTEs\
c. Placing logical CTEs before import CTEs\
d. Combining all CTEs into one to minimize the number of subqueries

Answer: b

##
What is the advantage of centralizing transformation into a staging model when refactoring a SQL script in dbt?

a. It allows for the automatic generation of database indexes\
b. It reduces the need for writing SQL queries\
c. It eliminates the need for documentation in dbt Cloud\
d. It ensures that transformations are applied consistently across the project

Answer: d

##
Which is a best practice when handling large SQL queries with multiple complex joins in dbt?

a. Writing all operations in a single, lengthy SQL query to minimize database calls\
b. Using multiple CTEs to break down the query into logical steps\
c. Nesting subqueries to ensure that all calculations are performed in a single execution\
d. Avoiding the use of aliases to maintain original table names for clarity

Answer: b
