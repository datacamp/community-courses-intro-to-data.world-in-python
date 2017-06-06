---
title       : Querying with data.world
description : Querying with data.world
--- type:NormalExercise lang:python xp:100 skills:2 key:27cbaefdc0
## SQL: Querying a table

*** =instructions
- Write a SQL query to select all rows from the `unhcr_all.csv/unhcr_all` table where `Year` equals 2010. Assign the query string to a `sql_query` variable.
- Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/nrippner/refugee-host-nations` dataset. Assign the results to a `query2010` variable.
- Use the dataframe property of the resulting query to create a dataframe variable named `unhcr2010`
- Print the first 5 rows using the head method.

*** =hint

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

## Write a SQL query to select all rows from the `unhcr_all.csv/unhcr_all` table where `Year` equals 2010. Assign the query string to a `sql_query` variable.
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

## Write a SQL query to select all rows from the `unhcr_all.csv/unhcr_all` table where `Year` equals 2010. Assign the query string to a `sql_query` variable.
sql_query = "SELECT * FROM `unhcr_all.csv/unhcr_all` WHERE Year = 2010"

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/nrippner/refugee-host-nations` dataset. Assign the results to a `query2010` variable.
query2010 = dw.query('https://data.world/nrippner/refugee-host-nations', sql_query)

## Use the dataframe property of the resulting query to create a dataframe variable named `unhcr2010`
unhcr2010 = query2010.dataframe

## Print the first 5 rows using the head method.
unhcr2010.head(5)

```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

test_function('pprint.pprint', index = 2)

success_msg('Great work!')
```


--- type:NormalExercise lang:python xp:100 skills:2 key:a851333ad8
## SQL: Query multiple tables


*** =instructions

*** =hint

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

## Write a SQL query to select the state, count of farmers markets, and average obesity rate from health.`obesity-by-state-2014`.adult_obese and agriculture.`national-farmers-markets`.Export
sql_query = 

## Use the `query` method of the datadotworld module to run the `sql_query` against the `https://data.world/nrippner/refugee-host-nations` dataset. Assign the results to a `query2010` variable.
query2010 = 

## Use the dataframe property of the resulting query to create a dataframe variable named `unhcr2010`
unhcr2010 = 

## Print the first 5 rows using the head method.


```

*** =solution
```{python}

```

*** =sct
```{python}

```


--- type:NormalExercise lang:python xp:100 skills:2 key:27858032c6
## SPARQL: Querying linked data


*** =instructions

*** =hint

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

```

*** =solution
```{python}

```

*** =sct
```{python}

```
