## Grant permissions macro

We can run queries against the database when calling a macro. In the instructor's example, we walked through how to use a macro to execute multiple permissions statements in a parameterized way. We leveraged the following dbt specific Jinja functions to do so:

**run_query** ([documentation](https://docs.getdbt.com/reference/dbt-jinja-functions/run_query))

The run_query macro provides a convenient way to run queries and fetch their results. It is a wrapper around the statement block, which is more flexible, but also more complicated to use.

**log** ([documentation](https://docs.getdbt.com/reference/dbt-jinja-functions/log))

The log macro is used to log a line of text to the logs in dbt. We can add the key default=True to also log the same text to the command line interface.

**target** ([documentation](https://docs.getdbt.com/reference/dbt-jinja-functions/target))

Target contains information about your connection to the warehouse. The variables accessible within the target variable for all adapters include profile_name, name, schema, type, and threads. Check out the documentation for adapter specific variables

## Union by prefix macro

We can also use the results of a query to template the SQL we are writing in a model file. In the instructor's example, we walked through the use of the execute variable, agate file types, and the get_relations_by_prefix macro

**execute** ([documentation](https://docs.getdbt.com/reference/dbt-jinja-functions/execute))

The execute variable is a boolean variable that is true when dbt compiles each node of your project. This can be helpful to wrap around a block of text that you want to only run in the execution phase. Check out the docs linked above for a concrete example and additional context.

**agate file types** ([documentation](https://agate.readthedocs.io/en/latest/api/table.html))

When executing the run_query macro, the results of the query are stored in a file type called agate. If you are familiar with pandas in python, this works in a very similar fashion. Check out the documentation linked above for interacting with agate types.

**get_relations_by_prefix** ([documentation](https://github.com/dbt-labs/dbt-utils#get_relations_by_prefix-source))

The get_relations_by_prefix macro can be imported into your project through the dbt_utils package. This works by parsing through the dbt project and looking for relations with a similar prefix. These relations are returned in the form of a list. Check out the documentation linked above for additional ways to leverage this macro.

## Clean stale models macro

The instructor walks through an example of using all the tools in the previous lesson to clean up his development schema for any stale models that haven’t been altered in the past 7 days. This macro was built using the information schema in Snowflake and this can be replicated on other data platforms using the respective information schemas.
