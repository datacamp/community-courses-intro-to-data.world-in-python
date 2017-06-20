---
title       : Working with datasets
description : Working with data.world datasets
attachments :

--- type:NormalExercise lang:python xp:100 skills:1 key:f29011ea21
## Working with datasets

Datasets on data.world can be referenced by their full URL, or as we saw in the previous exercise, a portion of the URL that makes it's unique path or dataset key. We could have just as easily used `https://data.world/stephen-hoover/chicago-city-council-votes` in place of `stephen-hoover/chicago-city-council-votes` when loading our dataset with `load_dataset()`. We'll use the full URL for the rest of the tutorial, but this shorter 'dataset key' will be good to know for queries and APIs later on.

Datasets on data.world start with one or more files (including tabular data, documentation, scripts, reports, etc) and they are enhanced by members with metadata, including a dataset summary, descriptions for files and columns and more. The describe() function of the dataset object can be used to review all the metadata that is downloaded with the dataset.

In addition, data.world will analyze the data and attempt to extract a schema for all tabular files (CSVs). Use the same `describe()` function to get the metadata for a particular table (csv resource) by passing it as a parameter.

*** =instructions
- Import the `datadotworld` module as `dw`
- Use the `load_dataset` method to assign `https://data.world/stephen-hoover/chicago-city-council-votes` to a `dataset` variable (notice that this time we're using the full URL).
- Use the `describe()` function of the dataset object to print all the metadata that is downloaded with the dataset.
- Use the same `describe()` function again, but now, use it to print a description of a specific resource: `alderman_votes`.

*** =hint
- Use `import ___ as ___` to import `datadotworld` as `dw`.
- Use `dataset = dw.load_dataset(___)` to import `https://data.world/stephen-hoover/chicago-city-council-votes`.
- Print the dataset's metadata with `pp.pprint(dataset.describe())`
- Use `pp.pprint(dataset.describe(_____))` to print the `alderman_votes` metadata

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
    f.write('auth_token = eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50OmRhdGFjYW1wc3R1ZGVudCIsImlzcyI6ImFnZW50OmRhdGFjYW1wc3R1ZGVudDo6MmMzMTM4Y2YtMGJjNy00N2FmLTg1MWItMGE1YmQ3ZTlhYjliIiwiaWF0IjoxNDkzMjI5NjMwLCJyb2xlIjpbInVzZXJfYXBpX3JlYWQiXSwiZ2VuZXJhbC1wdXJwb3NlIjp0cnVlfQ.ISiCSEd1Zb5Ot40-osANMnlab3K4IehWFeT-7qYvzccgzuUp7eSYLY7GGNsJIhJT_JYf_PFdQG3vcTnSRGt5hA')
    f.close()
```

*** =sample_code
```{python}
# Import the datadotworld module as dw


# Import the city council votes dataset
dataset = 

# Use describe() to review all the metadata that is downloaded with the dataset. 
# Print it to the screen using pp.pprint().
pp.pprint(___)

# Use describe() again to get a description of a specific resource: alderman_votes. Print it to the screen.

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

test_function("datadotworld.load_dataset", not_called_msg = "Be sure to call `dw.load_dataset()`.",
                             incorrect_msg = "You should call `dw.load_dataset()` as follows: `dw.load_dataset('https://data.world/stephen-hoover/chicago-city-council-votes')`.")

msg = "Make sure to print out the metadata for `dataset` like this: `pp.pprint(dataset.describe())`."
test_function("pprint.pprint", 1, incorrect_msg = msg)
test_function("dataset.describe", 1, incorrect_msg = msg)

msg = "Make sure to print out the metadata for the `alderman_votes` resource like this: `pp.pprint(dataset.describe('alderman_votes'))`."
test_function('pprint.pprint', index = 2, incorrect_msg = msg)
test_function("dataset.describe", 2, incorrect_msg = msg)

success_msg('Great work!')
```


--- type:MultipleChoiceExercise lang:python xp:50 skills:2 key:4c1d2c0e03
## Reading the metadata

We've assigned the output of the previous exercise to an `alderman_votes` variable: 

`alderman_votes = dataset.describe('alderman_votes')`

In the iPython shell to the right, print the value by typing `alderman_votes`.

Based on the output, how many fields does the `alderman_votes` resource have?

*** =instructions
- 1
- 3
- 5
- 16

*** =hint
- Each field is an element in the `fields` array within the `schema` element. Each field will be surrournded by `{}`.
- You can also use `len(alderman_votes['schema']['fields'])` to count the field elements. 

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
    f.write('auth_token = eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50OmRhdGFjYW1wc3R1ZGVudCIsImlzcyI6ImFnZW50OmRhdGFjYW1wc3R1ZGVudDo6MmMzMTM4Y2YtMGJjNy00N2FmLTg1MWItMGE1YmQ3ZTlhYjliIiwiaWF0IjoxNDkzMjI5NjMwLCJyb2xlIjpbInVzZXJfYXBpX3JlYWQiXSwiZ2VuZXJhbC1wdXJwb3NlIjp0cnVlfQ.ISiCSEd1Zb5Ot40-osANMnlab3K4IehWFeT-7qYvzccgzuUp7eSYLY7GGNsJIhJT_JYf_PFdQG3vcTnSRGt5hA')
    f.close()

# Import the datadotworld module as dw
import datadotworld as dw

# Import the city council votes dataset
dataset = dw.load_dataset('https://data.world/stephen-hoover/chicago-city-council-votes')

# Use the same describe() to get a description of a specific resource: alderman_votes
alderman_votes = dataset.describe('alderman_votes')

```

*** =sct
```{python}
msg1 = "Try again! Count each element within `'schema': {'fields': [` and `]}`. Each field will be surrounded by `{` and `}`"
msg2 = "Try again! Count each element within `'schema': {'fields': [` and `]}`. Each field will be surrounded by `{` and `}`"
msg3 = "Well done. Proceed to the next exercise"
msg4 = "Nope. Just count each element within `'schema': {'fields': [` and `]}`. Each field will be surrounded by `{` and `}`"
test_mc(correct = 3, msgs = (msg1,msg2,msg3,msg4))
```

--- type:NormalExercise lang:python xp:100 skills:2 key:943dd4c4ef
## Accessing the data

Now that you know how to load a dataset object and explore it's metadata, you'll have access to three properties that let you access the data: `raw_data`, `tables`, and `dataframes`. 

Each of these returns a dictionary of values, just in different formats: `bytes`, `list` and `pandas.DataFrame` objects, respectively. Use what makes sense for your use case, but note that not all files within a dataset on data.world are tabular, and therefore would only be returned with the `raw_data` response.

Let's practice creating a dataframe from a specific table in our dataset. Note that `datadotworld` is already imported and the `dataset` variable has been created with `load_dataset`:

*** =instructions
- Use the `dataframes` property to assign the `alderman_votes` table to the variable `votes_dataframe`.
- Explore the data by printing out the dataframe's `shape` and first 3 rows.

*** =hint
- Make sure to use brackets to request the resources to return. Ex. `dataset.dataframes[______]`
- Print the table's shape using `pp.pprint(____.shape)`
- Use `pp.pprint(_____.head(_))` to print the first 3 rows. 


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
    f.write('auth_token = eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJwcm9kLXVzZXItY2xpZW50OmRhdGFjYW1wc3R1ZGVudCIsImlzcyI6ImFnZW50OmRhdGFjYW1wc3R1ZGVudDo6MmMzMTM4Y2YtMGJjNy00N2FmLTg1MWItMGE1YmQ3ZTlhYjliIiwiaWF0IjoxNDkzMjI5NjMwLCJyb2xlIjpbInVzZXJfYXBpX3JlYWQiXSwiZ2VuZXJhbC1wdXJwb3NlIjp0cnVlfQ.ISiCSEd1Zb5Ot40-osANMnlab3K4IehWFeT-7qYvzccgzuUp7eSYLY7GGNsJIhJT_JYf_PFdQG3vcTnSRGt5hA')
    f.close()
```

*** =sample_code
```{python}
# The datadotworld module and dataset have already been loaded for you:
import datadotworld as dw
dataset = dw.load_dataset('https://data.world/stephen-hoover/chicago-city-council-votes')

# Use the dataframes property to assign the alderman_votes table to the variable votes_dataframe.
votes_dataframe = 

# Use the pandas shape property to get rows/columns size for the `votes_dataframe` dataframe.
pp.pprint(___)

# Use the pandas head function to print the first 3 rows of the `votes_dataframe` dataframe.

```

*** =solution
```{python}
# The datadotworld module and dataset have already been loaded for you:
import datadotworld as dw
dataset = dw.load_dataset('https://data.world/stephen-hoover/chicago-city-council-votes')

# Use the dataframes property to assign the alderman_votes table to the variable votes_dataframe.
votes_dataframe = dataset.dataframes['alderman_votes']

# Use the pandas shape property to get rows/columns size for the `votes_dataframe` dataframe.
pp.pprint(votes_dataframe.shape)

# Use the pandas head function to print the first 3 rows of the `votes_dataframe` dataframe.
pp.pprint(votes_dataframe.head(3))

```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

msg = "You should load the `alderman_votes` dataframe as follows: `dataset.dataframes['alderman_votes']`."
test_object("votes_dataframe", undefined_msg = msg, incorrect_msg = msg)

msg = "Print the shape of the dataframe using `pp.pprint(votes_dataframe.shape)`."
test_function("pprint.pprint", 1, incorrect_msg = msg)

msg = "Make sure to print out the first 3 rows of the dataframe using `pp.pprint(votes_dataframe.head(3))`"
test_function('pprint.pprint', 2, incorrect_msg = msg)
test_function("votes_dataframe.head", 1, incorrect_msg = msg)

success_msg('Great work!')
```
