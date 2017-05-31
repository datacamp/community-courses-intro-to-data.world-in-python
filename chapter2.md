---
title       : Working with datasets
description : Working with data.world datasets
attachments :

--- type:NormalExercise lang:python xp:100 skills:1 key:f29011ea21
## Working with datasets

Datasets on data.world are identified by their URL (e.g. https://data.world/stephen-hoover/chicago-city-council-votes). More simply, they can be identified by their unique path, in this case: stephen-hoover/chicago-city-council-votes.
To get started, import the datadotworld module as dw and use the load_dataset() function to load the dataset and assign the result to a variable called dataset.

Datasets on data.world start with one or more files (including tabular data, documentation, scripts, reports, etc) and they are enhanced by users with metadata, including summary, descriptions for files and columns and more.
Use the describe() function of the dataset object to review all the metadata that is downloaded with the dataset.

In addition, data.world will analyze the data and attempt to extract a schema for all tabular files.
Use the same describe() function again, but now, try to get a description of a specific resource: alderman_votes.

*** =instructions
- Import the datadotworld module as dw
- Use the describe() function of the dataset object to review all the metadata that is downloaded with the dataset.
- Use the same describe() function again, but now, try to get a description of a specific resource: alderman_votes.

*** =hint
- You don't have to program anything for the first instruction, just take a look at the first line of code.
- Use `import ___ as ___` to import `matplotlib.pyplot` as `plt`.
- Use `plt.scatter(___, ___, c = ___)` for the third instruction.
- You'll always have to type in `plt.show()` to show the plot you created.

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
import datadotworld as __

# Import the city council votes dataset
dataset = dw.load_dataset('https://data.world/stephen-hoover/chicago-city-council-votes')

# Use describe() to review all the metadata that is downloaded with the dataset
pp.pprint(dataset.describe())

# Use describe() again to get a description of a specific resource: alderman_votes
pp.pprint(dataset.describe(___))
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

