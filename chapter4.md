---
title: 'Querying with data.world'
description: 'Querying with data.world'
---

## SQL: Querying a table

```yaml
type: NormalExercise
key: 27cbaefdc0
lang: python
xp: 100
skills: 2
```

Another way to pull data in from data.world is to use the `query()` method of the datadotworld module. `query()` lets you use SQL or SPARQL to query one or more datasets, and takes a dataset URL and the query string as parameters. This makes it easy for you to pull in exactly what fields and aggregations you need from the data, and even lets you get joined tables with a single call to data.world. 

The `query()` method is a lot like `load_dataset` as it gives you access to three properties to access the resulting data: `raw_data`, `table`, and `dataframe`. Lets try out a couple of SQL queries and then we'll jump into a SPARQL example. 

SQL on data.world is actually a dialect we've created called *dwSQL*. *dwSQL* does most everything you'd normally do in a SQL `SELECT`, and it also has some extended funcionality specific to data.world. Check out the [full dwSQL documentation](https://docs.data.world/tutorials/dwsql/), and here we'll work with some basics.

Using the dataset at `https://data.world/nrippner/refugee-host-nations`, follow the instructions below:

`@instructions`
- Complete the SQL query to select all rows from the `unhcr_all` table where `Year` equals 2010. Assign the query string to a `sql_query` variable.
- Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/nrippner/refugee-host-nations` dataset. Assign the results to a `query2010` variable.
- Use the dataframe property of the resulting query to create a dataframe variable named `unhcr2010`
- Print the first 5 rows using the head method.

`@hint`
- It's a good idea to use backtics around the table name in case it has non-alpha characters in it.
- For `sql_query`, just fill in the blank with the table name `unhcr_all`.
- The query method is in the format `dw.query(dataset_url, sql_query)`
- Assign the dataframe using this format: `____.dataframe`

`@pre_exercise_code`
```{python}
import pprint as pp
import os

filename = '/home/repl/.dw/config'
if not os.path.exists(os.path.dirname(filename)):
    try:
        os.makedirs(os.path.dirname(filename))
    except OSError as exc: # Guard against race condition
        if exc.errno != errno.EEXIST:
            raise
with open(filename, 'w') as f:
    f.write('[DEFAULT]\n')
    f.write('auth_token = eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50OmRhdGFjYW1wc3R1ZGVudCIsImlzcyI6ImFnZW50OmRhdGFjYW1wc3R1ZGVudDo6MmMzMTM4Y2YtMGJjNy00N2FmLTg1MWItMGE1YmQ3ZTlhYjliIiwiaWF0IjoxNDkzMjI5NjMwLCJyb2xlIjpbInVzZXJfYXBpX3JlYWQiXSwiZ2VuZXJhbC1wdXJwb3NlIjp0cnVlfQ.ISiCSEd1Zb5Ot40-osANMnlab3K4IehWFeT-7qYvzccgzuUp7eSYLY7GGNsJIhJT_JYf_PFdQG3vcTnSRGt5hA')
    f.close()
```

`@sample_code`
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## Complete the SQL query to select all rows from the `unhcr_all` table where `Year` equals 2010. Assign the query string to a `sql_query` variable.
sql_query = "SELECT * FROM `_____` WHERE Year = 2010"

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/nrippner/refugee-host-nations` dataset. Assign the results to a `query2010` variable.
query2010 = ___

## Use the dataframe property of the resulting query to create a dataframe variable named `unhcr2010`
unhcr2010 = ___

## Print the first 5 rows using the head method.

```

`@solution`
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## Complete the SQL query to select all rows from the `unhcr_all` table where `Year` equals 2010. Assign the query string to a `sql_query` variable.
sql_query = "SELECT * FROM `unhcr_all` WHERE Year = 2010"

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/nrippner/refugee-host-nations` dataset. Assign the results to a `query2010` variable.
query2010 = dw.query('https://data.world/nrippner/refugee-host-nations', sql_query)

## Use the dataframe property of the resulting query to create a dataframe variable named `unhcr2010`
unhcr2010 = query2010.dataframe

## Print the first 5 rows using the head method.
pp.pprint(unhcr2010.head(5))
```

`@sct`
```{python}
Ex().has_import('datadotworld', same_as = True)

msg = "Assign the following string to `sql_query` for your SQL statement: ```SELECT * FROM `unhcr_all` WHERE Year = 2010```"
Ex().check_object("sql_query", missing_msg = msg).has_equal_value(incorrect_msg = msg)

msg = "Assign the query results to `query2010` using `dw.query()` and pass the dataset URL and `sql_query` as the parameters."
Ex().check_function("datadotworld.query").multi(
  check_args(0).has_equal_ast(incorrect_msg = msg),
  check_args(1).has_equal_value(incorrect_msg = msg)
)

Ex().check_df("unhcr2010").multi(
  check_keys('year', missing_msg = "Did you convert `query2010` to a dataframe and assign the result to `unhcr2010`?").has_equal_value(append = True, incorrect_msg = "Did you convert `query2010` to a dataframe and assign the result to `unhcr2010`?"),
  check_keys('origin', missing_msg = "Did you convert `query2010` to a dataframe and assign the result to `unhcr2010`?").has_equal_value(append = True, incorrect_msg = "Did you convert `query2010` to a dataframe and assign the result to `unhcr2010`?"),
  check_keys('refugees_incl_refugee_like_situations', missing_msg = "Did you convert `query2010` to a dataframe and assign the result to `unhcr2010`?").has_equal_value(append = True, incorrect_msg = "Did you convert `query2010` to a dataframe and assign the result to `unhcr2010`?"),
  check_keys('total_population', missing_msg = "Did you convert `query2010` to a dataframe and assign the result to `unhcr2010`?").has_equal_value(append = True, incorrect_msg = "Did you convert `query2010` to a dataframe and assign the result to `unhcr2010`?")
)



msg = "Print the first 5 rows of `unhcr2010` using `pp.pprint(unhcr2010.head(5))`"
Ex().check_correct(
  check_function('pprint.pprint').check_args(0).has_equal_value(incorrect_msg = msg),
  check_function("unhcr2010.head").check_args(0).has_equal_value(incorrect_msg = msg)
)

success_msg('Great work!')
```

---

## SQL: Query multiple tables

```yaml
type: NormalExercise
key: a851333ad8
lang: python
xp: 100
skills: 2
```

Not only can you create very specific queries against a single table on data.world, you can also write queries against multiple tables within a single dataset or across many datasets! 

We call these cross-dataset queries 'federated queries' and they're just like same-dataset queries, but require you to specify not just the name of the tables, but also the unique dataset path that the remote table is in using dot notation. 

We've been using the full URL for the dataset in our datadotworld method examples, but for federated queries, you'll need to use just the unique part of the URL path. Let's look at the dataset `https://data.world/len/intelligence-of-dogs`. The unique part of the URL is `len/intelligence-of-dogs`, where `len` is the owner id and `intelligence-of-dogs` is the dataset id. 

Lets use that to build an example query that calls the `dog_intelligence` table from that dataset, which will be joined against the `AKC Breed Info` table of the 'local' dataset we'll pass as a parameter to the `query` method, `https://data.world/len/dog-canine-breed-size-akc`:

```{sql}
SELECT 
  breedSmarts.Classification, 
  AVG(breedSmarts.obey) AS obey, 
  AVG(weight_high_lbs) AS heavyWeightAvg, 
  AVG(weight_low_lbs) AS lowWeightAvg 
FROM `AKC Breed Info` AS breedSize
  JOIN len.`intelligence-of-dogs`.`dog_intelligence` 
    AS breedSmarts 
  ON breedSmarts.Breed = breedSize.breed
GROUP BY breedSmarts.Classification
ORDER BY obey
```

Notice on the 'secondary' table we used the dataset owner id and dataset id to reference the `dog_intelligence` table: 
```
len.`intelligence-of-dogs`.`dog_intelligence
```

Now try a similar query on your own with a different set of datasets:

`@instructions`
- Complete the federated SQL query to return three columns: state, the count of farmers markets (fmid) per state, and the average adult obesity rate (`adult_obese`.`value`) per state from the `export` table in `https://data.world/agriculture/national-farmers-markets`, left joined with the `adult_obese` table in `https://data.world/health/obesity-by-state-2014` on the `export`.`state` and `adult_obese`.`location` fields.
- Execute the SQL query against `https://data.world/agriculture/national-farmers-markets` using the `query()` method
- Create a `stateStats` dataframe from the results
- Plot the `stateStats` results using State as the x-axis (matplotlib is already imported)

`@hint`
- Here's the query you can use 
``
SELECT state, count(fmid) as count, Avg(obesity.value) as obesityAvg FROM Export LEFT JOIN health.`obesity-by-state-2014`.`adult_obese` as obesity ON state = obesity.location GROUP BY state ORDER BY count desc``
- To execute the query use `queryResults = dw.query(____, _____)`
- To plot the results, use `stateStats.plot(x='state')`

`@pre_exercise_code`
```{python}
import pprint as pp
import os
import matplotlib
import matplotlib.pyplot as plt

filename = '/home/repl/.dw/config'
if not os.path.exists(os.path.dirname(filename)):
    try:
        os.makedirs(os.path.dirname(filename))
    except OSError as exc: # Guard against race condition
        if exc.errno != errno.EEXIST:
            raise
with open(filename, 'w') as f:
    f.write('[DEFAULT]\n')
    f.write('auth_token = eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50OmRhdGFjYW1wc3R1ZGVudCIsImlzcyI6ImFnZW50OmRhdGFjYW1wc3R1ZGVudDo6MmMzMTM4Y2YtMGJjNy00N2FmLTg1MWItMGE1YmQ3ZTlhYjliIiwiaWF0IjoxNDkzMjI5NjMwLCJyb2xlIjpbInVzZXJfYXBpX3JlYWQiXSwiZ2VuZXJhbC1wdXJwb3NlIjp0cnVlfQ.ISiCSEd1Zb5Ot40-osANMnlab3K4IehWFeT-7qYvzccgzuUp7eSYLY7GGNsJIhJT_JYf_PFdQG3vcTnSRGt5hA')
    f.close()
```

`@sample_code`
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## Complete the SQL query to select state, the count of farmers markets (fmid), and average obesity rate from agriculture.`national-farmers-markets`.export, LEFT JOINED against health.`obesity-by-state-2014`.adult_obese on state and location
sql_query = "SELECT state, count(fmid) as count, Avg(obesity.value) as obesityAvg FROM ____ LEFT JOIN ____.`____`.`____` as obesity ON state = obesity.location GROUP BY state ORDER BY count desc"

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/agriculture/national-farmers-markets` dataset. Assign the results to a `queryResults` variable.
queryResults = ___

## Use the dataframes property of the resulting query to create a dataframe variable named `stateStats`
stateStats = ___

## Plot the stateStats results using state as the x-axis (matplotlib is already imported)
____.plot(x=____)

plt.show()
```

`@solution`
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## Complete the SQL query to select state, the count of farmers markets (fmid), and average obesity rate from agriculture.`national-farmers-markets`.export, LEFT JOINED against health.`obesity-by-state-2014`.adult_obese on state and location
sql_query = "SELECT state, count(fmid) as count, Avg(obesity.Value) as obesityAvg FROM Export LEFT JOIN health.`obesity-by-state-2014`.`adult_obese` as obesity ON state = obesity.location GROUP BY state ORDER BY count desc"

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/agriculture/national-farmers-markets` dataset. Assign the results to a `queryResults` variable.
queryResults = dw.query('https://data.world/agriculture/national-farmers-markets', sql_query)

## Use the dataframes property of the resulting query to create a dataframe variable named `stateStats`
stateStats = queryResults.dataframe

## Plot the stateStats results using state as the x-axis (matplotlib is already imported)
stateStats.plot(x='state')

plt.show()
```

`@sct`
```{python}
test_import('datadotworld', same_as = True)

msg = "Assign the following string to `sql_query` for your SQL statement: ```SELECT state, count(FMID) as count, Avg(obesity.value) as obesityAvg FROM export LEFT JOIN health.`obesity-by-state-2014`.`adult_obese` as obesity ON state = obesity.location GROUP BY state ORDER BY count desc```"
test_object("sql_query", undefined_msg = msg, incorrect_msg = msg)

msg = "Assign the query results to `queryResults` using `dw.query()` and pass `https://data.world/agriculture/national-farmers-markets` and `sql_query` as the parameters."
test_function("datadotworld.query", 1, incorrect_msg = msg)

msg = "Create the `stateStats` dataframe using `queryResults.dataframe`"
test_object("stateStats", undefined_msg = msg, incorrect_msg = msg)

msg = "Plot the `stateStats` results using `stateStats.plot(x='state')`"
test_function('stateStats.plot', 1, incorrect_msg = msg)

msg = "No need to remove `plt.show()` from the code. It's needed to print your plot!"
test_function('matplotlib.pyplot.show', 1, incorrect_msg = msg, not_called_msg = msg)

success_msg('Great work!')
```

---

## SPARQL: Querying linked data

```yaml
type: NormalExercise
key: 27858032c6
lang: python
xp: 100
skills: 2
```

Behind the scenes, data.world is converting all tabular data files into linked data using Semantic Web technolgies. This allows you to upload any tabular format, like xlsx, csv, tsv or json, and instantly be able to query and join them without issue. SQL is great for this, but SPARQL - which is the query language for linked data - can be more robust and flexible than SQL, allowing for more complex queries. 

We won't cover all that SPARQL can do here, but get to know it through our [tutorial](https://docs.data.world/documentation/api/sparql.html), and practice loading data with SPARQL through the `query` method by adding a `query_type='sparql'` parameter. 

Let's give it a shot...

`@instructions`
- Use the pre-defined SPARQL query to query dataset `http://data.world/tutorial/sparqltutorial` and return the results to a `queryResults` variable.
- Create a `houseStark` dataframe.
- Use `pp.pprint` to print the dataframe to the screen.

`@hint`
- Don't forget to pass `query_type='sparql'` as a query parameter.
- Use the format `dw.query(____, ____, query_type=____)`
- Print the dataframe using `pp.pprint(____)`

`@pre_exercise_code`
```{python}
import pprint as pp
import os

filename = '/home/repl/.dw/config'
if not os.path.exists(os.path.dirname(filename)):
    try:
        os.makedirs(os.path.dirname(filename))
    except OSError as exc: # Guard against race condition
        if exc.errno != errno.EEXIST:
            raise
with open(filename, 'w') as f:
    f.write('[DEFAULT]\n')
    f.write('auth_token = eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50OmRhdGFjYW1wc3R1ZGVudCIsImlzcyI6ImFnZW50OmRhdGFjYW1wc3R1ZGVudDo6MmMzMTM4Y2YtMGJjNy00N2FmLTg1MWItMGE1YmQ3ZTlhYjliIiwiaWF0IjoxNDkzMjI5NjMwLCJyb2xlIjpbInVzZXJfYXBpX3JlYWQiXSwiZ2VuZXJhbC1wdXJwb3NlIjp0cnVlfQ.ISiCSEd1Zb5Ot40-osANMnlab3K4IehWFeT-7qYvzccgzuUp7eSYLY7GGNsJIhJT_JYf_PFdQG3vcTnSRGt5hA')
    f.close()
```

`@sample_code`
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

# We've written a SPARQL query for you and assigned it to the `sparql_query` variable: 
sparql_query = "PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/> SELECT ?FName ?LName WHERE {?person GOT:col-got-house \"Stark\" . ?person GOT:col-got-fname ?FName . ?person GOT:col-got-lname ?LName .}"

# Use the pre-defined SPARQL query to query dataset http://data.world/tutorial/sparqltutorial and return the results to a queryResults variable

# Use the dataframe property of the resulting query to create a dataframe variable named `houseStark`

# Use pp.pprint() to print the dataframe to the screen.

```

`@solution`
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

# We've written a SPARQL query for you and assigned it to the `sparql_query` variable: 
sparql_query = "PREFIX GOT: <https://tutorial.linked.data.world/d/sparqltutorial/> SELECT ?FName ?LName WHERE {?person GOT:col-got-house \"Stark\" . ?person GOT:col-got-fname ?FName . ?person GOT:col-got-lname ?LName .}"

# Use the pre-defined SPARQL query to query dataset http://data.world/tutorial/sparqltutorial and return the results to a queryResults variable
queryResults = dw.query('http://data.world/tutorial/sparqltutorial', sparql_query, query_type='sparql')

# Use the dataframe property of the resulting query to create a dataframe variable named `houseStark`
houseStark = queryResults.dataframe

# Use pp.pprint() to print the dataframe to the screen.
pp.pprint(houseStark)

```

`@sct`
```{python}
test_import('datadotworld', same_as = True)

msg = "No need to change or remove the predefied `sparql_query`! We've created this for you to use in the exercise."
test_object("sparql_query", undefined_msg = msg, incorrect_msg = msg)

msg = "Assign the query results to `queryResults` using `dw.query()` and pass `http://data.world/tutorial/sparqltutorial`, `sparql_query` and `query_type='sparql'` as the parameters."
test_function("datadotworld.query", 1, incorrect_msg = msg)

msg = "Create the `houseStark` dataframe using `queryResults.dataframe`"
test_object("houseStark", undefined_msg = msg, incorrect_msg = msg)

msg = "Be sure and print your dataframe using `pp.pprint(houseStark)`"
test_function('pprint.pprint', 1, incorrect_msg = msg, not_called_msg = msg)

success_msg('Great work!')
```
