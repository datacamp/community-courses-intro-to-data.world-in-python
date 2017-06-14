---
title       : Querying with data.world
description : Querying with data.world
--- type:NormalExercise lang:python xp:100 skills:2 key:27cbaefdc0
## SQL: Querying a table

Another way to pull data in from data.world is to use the `query` method of the datadotworld module. The `query` method lets you use the SQL or SPARQL query languages to query one or more datasets. This makes it easy for you to pull in just what fields and aggregations you need from the data, and lets you even join tabular data together with a single call to data.world. 

The `query` function is a lot like `load_dataset` as it gives you access to three properties to access the resulting data: `raw_data`, `table`, and `dataframe`. So, lets try out a couple of SQL queries and then we'll jump into a SPARQL example. 

Data.world actually supports a dialect of SQL called *dwSQL*. *dwSQL* does most everything you'd normally do with SQL, with the exception of `INSERT`, `UPDATE` or `DELETE`. It also has some extended funcionality specific to data.world. Check out the [full dwSQL documentation](https://docs.data.world/tutorials/dwsql/), and here we'll cover the basics of using the `query` method.

Using the dataset at `https://data.world/nrippner/refugee-host-nations`, follow the instructions below:


*** =instructions
- Write a SQL query to select all rows from the `unhcr_all` table where `Year` equals 2010. Assign the query string to a `sql_query` variable.
- Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/nrippner/refugee-host-nations` dataset. Assign the results to a `query2010` variable.
- Use the dataframe property of the resulting query to create a dataframe variable named `unhcr2010`
- Print the first 5 rows using the head method.

*** =hint
- Make sure to use backtics around the table name, since it has an understore in it. You'll need to include these for hyphens as well.
- Use the query ``SELECT * FROM `unhcr_all` WHERE Year = 2010``
- Use t dataframe property with this format: `____.dataframe`

*** =pre_exercise_code
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
    f.write('auth_token = eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50OmRhdGFjYW1wc3R1ZGVudCIsImlzcyI6ImFnZW50OmRhdGFjYW1wc3R1ZGVudDo6MmMzMTM4Y2YtMGJjNy00N2FmLTg1MWItMGE1YmQ3ZTlhYjliIiwiaWF0IjoxNDkzMjI5NjMwLCJyb2xlIjpbInVzZXJfYXBpX3dyaXRlIiwidXNlcl9hcGlfcmVhZCJdLCJnZW5lcmFsLXB1cnBvc2UiOnRydWV9.MODLiozjfoCE9VS91Ycf1-inHuZjU-tR3vBvTjRHcBuhpYoxNhmvdy_1IW28doMFO4XNgJSMu3PTuSqNaCeWTg')
    f.close()
```

*** =sample_code
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## Write a SQL query to select all rows from the `unhcr_all` table where `Year` equals 2010. Assign the query string to a `sql_query` variable.
sql_query = 

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/nrippner/refugee-host-nations` dataset. Assign the results to a `query2010` variable.
query2010 = 

## Use the dataframe property of the resulting query to create a dataframe variable named `unhcr2010`
unhcr2010 = 

## Print the first 5 rows using the head method.

```

*** =solution
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## Write a SQL query to select all rows from the `unhcr_all` table where `Year` equals 2010. Assign the query string to a `sql_query` variable.
sql_query = "SELECT * FROM `unhcr_all` WHERE Year = 2010"

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/nrippner/refugee-host-nations` dataset. Assign the results to a `query2010` variable.
query2010 = dw.query('https://data.world/nrippner/refugee-host-nations', sql_query)

## Use the dataframe property of the resulting query to create a dataframe variable named `unhcr2010`
unhcr2010 = query2010.dataframe

## Print the first 5 rows using the head method.
pp.pprint(unhcr2010.head(5))
```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

#test_function('pprint.pprint', index = 2)

