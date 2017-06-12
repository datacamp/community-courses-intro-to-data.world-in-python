---
title       : Working with datasets
description : Working with data.world datasets
attachments :

--- type:NormalExercise lang:python xp:100 skills:1 key:f29011ea21
## Working with datasets

Datasets on data.world can be referenced by their full URL, or as we saw in the previous exercise, a portion of the URL that makes it's unique path. We could have just as easily used `https://data.world/stephen-hoover/chicago-city-council-votes` in place of `stephen-hoover/chicago-city-council-votes` when loading our dataset with `load_dataset()`. We'll use the full URL for the rest of the tutorial, but this shorter 'table id' will be good to know for queries later on.

Datasets on data.world start with one or more files (including tabular data, documentation, scripts, reports, etc) and they are enhanced by users with metadata, including a dataset summary, descriptions for files and columns and more. The describe() function of the dataset object can be used to review all the metadata that is downloaded with the dataset.

In addition, data.world will analyze the data and attempt to extract a schema for all tabular files (CSVs). Use the same `describe()` function to get the metadata for a particular csv file by passing it as a parameter.

*** =instructions
- Import the `datadotworld` module as `dw`
- Use the `load_dataset` method to assign `https://data.world/stephen-hoover/chicago-city-council-votes` to a `dataset` variable (notice that this time we're using the full URL).
- Use the `describe()` function of the dataset object to print all the metadata that is downloaded with the dataset.
- Use the same `describe()` function again, but now, use it to get a description of a specific resource: `alderman_votes`.

*** =hint
- You don't have to program anything for the first instruction, just take a look at the first line of code.
- Use `import ___ as ___` to import `datadotworld` as `dw`.
- Use `dataset = dw.load_dataset(___)` to import `https://data.world/stephen-hoover/chicago-city-council-votes`.
- Print the dataset's metadata with `pp.pprint(dataset.describe())`

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
# Import the datadotworld module as dw


# Import the city council votes dataset
dataset = 

# Use describe() to review all the metadata that is downloaded with the dataset. 
# Print it to the screen using pp.print().
pp.pprint(___)

# Use describe() again to get a description of a specific resource: alderman_votes

```

*** =solution
```{python}
# Import the datadotworld module as dw
import datadotworld as dw

# Import the city council votes dataset
dataset = dw.load_dataset('https://data.world/stephen-hoover/chicago-city-council-votes')

# Use describe() to review all the metadata that is downloaded with the dataset
pp.pprint(dataset.describe())

# Use the same describe() to get a description of a specific resource: alderman_votes
pp.pprint(dataset.describe('alderman_votes'))
```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

test_function('pprint.pprint', index = 2)

success_msg('Great work!')
```


--- type:MultipleChoiceExercise lang:python xp:50 skills:2 key:4c1d2c0e03
## Reading the metadata

Based on the output from the previous exercise, how many fields does the `alderman_votes` resource have?

*** =instructions
- 1
- 3
- 5
- 16

*** =hint
Each field is an element in the `fields` array within the `schema` element. Each field will be surrournded by `{}`.

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

# Import the datadotworld module as dw
import datadotworld as dw

# Import the city council votes dataset
dataset = dw.load_dataset('https://data.world/stephen-hoover/chicago-city-council-votes')

# Use the same describe() to get a description of a specific resource: alderman_votes
pp.pprint(dataset.describe('alderman_votes'))

```

*** =sct
```{python}
msg1 = "Try again! Count each element within `'schema': {'fields': [` and `]}`. Each field will be surrounded by `{` and `}`"
msg2 = "Note that each field element can have a different number of attributes."
msg3 = "Well done. Proceed to the next exercise"
test_mc(correct = 3, msgs = (msg1,msg2,msg3))
```

--- type:NormalExercise lang:python xp:100 skills:2 key:943dd4c4ef
## Accessing the data

Now that you know how to load a dataset object, you'll have access to three properties that let you access the data: `raw_data`, `tables`, and `dataframes`. 

Each of these returns a dictionary of values, just in different formats: `bytes`, `list` and `pandas.DataFrame` objects, respectively. Use what makes sense for your use case, but note that not all files within a dataset on data.world are tabular, and therefore would only be returned with the `raw_data` response.

Let's practice creating a dataframe from a specific table in our dataset. Note that `datadotworld` is already imported and the `dataset` variable has been created with `load_dataset`:

*** =instructions
- Use the `dataframes` property to assign the `alderman_votes` table to the variable `votes_dataframe`.
- Explore the data by printing out the dataframe's `shape` and first 3 rows.

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
# The datadotworld module and dataset have already been loaded for you:
import datadotworld as dw
dataset = dw.load_dataset('https://data.world/stephen-hoover/chicago-city-council-votes')

# Use the dataframes property to assign the alderman_votes table to the variable votes_dataframe.
votes_dataframe = 

# Use the pandas shape property to get rows/columns size.
pp.pprint(___)

# Use the pandas head function to print the first 3 rows.

```

*** =solution
```{python}
# The datadotworld module and dataset have already been loaded for you:
import datadotworld as dw
dataset = dw.load_dataset('https://data.world/stephen-hoover/chicago-city-council-votes')

# Use the dataframes property to assign the alderman_votes table to the variable votes_dataframe.
votes_dataframe = dataset.dataframes['alderman_votes']

# Use the pandas shape property to get rows/columns size.
pp.pprint(votes_dataframe.shape)

# Use the pandas head function to print the first 3 rows.
votes_dataframe.head(3)

```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

test_function('pprint.pprint', index = 1)

success_msg('Great work!')
```
