---
title       : APIs
description : APIs
--- type:NormalExercise lang:python xp:100 skills:2 key:4501d1df41
## Saving your work


*** =instructions

The data.world python SDK also includes a variety of API wrapper functions that allow you to easily interface with our API endpoints. See the full documentation for the [data.world API](https://docs.data.world/documentation/api/), and access the wrappers through the `ApiClient` class. 

To obtain an instance, simply call `api_client()`:

`client = dw.api_client()`

Now let's walk through publishing your modified dataframe to your own data.world dataset:

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

```

*** =sct
```{python}

```
