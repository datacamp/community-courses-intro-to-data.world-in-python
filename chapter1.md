---
title       : Introduction
description : Introduction to data.world
attachments :

--- type:NormalExercise lang:python xp:100 skills:1 key:f29011ea21
## Introduction

Hello and welcome to the intro to data.world tutorial! At data.world, we're building the most meaningful, collaborative, and abundant data resource in the world by breaking down the barriers between data and people. Join data.world to find interesting data and understand it at a glance, store and showcase your own data and data projects, as well as find and collaborate with others. 

Open data is at the heart of data.world, and as such we want to make it as easy as possible to use data.world data in your environment of choice so you can do your work easier and solve real problems faster. 

Which brings us to this tutorial where you’ll learn the different ways to connect to data.world using our Python SDK. The data.world Python SDK will help you to easily load data, explore metadata, query datasets and even push your work back to data.world for storage and sharing. 

Learn more at [https://data.world/integrations/python](https://data.world/integrations/python) and let’s start with the basics of loading the `datadotworld` library and pulling in a dataset to kick things off….

*** =instructions
- Import the `datadotworld` module as `dw`
- Use the `load_dataset` method to assign `stephen-hoover/chicago-city-council-votes` to a `dataset` variable.

*** =hint
- Just fill in the blanks with the provided values:
- Use `import ___ as ___` to import `datadotworld` as `dw`.
- Use `dataset = dw.load_dataset(___)` to import `stephen-hoover/chicago-city-council-votes`. Don't forget apostrophes around the dataset value! 

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
import ___ as ___

# Import the city council votes dataset
dataset = dw.___(___)
```

*** =solution
```{python}
# Import the datadotworld module as dw
import datadotworld as dw

# Import the city council votes dataset
dataset = dw.load_dataset('stephen-hoover/chicago-city-council-votes')
```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

test_function("datadotworld.load_dataset", not_called_msg = "Be sure to call `dw.load_dataset()`.",
                             incorrect_msg = "You should call `dw.load_dataset()` as follows: `dw.load_dataset('stephen-hoover/chicago-city-council-votes')`.")

success_msg('Great work!')
```
