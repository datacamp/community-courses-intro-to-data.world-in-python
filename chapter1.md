---
title       : Introduction
description : Introduction to data.world
attachments :

--- type:NormalExercise lang:python xp:100 skills:1 key:f29011ea21
## Introduction

Hello and welcome to the intro to data.world tutorial! At data.world, we're building the most meaningful, collaborative, and abundant data resource in the world by breaking down the barriers between data and people. Join data.world to find interesting data and understand it at a glance, store and showcase your own data and data projects, as well as find and collaborate with others. 

Open data is at the heart of data.world, and as such we want to make it as easy as possible to use data.world data in your environment of choice, so that you can do your work easier and solve real problems faster. Which brings us to this tutorial where you’ll learn how to work with data.world using Python.

We’ll walk through the different ways to connect to data.world and the basic functionality in our Python SDK. Let’s start with some basics to kick things off….

*** =instructions
- Import the `datadotworld` module as `dw`
- Use the `load_dataset` method to assign `stephen-hoover/chicago-city-council-votes` to a `dataset` variable.
- Use the `describe()` function of the dataset object to print all the metadata that is downloaded with the dataset.

*** =hint
- You don't have to program anything for the first instruction, just take a look at the first line of code.
- Use `import ___ as ___` to import `datadotworld` as `dw`.
- Use `dataset = dw.load_dataset(___)` to import `stephen-hoover/chicago-city-council-votes`.
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
import ___ as ___

# Import the city council votes dataset
dataset = dw.___(___)

# Use describe() to review all the metadata that is downloaded with the dataset
pp.pprint(dataset.___)
```

*** =solution
```{python}
# Import the datadotworld module as dw
import datadotworld as dw

# Import the city council votes dataset
dataset = dw.load_dataset('stephen-hoover/chicago-city-council-votes')

# Use describe() to review all the metadata that is downloaded with the dataset
pp.pprint(dataset.describe())
```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

test_function('pprint.pprint', index = 2)

success_msg('Great work!')
```