success_msg('Great work!')
```


--- type:NormalExercise lang:python xp:100 skills:2 key:a851333ad8
## SQL: Query multiple tables

Not only can you create very specific queries against a single table on data.world, you can also write queries against multiple tables within a single dataset or across many datasets! 

We call these cross-dataset queries 'federated queries' and they're just like same-dataset queries, but require you to specify not just the name of the tables, but also the unique dataset path that the remote table is in. 

We've been using the full URL for the dataset in our datadotworld method examples, but for federated queries, you'll need to use just the unique part of the URL path. Let's look at the dataset `https://data.world/len/intelligence-of-dogs`. The unique part of the URL will be `len/intelligence-of-dogs`, where `len` is the owner id and `intelligence-of-dogs` is the dataset id. 

We'll use this to build an example query that calls the `dog_intelligence` table from that dataset, which will be joined against the `AKC Breed Info` table of the 'local' dataset we'll pass as a parameter to the `query` method, `https://data.world/len/dog-canine-breed-size-akc`:

``
SELECT breedSmarts.Classification, AVG(breedSmarts.obey) as obey, AVG(weight_high_lbs) as heavyWeightAvg, AVG(weight_low_lbs) as lowWeightAvg 
FROM `AKC Breed Info` as breedSize
JOIN len.`intelligence-of-dogs`.`dog_intelligence` as breedSmarts ON breedSmarts.Breed = breedSize.breed
GROUP BY breedSmarts.Classification
ORDER BY obey
``

Now try it on your own with a different set of datasets:

*** =instructions
- Write a query against `https://data.world/agriculture/national-farmers-markets` to left join it's `Export` table with the `adult_obese` table in `https://data.world/health/obesity-by-state-2014`. Select `State`, the count of farmer's markets (FMID), and the average of `Value` from `adult_obese`
- Execute the SQL query against `https://data.world/agriculture/national-farmers-markets` using the `query()` method
- Create a `stateStats` dataframe from the results
- Plot `stateStats` results using State as the x-axis (matplotlib is already imported)


*** =hint
- Here's the query you can use 
``
SELECT State, count(FMID) as count, Avg(obesity.Value) as obesityAvg FROM Export LEFT JOIN health.`obesity-by-state-2014`.`adult_obese` as obesity ON State = obesity.Location GROUP BY State ORDER BY count desc``
- To execute the query use: queryResults = dw.query(____, _____)
- To plot the results, use _____.plot(x=____)

*** =pre_exercise_code
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
    f.write('auth_token = eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50OmRhdGFjYW1wc3R1ZGVudCIsImlzcyI6ImFnZW50OmRhdGFjYW1wc3R1ZGVudDo6MmMzMTM4Y2YtMGJjNy00N2FmLTg1MWItMGE1YmQ3ZTlhYjliIiwiaWF0IjoxNDkzMjI5NjMwLCJyb2xlIjpbInVzZXJfYXBpX3dyaXRlIiwidXNlcl9hcGlfcmVhZCJdLCJnZW5lcmFsLXB1cnBvc2UiOnRydWV9.MODLiozjfoCE9VS91Ycf1-inHuZjU-tR3vBvTjRHcBuhpYoxNhmvdy_1IW28doMFO4XNgJSMu3PTuSqNaCeWTg')
    f.close()
```

*** =sample_code
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## Write a SQL query to select State, the count of farmers markets (FMID), and average obesity rate from agriculture.`national-farmers-markets`.Export, LEFT JOINED against health.`obesity-by-state-2014`.adult_obese on State and Location
sql_query = 

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/agriculture/national-farmers-markets` dataset. Assign the results to a `queryResults` variable.
queryResults = 

## Use the dataframes property of the resulting query to create a dataframe variable named `stateStats`
stateStats = 

## Plot the stateStats results using State as the x-axis (matplotlib is already imported)
____.plot(x=____)
```

*** =solution
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## Write a SQL query to select State, the count of farmers markets (FMID), and average obesity rate from agriculture.`national-farmers-markets`.Export, LEFT JOINED against health.`obesity-by-state-2014`.adult_obese on State and Location
sql_query = "SELECT State, count(FMID) as count, Avg(obesity.Value) as obesityAvg FROM Export LEFT JOIN health.`obesity-by-state-2014`.`adult_obese` as obesity ON State = obesity.Location GROUP BY State ORDER BY count desc"

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/agriculture/national-farmers-markets` dataset. Assign the results to a `queryResults` variable.
queryResults = dw.query('https://data.world/agriculture/national-farmers-markets', sql_query)

