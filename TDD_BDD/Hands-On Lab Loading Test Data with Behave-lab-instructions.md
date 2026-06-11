::page{title="Hands-on Lab: Loading Test Data with Behave"}

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/IDSN-logo.png" width="200">

**Estimated time needed:** 30 minutes

Welcome to the **Loading Test Data with Behave** lab. When you are writing Behavior Driven Development features, the scenarios will be better understood with relevant data that can be used for testing. You can specify the initial state of data before the tests using `feature` files. To implement this, you need to write some code to populate the database.

In this lab, you are going to see how to keep the initial state data in the `Background:` section of a feature file, and use a REST API to post that data to the service that is under test.

## Learning Objectives

After completing this lab, you will be able to:

- Parse the data from a table in a feature file
- Post that data to a REST API to create the initial state

::page{title="About Theia"}

Theia is an open-source Integrated Development Environment (IDE) that runs on a desktop or the cloud. You will use the Theia IDE to perform this lab. When you log into the Theia environment, you are presented with a 'dedicated computer on the cloud' exclusively for you. This is available to you as long as you work on the labs. Once you log off, this 'dedicated computer on the cloud' is deleted, along with any files you may have created. It is a good idea to finish your labs in a single session. If you finish part of the lab and return to the Theia lab later, you may have to start from the beginning. Plan to work out all your Theia labs when you have the time to finish the complete lab in a single session.

::page{title="Set Up the Lab Environment"}

You have to prepare the environment before you can start the lab. You need to open a terminal and install some system and Python dependencies.

## Open a Terminal

Open a terminal window by using the menu in the editor: Terminal > New Terminal.

In the terminal, if you are not already in the `/home/projects` folder, change to your project folder now.

```bash
cd /home/project
```

## Clone the Code Repo

Now get the code that you need to test. To do this, use the `git clone` command to clone the git repository:

```bash
git clone https://github.com/ibm-developer-skills-network/duwjx-tdd_bdd_PracticeCode.git
```

## Change into the Repo Folder

Next switch to the directory that contains the lab files.

```bash
cd /home/project/duwjx-tdd_bdd_PracticeCode
```

## Install Lab Dependencies

Once you have cloned the repository, you need to install some prerequisite software into the development environment.

```bash
bash ./bin/setup.sh
```

## Change into the Lab Folder

Then you should switch to the directory that contains the lab files.

```bash
cd /home/project/duwjx-tdd_bdd_PracticeCode/labs/10_loading_test_data
```

## Install Python Dependencies

The final preparation step is to use `pip` to install the Python packages needed for the lab:

```bash
pip install -r requirements.txt
```

You are now ready to start the lab.

### Optional

If working on the terminal becomes difficult because of the length of the command prompt, you can shorten the prompt using the following command:

```bash
export PS1="[\[\033[01;32m\]\u\[\033[00m\]: \[\033[01;34m\]\W\[\033[00m\]]\$ "
```


::page{title="Navigate to the Code"}

In the IDE, navigate to the `duwjx-tdd_bdd_PracticeCode/labs/10_loading_test_data` folder. This folder contains all the source code that you will use for this lab.

![Lab Folder](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/10_loading_test_data_folder.png "Lab Folder")

::page{title="Step 1: Create a Step"}

First create a step to add the code to load the data. As you learned in the video, all the steps should be placed in a folder named `steps` under the `features` folder.

While Behave does not care what you name the step files, it is recommended that you use names that let you know what each file contains. The folder already contains a file named `web_steps.py` which handles all web interactions. Since you are going to load data in this step, name the file `load_step.py`.

Open the `features/steps/load_steps.py` file in the IDE editor. You will work in this file for the remainder of the lab.

::openFile{path="/home/project/duwjx-tdd_bdd_PracticeCode/labs/10_loading_test_data/features/steps/load_steps.py"}

It already contains some initial setup code. You need to add the `step_impl()` implementation. The `petshop.feature` file bas the following `Background: ` statement:

```
Background:
    Given the following pets
```

## Your Task

Use the correct Python decorator from (`@given()`, `@when()`, `@then()`) to add a step that matches the statement "Given the following pets". Remember that all steps have the function name `step_impl()`. Don\'t forget to add a good docstring that describes what the step does.

