---
title       : APIs
description : APIs
--- type:NormalExercise lang:python xp:100 skills:2 key:4501d1df41
## Saving your work

Now that you can pull data in from data.world, let see how to push your work back onto the platform for easy storage or sharing and collaborating with other members. 

The data.world Python SDK includes a variety of API wrappers, available via the `ApiClient` class, that let you create, replace, update, and delete a dataset. In this section, we’ll walk through a few common tasks:

- Use `api_client()` to get an instance of the `ApiClient`
- Create a dataset
- Add a file from a dataframe: we’ll write to a local csv and the upload the file
- Add a file from a source URL: this is an easy way to add external data to your dataset and keep it up to date. We’ll use a file from GitHub as an example, but you can use any URL source that points to a file.
- Sync the dataset: this simple call reloads any files with a source URL, to ensure the latest version.
- Update the dataset: after creating a dataset, use `update_dataset` to change attirbutes like description, summary or tags.

Use `help(api_client)` to learn more about each available function or see the full [data.world API documentation](https://docs.data.world/documentation/api/).

*** =instructions
- Create an `api_client` variable and assign it an instance of the ApiClient using `api_client()`.
- Use `create_dataset()` to create a dataset under the `datacampstudent` account named `yourname_datacamp` (use your name or handle!), with a `visibility` of `OPEN`
- Use the pandas `to_csv()` method to write the `police_shootings` dataframe to `police_shootings.csv`. Be sure to pass a `encoding='utf-8'` parameter
- Use the `upload_files()` method to upload `police_shootings.csv` to your dataset. Note that you'll use the unique path of the dataset rather than the full URL (`owner_id/title` you used in `create_dataset()`)


*** =hint
- Remember to use quotes around your parameter values.
- Create a local `police_shootings.csv` file using `_____.to_csv('police_shootings.csv', encoding='utf-8’)`
- Use the format `api_client.upload_files(['INSERT_DATASET_UNIQUE_PATH', ['INSERT_FILE_PATH'])`

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
# datadotworld module has been imported as dw and the `police_shootings` dataframe has been created for you
import datadotworld as dw
police_shootings = dw.load_dataset('https://data.world/jonloyens/intermediate-data-world').dataframes['fatal-police-shootings-data']

# Create an instance of the ApiClient using `api_client()` and assign it to a `api_client` variable
api_client = ____

# Use the `create_dataset()` method to create a dataset under the ‘datacampstudent’ account named ‘yourname_datacamp’ (use your name or handle!), with a `visibility` of ‘OPEN’
api_client.____(owner_id=____, title=____, visibility=____)

# Use the pandas to_csv() method to write the `police_shootings` dataframe to 'police_shootings.csv'. Be sure to pass a encoding='utf-8’ parameter

# Use the `upload_files()` method to upload `police_shootings.csv` to your dataset
_____.____(_____,[_____])
```

*** =solution
```{python}
# datadotworld module has been imported as dw and the `police_shootings` dataframe has been created for you
import datadotworld as dw
police_shootings = dw.load_dataset('https://data.world/jonloyens/intermediate-data-world').dataframes['fatal-police-shootings-data']


# Use the `create_dataset()` method to create a dataset under the ‘datacampstudent’ account named ‘yourname_datacamp’ (use your name or handle!), with a `visibility` of ‘OPEN’
api_client.create_dataset(owner_id='datacampstudent', title='rebecca_datacamp', visibility='OPEN')

# Use the pandas to_csv() method to write the `police_shootings` dataframe to 'police_shootings.csv'. Be sure to pass a encoding='utf-8’ parameter
police_shootings.to_csv('police_shootings.csv', encoding='utf-8’)

## Use the `upload_files()` method to upload `police_shootings.csv` to your dataset
api_client.upload_files('datacampstudent/rebecca_datacamp',['police_shootings.csv'])

```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

#test_function('pprint.pprint', index = 2)

success_msg('Great work!')

```

--- type:NormalExercise lang:python xp:100 skills:2 key:2c0317fd2f
## Updating your dataset

Now that you've created a dataset, lets modify it a bit...

*** =instructions
- Lets say we found some interesting data on GitHub, located at `https://github.com/fivethirtyeight/data/blob/master/police-deaths/all_data.csv`, that would be good to use in your data project. Use the `add_files_via_url()` method to upload it to your dataset as `shootings_of_police.csv`.
- After adding `shootings_of_police.csv` from the GitHub URL, you notice that the data has been updated. Use the `sync()` method to fetch the latest version.
- Your dataset is missing some crucial metadata. Use the `update_dataset()` method to add:
    - a dataset description: `Dataset created to test out the python SDK functionality.`
    - dataset tags: `test` and `datacamp`

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
# Use the `add_files_via_url()` method to upload 'https://github.com/fivethirtyeight/data/blob/master/police-deaths/all_data.csv’ to your dataset. Name the file ‘shootings_of_police.csv’.
____.____(____,{[INSERT_FILE_NAME: [INSERT_SOURCE_URL]})

# Call the `sync()` method to fetch the latest version of all files with a source URL


# Use the `update_dataset()` method to add a description and tags to your dataset


```

*** =solution
```{python}
# Use the `add_files_via_url()` method to upload 'https://github.com/fivethirtyeight/data/blob/master/police-deaths/all_data.csv’ to your dataset. Name the file ‘shootings_of_police.csv’.
api_client.add_files_via_url(‘datacampstudent/yourname_datacamp',{'shootings_of_police.csv': 'https://github.com/fivethirtyeight/data/blob/master/police-deaths/all_data.csv’})

# Call the `sync()` method to fetch the latest version of all files with a source URL
api_client.sync_files('datacampstudent/yourname_datacamp')

# Use the `update_dataset()` method to add a description and tags to your dataset
api_client.update_dataset('datacampstudent/yourname_datacamp', description='Dataset created to test out the python SDK functionality.', tags=['test', 'datacamp'])



```

*** =sct
```{python}
test_import('datadotworld', same_as = True)

#test_function('pprint.pprint', index = 2)

success_msg('Great work!')

```
