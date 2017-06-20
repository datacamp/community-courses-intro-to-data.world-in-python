---
title       : Wrap up & next steps
description : Setup your own data.world account and apply what you've learned and more!

--- type:NormalExercise lang:python xp:100 skills:2 key:d55f0708ee
## Wrap up & next steps

Congrats! You now know multiple ways of pulling data from data.world into your local environment using our Python SDK. But don't stop there! The Python SDK has additional functionality for uploading and modifying data for easy storage as well as sharing and collaborating with other members. 

data.world is completely free, so signup at [https://data.world/](https://data.world/) and start applying your new skills. We've also put together a handy jupyter notebook with all of the things we've covered in this tutorial, as well as some of the more advanced functionality. 

Download the notebook [here](https://query.data.world/s/59dlfssv3zwf1k2l8k18gg9z3), and follow the below steps for installing the data.world Python SDK on your machine:

1 ) Install data.world's Python package, including optional `pandas` dependencies:

`pip install datadotworld[pandas]`

2 ) Run the dw command-line tool to configure your machine:

`dw configure`

3 ) Copy/Paste in your data.world API token when prompted. Find your token at [https://data.world/settings/advanced](https://data.world/settings/advanced)

We've also included one final code example here that shows some more ways to inspect a dataset, so check it out and just click submit to finish the course. We hope you enjoyed it!

*** =instructions
- Setup your data.world account at `https://data.world/`.
- Install the datadotworld Python package to your local machine using `pip install datadotworld[pandas]`.
- Download the [jupyter notebook](https://query.data.world/s/59dlfssv3zwf1k2l8k18gg9z3) to quickly apply the things you've learned in this tutorial.
- Use data.world to find more interesting data, store and share your own data and projects, and collaborate with other community members!
- Just click submit to complete the course.

*** =hint
- The exercise is complete example code, so no work is needed! Just review and click submit to finish the course.

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
# Import the datadotworld module as dw and the sys module
import datadotworld as dw
import sys

# Import a dataset
refugee_dataset = dw.load_dataset('nrippner/refugee-host-nations')

# Get the size of the dataset:
sys.getsizeof(refugee_dataset)

# List all of the data files:
dataframes = refugee_dataset.dataframes
for df in dataframes:
    pp.pprint(df)
    
# print all of the files in a dataset:
resources = refugee_dataset.describe()['resources']
pp.pprint('name:')
for r in resources:
    pp.pprint(r['name'])
pp.pprint('\ntype of file:')
for r in resources:
    pp.pprint(r['format'])

```

*** =solution
```{python}
# Import the datadotworld module as dw and the sys module
import datadotworld as dw
import sys

# Import a dataset
refugee_dataset = dw.load_dataset('nrippner/refugee-host-nations')

# Get the size of the dataset:
sys.getsizeof(refugee_dataset)

# List all of the data files:
dataframes = refugee_dataset.dataframes
for df in dataframes:
    pp.pprint(df)
    
# print all of the files in a dataset:
resources = refugee_dataset.describe()['resources']
pp.pprint('name:')
for r in resources:
    pp.pprint(r['name'])
pp.pprint('\ntype of file:')
for r in resources:
    pp.pprint(r['format'])
```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

success_msg('Great work! Congrats on completing the course!')
```
