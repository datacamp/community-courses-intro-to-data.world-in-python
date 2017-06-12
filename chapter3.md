---
title       : Working with multiple datasets
description : Working with multiple datasets

--- type:NormalExercise lang:python xp:100 skills:2 key:be733d3f8a
## Working with multiple datasets

You can load as many different datasets as you’d like from data.world and work with them together. Here we’ve used the `load_dataset` method to bring in two separate datasets, assigning them each to a variable. 

We’ll leave it to you to create a dataframe for each using the `dataframe` property, and then merge the two dataframes together on the `state` and `STUSAB` fields. 

After merging them together, add a new `CityState` field to `police_shootings`, populating it with the concatenated values of the `city` and `STATE_NAME` fields, separated by `, ` resulting in a `city, state` format.


*** =instructions
- Create a `police_shootings` dataframe from the `fatal-police-shootings-data` table in `int_dataset`
- Create a `state_abbrvs` dataframe from the `StatesFIPSCodes` table in `fipsCodes_dataset`

*** =hint
- Add instructions here

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

# We've loaded two datasets to use 'int_dataset' and 'fipsCodes_dataset'
int_dataset = dw.load_dataset('https://data.world/jonloyens/intermediate-data-world')
fipsCodes_dataset = dw.load_dataset('https://data.world/uscensusbureau/fips-state-codes')

## Create two dataframes, police_shootings from the 'fatal-police-shootings-data' table of int_dataset and state_abbrvs, from the 'statesfipscodes' table of fipsCodes_dataset


## Merge full the two datasets together on the STUSAB and state fields


## Add a 'CityState' column to the police_shootings dataframe, populating it with the concatinated values from the 'city' and 'STATE_NAME' columns, separated by ', '. 


## Print head of dataframe

```

*** =solution
```{python}
# datadotworld module has been imported as dw
import datadotworld as dw

# We've loaded two datasets to use
int_dataset = dw.load_dataset('https://data.world/jonloyens/intermediate-data-world')
fipsCodes_dataset = dw.load_dataset('https://data.world/uscensusbureau/fips-state-codes')

# Create two dataframes, police_shootings from the 'fatal-police-shootings-data' table of int_dataset and state_abbrvs, from the 'statesfipscodes' table of fipsCodes_dataset
police_shootings = int_dataset.dataframes['fatal-police-shootings-data']
state_abbrvs = fipsCodes_dataset.dataframes['statesfipscodes']

## Merge full the two datasets together on the STUSAB and state fields
police_shootings = police_shootings.merge(state_abbrvs, how = 'left', left_on = 'state', right_on='STUSAB')

## Add a 'CityState' column to the police_shootings dataframe, populating it with the concatinated values from the 'city' and 'STATE_NAME' columns, separated by ', '. 
police_shootings["citystate"] = police_shootings["city"] + ", " + police_shootings["STATE_NAME"]

## Print head of dataframe
police_shootings.head(3)
```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

#test_function('pprint.pprint', index = 2)

success_msg('Great work!')
```