## Use the dataframes property of the resulting query to create a dataframe variable named `stateStats`
stateStats = queryResults.dataframes

## Plot the stateStats results using State as the x-axis (matplotlib is already imported)
stateStats.plot(x='State')
```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

test_function('pprint.pprint', index = 2)

success_msg('Great work!')
```


--- type:NormalExercise lang:python xp:100 skills:2 key:27858032c6
## SPARQL: Querying linked data

Behind the scenes, data.world is converting all tabular data files into linked data using Semantic Web technolgies. This allows you to upload any tabular format, like xlsx, csv, tsv or json, and instantly be able to query and join them without issue. SQL is great for this, but SPARQL - which is the query language for linked data - can be more robust and flexible than SQL creating much more complex queries. 

We won't cover all that SPARQL can do here, but get to know SPARQL through our [tutorial](https://docs.data.world/documentation/api/sparql.html), and practice loading data with `SPARQL` through the `query` method by adding a `query_type='sparql'` parameter. 

Let's give it a shot...

*** =instructions
- Use the pre-defined SPARQL query to query dataset `http://data.world/tutorial/sparqltutorial` and return the results to a `queryResults` variable.
- Create a `houseStark` dataframe.
- Use `print` to print the dataframe to the screen.

*** =hint
- Use the format `dw.query(____, ____, query_type=____)`
- Print the dataframe using `print(____)`


*** =pre_exercise_code
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
    f.write('auth_token = eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50OmRhdGFjYW1wc3R1ZGVudCIsImlzcyI6ImFnZW50OmRhdGFjYW1wc3R1ZGVudDo6MmMzMTM4Y2YtMGJjNy00N2FmLTg1MWItMGE1YmQ3ZTlhYjliIiwiaWF0IjoxNDkzMjI5NjMwLCJyb2xlIjpbInVzZXJfYXBpX3dyaXRlIiwidXNlcl9hcGlfcmVhZCJdLCJnZW5lcmFsLXB1cnBvc2UiOnRydWV9.MODLiozjfoCE9VS91Ycf1-inHuZjU-tR3vBvTjRHcBuhpYoxNhmvdy_1IW28doMFO4XNgJSMu3PTuSqNaCeWTg')
    f.close()
```

*** =sample_code
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## We've written a SPARQL query for you and assigned it to the `sparql_query` variable: 
sparql_query = "PREFIX GOT: <http://data.world/tutorial/sparqltutorial/GOT.csv/GOT#> SELECT ?FName ?LName WHERE {?person GOT:House \"Stark\" . ?person GOT:FName ?FName . ?person GOT:LName ?LName .}"

## Use the `query` method of the datadotworld module to run the query against `http://data.world/tutorial/sparqltutorial` dataset. Remember to specify it as a sparql query. 
## Assign the results to a `queryResults` variable.

## Use the dataframe property of the resulting query to create a dataframe variable named `houseStark`

## Plot the stateStats results using State as the x-axis (matplotlib is already imported)

```

*** =solution
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

## We've written a SPARQL query for you and assigned it to the `sparql_query` variable: 
sparql_query = "PREFIX GOT: <http://data.world/tutorial/sparqltutorial/GOT.csv/GOT#> SELECT ?FName ?LName WHERE {?person GOT:House \"Stark\" . ?person GOT:FName ?FName . ?person GOT:LName ?LName .}"

## Use the `query` method of the datadotworld module to run the query against `http://data.world/tutorial/sparqltutorial` dataset. Remember to specify it as a sparql query. 
## Assign the results to a `queryResults` variable.
queryResults = dw.query('http://data.world/tutorial/sparqltutorial', sparql_query, query_type='sparql')

## Use the dataframe property of the resulting query to create a dataframe variable named `houseStark`
houseStark = queryResults.dataframe

## Plot the stateStats results using State as the x-axis (matplotlib is already imported)
print(houseStark)

```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

test_function('print', index = 1)

success_msg('Great work!')
```