<details>
	<summary>Click here for a hint.</summary>

```python
@given(...place a string here that matches...)
def step_impl(context):
    """...add a docstring that tells what this step does..."""
```

</details>

## Solution

<details>
	<summary>Click here for the solution.</summary>

This is the solution for adding the first step.

```python
@given('the following pets')
def step_impl(context):
    """Refresh all Pets in the database"""
```

</details>


::page{title="Step 2: Delete previous data"}

Next, you will write code to delete all existing pets in the database.

The petshop application has a REST API with an endpoint named `/pets`. If you make a call to `GET /pets` all pets will be returned with a status code of `200_OK`. If you make a call to `DELETE /pets/{id}` the pet with that `id` will be deleted with a status code of `204_NO_CONTENT`. Use the REST API to write code to delete all existing pets.

## REST API Information

The `BASE_URL` of the REST API endpoint is stored in a context variable called: `context.base_url`. This is the hostname of the server to send requests to.

You can get all pets in the database and store them in a variable called `response`  with the following REST API call:

```python
response = requests.get(f"{context.base_url}/pets")
```

You can check the status code of the `response` with:

```python
response.status_code
```

You can get the `json` that comes back from the `response` with:

```python
response.json()
```

You can delete a pet by getting the `pet['id']` from the `json` and using the `request.delete()` call as follows:

```python
requests.delete(f"{context.base_url}/pets/{pet['id']}")
```

With this information, you can now write the code to delete all pets in the databse.

## Your Task

Write code that implements the following steps:

1. Write a comment that describes that we are about to delete all pets
	<details>
		<summary>Click here for the solution.</summary>

	```python
		# List all pets and delete them one by one
	```
	</details>

1. Use the `requests` package to make a `get()` request to the `/pets` endpoint and store the results in a variable called `response`
	<details>
		<summary>Click here for the solution.</summary>

	```python
	    response = requests.get(f"{context.base_url}/pets")
	```
	</details>

1. `Assert` that the `status_code` of the `response` is `200`
	<details>
		<summary>Click here for the solution.</summary>

	```python
		assert response.status_code == 200
	```
	</details>

1. Create a `for` loop to iterate over `response.json()` to process each dictionary as the variable `pet`
	<details>
		<summary>Click here for the solution.</summary>

	```python
		for pet in response.json():
	```
	</details>

1. Inside the loop, make a `requests.delete()` call to the `/pets` endpoint passing in the URL to delete the pet by it\'s `id`.

	> _Hint:_ The call format is: `DELETE hostname/pets/{id}`

	<details>
		<summary>Click here for the solution.</summary>

	```python
			response = requests.delete(f"{context.base_url}/pets/{pet['id']}")
	```
	</details>

1. Still inside the loop, `assert` that the `status_code` from the delete is `204`
	<details>
		<summary>Click here for the solution.</summary>

	```python
			assert response.status_code == 204
	```
	</details>

## Solution

If you have done the steps correctly, your code should look like this solution:

<details>
	<summary>Click here for the solution.</summary>

This is the solution for deleting all pets in the database:

```python
    # List all of the pets and delete them one by one
    response = requests.get(f"{context.base_url}/pets")
    assert response.status_code == 200
    for pet in response.json():
        response = requests.delete(f"{context.base_url}/pets/{pet['id']}")
        assert response.status_code == 204

```

</details>


::page{title="Step 3: Load new data"}

Now it is time to load the new data from the table in the `Background:` statement into the database.  Remember from the video that the data from the `Background:` section will be returned in a variable named `context.table`. You can iterate over this table to get each row as a Python dictionary.

## REST API Information

The `BASE_URL` of the REST API endpoint is stored in a context variable called: `context.base_url`, This is the hostname of the server to send requests to.

The REST API only accepts `json` data which is similar to a Python dictionary.

You can create a pets dictionary in the database using a `POST` request and sending a `dict` using the `json=` parameter of the request. You can also store the result of the request in a variable called `response` to check the status code using the following REST API call:

```python
response = requests.post(f"{context.base_url}/pets", json=payload)
```

## Your Task

Write code that implements the following steps to process each row of data in this `Background:` statement:

