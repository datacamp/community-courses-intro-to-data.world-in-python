---
title       : Working with multiple datasets
description : Working with multiple datasets

--- type:NormalExercise lang:python xp:100 skills:2 key:be733d3f8a
## Working with multiple datasets

You can load as many different datasets as you’d like from data.world and work with them together. Here we’ve used the `load_dataset` method to bring in two separate datasets, assigning them each to a variable. 

We’ll leave it to you to create a dataframe for each using the `dataframes` property, and then merge the two dataframes together on the `state` and `STUSAB` fields. 

After merging them together, add a new `citystate` field to your merged dataset, populating it with the concatenated values of the `city` and `STATE_NAME` fields, separated by `, ` resulting in a `city, state` format.


*** =instructions
- Create a `police_shootings` dataframe from the `fatal-police-shootings-data` table in `int_dataset`
- Create a `state_abbrvs` dataframe from the `statesfipscodes` table in `fipsCodes_dataset`
- Merge the two dataframes together on the `state` and `STUSAB` fields using the merge() function. Assign to `merged_dataframe`.
- Add a `citystate` column to your merged dataframe, populating it with the concatinated values from the `city` and `STATE_NAME` columns, separated by ', '. 
- Print first 5 rows of merged dataframe

*** =hint
- Make sure to use brackets to request the resources to return. Ex. `police_shootings = int_dataset.dataframes[____]`
- Merge the datasets with `police_shootings.merge(____, how = 'left', left_on = ___, right_on=___)`
- Create the new `citystate` field using `____["citystate"] = ____["city"] + "__" + ____["STATE_NAME"]`
- Print the first 5 rows using the `head()` function using `pp.pprint`.

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
# datadotworld module has been imported as dw
import datadotworld as dw

# We've loaded two datasets to use 'int_dataset' and 'fipsCodes_dataset'
int_dataset = dw.load_dataset('https://data.world/jonloyens/intermediate-data-world')
fipsCodes_dataset = dw.load_dataset('https://data.world/uscensusbureau/fips-state-codes')

## Create two dataframes: police_shootings from the 'fatal-police-shootings-data' table of int_dataset and state_abbrvs, from the 'statesfipscodes' table of fipsCodes_dataset


## Merge the two datasets together on the state and STUSAB fields. Assign to a merged_dataframe variable.
merged_dataframe = ___


## Add a 'citystate' column to the merged_dataframe dataframe, populating it with the concatinated values from the 'city' and 'STATE_NAME' columns, separated by ', '. 

## Print first 5 rows of merged_dataframe


```

*** =solution
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

# We've loaded two datasets to use
int_dataset = dw.load_dataset('https://data.world/jonloyens/intermediate-data-world')
fipsCodes_dataset = dw.load_dataset('https://data.world/uscensusbureau/fips-state-codes')

# Create two dataframes: police_shootings from the 'fatal-police-shootings-data' table of int_dataset and state_abbrvs, from the 'statesfipscodes' table of fipsCodes_dataset
police_shootings = int_dataset.dataframes['fatal-police-shootings-data']
state_abbrvs = fipsCodes_dataset.dataframes['statesfipscodes']

## Merge the two datasets together on the state and STUSAB fields. Assign to a merged_dataframe variable.
merged_dataframe = police_shootings.merge(state_abbrvs, how = 'left', left_on = 'state', right_on='STUSAB')

## Add a 'citystate' column to the merged_dataframe dataframe, populating it with the concatinated values from the 'city' and 'STATE_NAME' columns, separated by ', '. 
merged_dataframe["citystate"] = merged_dataframe["city"] + ", " + merged_dataframe["STATE_NAME"]

## Print head of merged_dataframe
pp.pprint(merged_dataframe.head(5))


```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

msg = "Create the `police_shootings` dataframe using `int_dataset.dataframes['fatal-police-shootings-data']`"
test_object("police_shootings", undefined_msg = msg, incorrect_msg = msg)

msg = "Create the `state_abbrvs` dataframe using `fipsCodes_dataset.dataframes['statesfipscodes']`"
test_object("state_abbrvs", undefined_msg = msg, incorrect_msg = msg)

msg = "Create the `merged_dataframe` dataframe with `police_shootings.merge(state_abbrvs, how = 'left', left_on = 'state', right_on='STUSAB')`"
test_object("merged_dataframe", undefined_msg = msg, incorrect_msg = msg)

msg = "Print the first 5 rows of the `merged_dataframe` using `pp.pprint(merged_dataframe.head(5))`"
test_function('pprint.pprint', 1, incorrect_msg = msg, not_called_msg = msg)
test_function("merged_dataframe.head", 1, incorrect_msg = msg)

success_msg('Great work!')
```