```
Background:
    Given the following pets
        | name       | category | available | gender  | birthday   |
        | Fido       | dog      | True      | MALE    | 2019-11-18 |
        | Kitty      | cat      | True      | FEMALE  | 2020-08-13 |
        | Leo        | lion     | False     | MALE    | 2021-04-01 |
```

1. Write a comment that describes that we are about to create all of the new pets
	<details>
		<summary>Click here for the solution.</summary>

	```python
	    # load the database with new pets
	```
	</details>

1. Use a `for` loop to iterate the `context.table` structure to process each dictionary as the variable `row`
	<details>
		<summary>Click here for the solution.</summary>

	```python
	    for row in context.table:
	```
	</details>

1. Create a dictionary named `payload` that pulls out the keys `name`, `category`, `available`, `gender`, and `birthday` from each `row` of the table. Make sure to convert the `available` attributes into a boolean using the words `True`, `true`, and `1` as tests.
	<details>
		<summary>Click here for the solution.</summary>

	```python
			payload = {
				"name": row['name'],
				"category": row['category'],
				"available": row['available'] in ['True', 'true', '1'],
				"gender": row['gender'],
				"birthday": row['birthday']
			}
	```
	</details>

1. Inside the loop, make a `requests.post()` call to the `/pets` endpoint passing in the URL and the dictionary named `payload` as `json` data.

	> _Hint:_ The call format is: `DELETE hostname/pets/{id}`

	<details>
		<summary>Click here for the solution.</summary>

	```python
	        response = requests.post(f"{context.base_url}/pets", json=payload)
	```
	</details>

1. Still inside the loop, `assert` that the `status_code` from the post is `201`
	<details>
		<summary>Click here for the solution.</summary>

	```python
	        assert response.status_code == 201
	```
	</details>

## Solution

If all steps are correct, your code should look like this solution:

<details>
	<summary>Click here for the solution.</summary>

This is the solution for adding the data to the database via REST API calls:

```python
    # load the database with new pets
    for row in context.table:
        payload = {
            "name": row['name'],
            "category": row['category'],
            "available": row['available'] in ['True', 'true', '1'],
            "gender": row['gender'],
            "birthday": row['birthday']
        }
        response = requests.post(f"{context.base_url}/pets", json=payload)
        assert response.status_code == 201

```
</details>

::page{title="Step 4: Check your work"}

The final step function should look like this. If it does not, please correct it before proceeding:

```python
# pylint: disable=function-redefined, missing-function-docstring
# flake8: noqa
"""
Pet Steps
Steps file for Pet.feature
For information on Waiting until elements are present in the HTML see:
    https://selenium-python.readthedocs.io/waits.html
"""
import requests
from behave import given

# Load data here

@given('the following pets')
def step_impl(context):
    """Refresh all Pets in the database"""

    # List all pets and delete them one by one
    response = requests.get(f"{context.base_url}/pets")
    assert response.status_code == 200
    for pet in response.json():
        response = requests.delete(f"{context.base_url}/pets/{pet['id']}")
        assert response.status_code == 204

    # load the database with new pets
    for row in context.table:
        payload = {
            "name": row['name'],
            "category": row['category'],
            "available": row['available'] in ['True', 'true', '1'],
            "gender": row['gender'],
            "birthday": row['birthday']
        }
        response = requests.post(f"{context.base_url}/pets", json=payload)
        assert response.status_code == 201

```


::page{title="Step 5: Run behave"}

Now it is time to run the `behave` command and see if everything is working properly.

## Your Task

Run `behave` from the lab folder in the terminal:

```bash
behave
```

The output should look like this:

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/10-behave-output.png)


::page{title="Conclusion"}

Congratulations! You just completed the **Loading Test Data with Behave** lab. You should now have the skills to take any test data that is specoified in the `Background:` section of a feature file and load it into the service under test using a REST API.

Your next challenge is to apply these techniques in your projects to load test data as the initial state of your Behavior Driven Development tests.

## Author(s)

[John J. Rofrano](https://www.linkedin.com/in/johnrofrano)

## Contributors

## Changelog

| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2023-04-06 | 1.0 | J. Rofrano | Create new lab |
| 2023-04-11 | 1.1 | J. Rofrano | Minor updates |
| 2023-07-19 | 1.2 | Mercedes Schneider | QA with Edits | 
|   |   |   |   |

<h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>
