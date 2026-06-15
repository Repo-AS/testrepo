::page{title="TDD / BDD Final Project (Option A: Python)"}

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/IDSN-logo.png" width="200"> <br>

**Estimated time:** 60 minutes 

Welcome to the **TDD / BDD Final Project** development environment. Now it\'s time to prove to yourself that you can apply the learning from the Test Driven Development and Behavior Driven Development modules of this course. This lab environment will provide you with a Cloud IDE and Docker which will enable you to carry out the following objectives:

## Objectives

- Develop unit test cases for a Product model
- Develop unit test cases and code for a RESTful API for products
- Load background data from your BDD scenarios into your service before each scenario executes
- Develop a feature file to test the Product administrative UI with Behave

All of your work on the final project should be completed from this environment.

::page{title="Note:"}

1.  Please ensure that all updates and changes made during each task are properly completed and saved before proceeding to the next steps.
    
2.  As mentioned in the _“Final Project Overview”_, you can submit your project deliverables through either Option 1: AI-Graded Submission and Evaluation or Option 2: Peer-Graded Submission and Evaluation.
    
3.  **For Option 1: AI-Graded Submission and Evaluation:**  
    Submission requires:

    -   **Code snippets** for all activities under **Tasks 1 to 7**.
        
4.  **For Option 2: Peer-Graded Submission and Evaluation:**
    
    -   **GitHub repository URL** for all activities under **Tasks 1 to 7**.

::page{title="Important Security Information"}

Welcome to the Cloud IDE with Docker. This is where all of your development will take place. It has all of the tools you will need to use Docker.

It is important to understand that the lab environment is **ephemeral**. It only lives for a short while and then it will be destroyed. This makes it imperative that you push all changes made to your own GitHub repository so that it can be recrated in a new lab environment any time it is needed.

Also note that this environment is shared and therefore not secure. You should not store any personal information, usernames, passwords, or access tokens in this environments for any purposes.

## Your Task

1. If you haven't generated a **GitHub Personal Access Token** you should do so now. You will need it to push code back to your repository. It should have `repo` and `write` permissions, and set to expire in `60` days. When Git prompts you for a password in the Cloud IDE environment, use your Personal Access Token instead.

1. The environment may be recreated at any time so you may find that you have to perform the **Initialize Development Environment** each time the environment is created.

1. Create a repository from the GitHub template provided for this lab in the next step.

::page{title="Create your own GitHub Repository"}

You will need your own repository to complete the final project. We have provided GitHub Template repository to create your own repository in your own GitHub account. No need to Fork it as it has been set up as a Template. This will avoid confusion when making Pull Requests in the future.

## Your Task

1. In a browser, visit this GitHub repository:
	https://github.com/ibm-developer-skills-network/xgcyk-tdd-bdd-final-project-template

1. From the GitHub **Code** tab, press the green **Use this template** button to create your own repository from this template.

1. Select **Create a new repository** from the dropdown menu

On the next screen, fill out these prompts following the screenshot below:

![Create Repository](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/final-create-repository.png "Create Repository")

1. Select your GitHub account from the dropdown list

1. Name the new repository: `tdd-bdd-final-project` 
>Note: The repository name must remain the same and should not be changed.

1. (Optional) Add a nice description to let people know what this repo is for

1. Make the repo **Public** so that others can see if (and grade it)

1. Press the **Create repository from template** button to create the repository in the GitHub account you have selected.

Note: These steps only need to be done once. Whenever you re-enter this lab, you should start from the next page: **Initialize Development Environment**

::page{title="Initialize Development Environment"}

As previously covered, the Cloud IDE with Docker environment is ephemeral, and may be deleted at any time. The next time you come into the lab, a new environment may be created. Unfortunately, this means that you will need to initialize your development environment every time it is recreated. This shouldn't happen too often as the environment can last for several days at a time but when it is removed, this is the procedure to recreate it.

## Overview

Each time you need to set up your lab development environment, you will need to run three commands.

Each command will be explained in further detail, one at a time, in the following section.

 `{your_github_account}` represents your GitHub account username.

The commands include:

```
git clone https://github.com/{your_github_account}/tdd-bdd-final-project.git
cd tdd-bdd-final-project
bash ./bin/setup.sh
exit
```

Now, let's discuss each of these commands and explain what needs to be done.

## Task Details

Initialize your environment using the following steps:

1. Open a terminal with `Terminal` -> `New Terminal` if one isn\'t open already.

1. Next, use the `export GITHUB_ACCOUNT=` command to export an environment variable that contains the name of your GitHub account.
> Note: Substitute your real GitHub account that you used to create the repository, for the `{your_github_account}` place holder below:

	```text
	export GITHUB_ACCOUNT={your_github_account}
	```

1. Then use the following commands to clone your repository, change into the `devops-capstone-project` directory, and execute the `./bin/setup.sh` command.

	```bash
	git clone https://github.com/$GITHUB_ACCOUNT/tdd-bdd-final-project.git
	cd tdd-bdd-final-project
	bash ./bin/setup.sh
	```

	You should see the follow at the end of the setup execution:

	
	![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/Final%20Setup%20Complete.jpg)

1. Finally, use the `exit` command to close the current terminal. The environment won\'t be fully active until you open a new terminal in the next step.

	```bash
	exit
	```

## Validate

In order to validate that your environment is working correctly, you must open a new terminal because the Python virtual environment will only activate when a new terminal is created. You should have ended the previous task by using the `exit` command to exit the terminal.

1. Open a terminal with `Terminal` -> `New Terminal` and check that everything worked correctly by using the `which python` command:

	Your prompt should look like this:

	
	![Setup Prompt](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/Setup%20Prompt.jpg "Setup Prompt")

	Check which Python you are using:
	```bash
	which python
	```

	You should get back:

	![Which Python](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/Which%20Python.jpg "Which Python")

	Check the Python version:
	```bash
	python --version
	```

	You should get back some patch level of Python 3.8:

	![Python Version](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/Python%20Version.jpg)

This completes the setup of the development environment. Anytime your environment is recreated, you will need to follow this procedure.

You are now ready to start working.

::page{title="Final Project Scenario"}

You have been asked by the product catalog manager at your company to develop an Product microservice to build a catalog for your e-commerce website. The user interface (UI) has been developed by another team and will be used by product administrators to maintain the product catalog. Since it is a microservice, it is expected to have a well-formed REST API that the UI and other microservices can call. This service initially needs the ability to create, read, update, delete, and list products by various attributes.

You have also been informed that someone else has started on this project and has already developed the database model and a Python Flask-based REST API with an endpoint to **create** products. You will already have this code in your copy of the repository.

In the first part of this project you will use good **Test Driven Development** practices to create a **REST API** that allows users to Create, Read, Update, Delete, and List products by various attributes. As mentioned, the Create implementation and tests will be provided for you to use as an example for your code.

In the second part of this project you will write **Behavior Driven Development** scenarios to test that the administrative user interface, which has been provided for you, behaves as expected. The scenario for **Create** is already implemented. You will also need to write code to load the background data, and more scenarios to fill out the allowed actions.

Good Luck!

::page{title="Exercise 1: Create Fake Products"}

### Update the ProductFactory class

Open the `service/models.py` file to familiarize yourself with the attributes of the `Product` class. These are the same attributes that you will need to add to the `ProductFactory` class in the `tests/factories.py` file.

::openFile{path="/home/project/tdd-bdd-final-project/service/models.py"}

Open the `tests/factories.py` file in the IDE editor. This is the file in which you will add the attributes of the `Product` class to the `ProductFactory` class.

::openFile{path="/home/project/tdd-bdd-final-project/tests/factories.py"}

## Your Task

In the `tests/factories.py` file, use the **Faker** providers and **Fuzzy** attributes to create fake data for the `name`, `description`, `price`, `available`, and `category` fields by adding them to the `ProductFactory` class.

You can also refer to the video  [Factories and Fakes](https://www.coursera.org/learn/test-and-behavior-driven-development-tdd-bdd/lecture/1Ywjz/factories-and-fakes) and the lab [Using Factories and Fakes](https://www.coursera.org/learn/test-and-behavior-driven-development-tdd-bdd/ungradedLti/KAbA4/using-factories-and-fakes) in case you want to familiarise yourself with the concepts before proceeding further.

<details>

<summary>Click here for a hint.</summary>

1. Use the **FuzzyChoice** attribute to create random choices of products for the `name` field such as Hat,Pants,Shirt,Apple,Banana,Pots,Towels,Ford,Chevy,Hammer,Wrench

2. Use **faker** to get a fake `text` for the `description` field

3. Use the **FuzzyDecimal** attribute with 0.5, 2000.0, 2 as options for the `price` field

4. Use the **FuzzyChoice** attribute with True / False as the choices for the `available` field

5. Use the **FuzzyChoice** attribute to create random choices of categories such as UNKNOWN,CLOTHS,FOOD,HOUSEWARES,AUTOMOTIVE,TOOLS for the `category` field

</details>

## Solution

<details>
	<summary>Click here for the solution.</summary>

In `factories.py`, update the code below and please be sure to indent properly.

```python
class ProductFactory(factory.Factory):
    """Creates fake products for testing"""

    class Meta:
        """Maps factory to data model"""

        model = Product

    id = factory.Sequence(lambda n: n)
    name = FuzzyChoice(
        choices=[
	        "Hat",
	        "Pants",
	        "Shirt",
	        "Apple",
	        "Banana",
	        "Pots",
	        "Towels",
	        "Ford",
	        "Chevy",
	        "Hammer",
	        "Wrench"
	    ]
    )
    description = factory.Faker("text")
    price = FuzzyDecimal(0.5, 2000.0, 2)
    available = FuzzyChoice(choices=[True, False])
    category = FuzzyChoice(
        choices=[
            Category.UNKNOWN,
            Category.CLOTHS,
            Category.FOOD,
            Category.HOUSEWARES,
            Category.AUTOMOTIVE,
            Category.TOOLS,
        ]
    )
```

</details>

Now you can move on to writing test cases for the model.

::page{title="Exercise 2: Create Test Cases for the Model"}

Before we proceed with creating test cases for the Product Model, let us see the different attributes used in this model:

| Attribute  | Description   |
| ------------ | ------------ |
| id | The id of the product |
| name | The name of the product |
| description | The description of the product |
| price | The price of the product |
| available | True if the product is available, otherwise False |
| category | The category under which the product belongs |

Please refer to the Reading: About the Product Model (include link to the course reading) to understand the classes and methods used in the models.py file.

The first thing you need to do while creating test cases for the Model, is ensure that the database model is working correctly. Someone wrote all of the code but only wrote a test case for create. You have no idea if the other functions work properly or not.

## Your Task

Create test cases in `tests/test_models.py` to exercise the code in `service/models.py` to test that the `Product` model works.

1. Write test case to **read** a product and ensure that it passes
1. Write test case to **update** a product and ensure that it passes
1. Write test case to **delete** a product and ensure that it passes
1. Write test case to **list all** products
1. Write test case to search for a product by **name** and ensure that it passes
1. Write test case to search for a product by **category** and ensure that it passes
1. Write test case to search for a product by **availability** and ensure that it passes

::openFile{path="/home/project/tdd-bdd-final-project/tests/test_models.py"}

**Note:** To open in file explorer go to the location:

`/home/project/tdd-bdd-final-project/tests/test_models.py`

### Test Case to Read a Product

1. Create a `Product` object using the `ProductFactory`
2. Add a log message displaying the `product` for debugging errors
3. Set the ID of the `product` object to `None` and then create the product.
4. Assert that the `product ID` is not None
5. Fetch the product back from the database
6. Assert the properties of the found product are correct

Overall, this test case should verify if the reading functionality of the Product class is working correctly. It should create a product, assign it an ID, save it to the system, retrieve it back using the ID, and verify that the retrieved product has the same properties as the original product.

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test reading an product:

```python
    def test_read_a_product(self):
        """It should Read a Product"""
        product = ProductFactory()
        # Set the ID of the product object to None and then call the create() method on the product.
        # Assert that the ID of the product object is not None after calling the create() method.
        # Fetch the product back from the system using the product ID and store it in found_product
        # Assert that the properties of the found_product match with the properties of the original product object, such as id, name, description and price.
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for reading a product:

```python
    def test_read_a_product(self):
        """It should Read a Product"""
        product = ProductFactory()
        product.id = None
        product.create()
        self.assertIsNotNone(product.id)
        # Fetch it back
        found_product = Product.find(product.id)
        self.assertEqual(found_product.id, product.id)
        self.assertEqual(found_product.name, product.name)
        self.assertEqual(found_product.description, product.description)
        self.assertEqual(found_product.price, product.price)
```

</details>

### Test Case to Update a Product

1. Create a `Product` object using the `ProductFactory`
2. Add a log message displaying the `product` for debugging errors
3. Set the ID of the `product` object to `None` and create the product.
4. Log the `product` object again after it has been created to verify that the product was created with the desired properties.
5. Update the description property of the `product` object.
6. Assert that that the `id` and `description` properties of the `product` object have been updated correctly.
7. Fetch all products from the database to verify that after updating the product, there is only one product in the system.
8. Assert that the fetched product has the original id but updated description.

Overall, this test case should verify if the update functionality of the Product class is working correctly. It should create a product, save it to the system, update its properties, verify the updated properties, fetch the product back from the system, and confirm that the fetched product has the updated properties.

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test updating an product:

```python
    def test_update_a_product(self):
        """It should Update a Product"""
        product = ProductFactory()
        # Set the ID of the product object to None and then call the create() method on the product.
        # Log the product object again after it has been created to verify that the product was created with the desired properties.
        # Assert that the ID of the product object is not None after calling the create() method.
        # Update the product in the system with the new property values using the update() method.
        # Assert that the id is same as the original id but description property of the product object has been updated correctly after calling the update() method.
        # Fetch all the product back from the system.
        # Assert the length of the products list is equal to 1 to verify that after updating the product, there is only one product in the system.
        # Assert that the fetched product has id same as the original id.
        # Assert that the fetched product has the updated description.
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for updating a product:

```python
   def test_update_a_product(self):
        """It should Update a Product"""
        product = ProductFactory()
        product.id = None
        product.create()
        self.assertIsNotNone(product.id)
        # Change it an save it
        product.description = "testing"
        original_id = product.id
        product.update()
        self.assertEqual(product.id, original_id)
        self.assertEqual(product.description, "testing")
        # Fetch it back and make sure the id hasn't changed
        # but the data did change
        products = Product.all()
        self.assertEqual(len(products), 1)
        self.assertEqual(products[0].id, original_id)
        self.assertEqual(products[0].description, "testing")
```

</details>

### Test Case to Delete a Product

1. Create a `Product` object using the `ProductFactory` and save it to the database.
2. Assert that after creating a product and saving it to the database, there is only one product in the system.
3. Remove the product from the database.
4. Assert if the product has been successfully deleted from the database.

Overall, this test case should verify if the deletion functionality of the Product class is working correctly. It should create a product, save it to the database, delete it, and verify that the product is no longer present in the database.

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test deleting an product:

```python
    def test_delete_a_product(self):
        """It should Delete a Product"""
        product = ProductFactory()
        # Call the create() method on the product to save it to the database.
        # Assert  if the length of the list returned by Product.all() is equal to 1, to verify that after creating a product and saving it to the database, there is only one product in the system.
        # Call the delete() method on the product object, to remove the product from the database.
        # Assert if the length of the list returned by Product.all() is now equal to 0, indicating that the product has been successfully deleted from the database.

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for deleting a product:

```python
    def test_delete_a_product(self):
        """It should Delete a Product"""
        product = ProductFactory()
        product.create()
        self.assertEqual(len(Product.all()), 1)
        # delete the product and make sure it isn't in the database
        product.delete()
        self.assertEqual(len(Product.all()), 0)
```

</details>

### Test Case to List all Products

1. Retrieve all products from the database and assign them to the products variable.
2. Assert there are no products in the database at the beginning of the test case.
3. Create five products and save them to the database.
4. Fetching all products from the database again and assert the count is 5

Overall, this test case should verify if the listing functionality of the Product class is working correctly. It should check that initially there are no products, create five products, and confirm that the count of the retrieved products matches the expected count of 5.

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test listing all products:

```python
    def test_list_all_products(self):
        """It should List all Products in the database"""
        products = Product.all()
        # Assert if the products list is empty, indicating that there are no products in the database at the beginning of the test case.
        # Use for loop to create five Product objects using a ProductFactory() and call the create() method on each product to save them to the database.
        # Fetch all products from the database again using product.all()
        # Assert if the length of the products list is equal to 5, to verify that the five products created in the previous step have been successfully added to the database.

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for listing a product:

```python
    def test_list_all_products(self):
        """It should List all Products in the database"""
        products = Product.all()
        self.assertEqual(products, [])
        # Create 5 Products
        for _ in range(5):
            product = ProductFactory()
            product.create()
        # See if we get back 5 products
        products = Product.all()
        self.assertEqual(len(products), 5)
```

</details>

### Test Case to Find a Product by Name

1. Create a batch of 5 Product objects using the ProductFactory and save them to the database.
2. Retrieve the name of the first product in the products list
3. Count the number of occurrences of the product name in the list
4. Retrieve products from the database that have the specified name.
5. Assert if the count of the found products matches the expected count.
6. Assert that each product's name matches the expected name.

Overall, this test case should verify if the `Product.find_by_name()` method correctly retrieves products from the database based on their name, by creating a batch of products, saving them to the database, finding products by name, and verifying that the count and names of the found products match the expected values.

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test finding a product by name:

```python
    def test_find_by_name(self):
        """It should Find a Product by Name"""
        products = ProductFactory.create_batch(5)
        # Use a for loop to iterate over the products list and call the create() method on each product to save them to the database.
        # Retrieve the name of the first product in the products list.
        # Use a list comprehension to filter the products based on their name and then use len() to calculate the length of the filtered list, and use the variable called count to hold the number of products that match the name.
        # Call the find_by_name() method on the Product class to retrieve products from the database that have the specified name.
        # Assert if the count of the found products matches the expected count.
        # Use a for loop to iterate over the found products and assert that each product's name matches the expected name, to ensure that all the retrieved products have the correct name.

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for finding a product by name

```python
     def test_find_by_name(self):
        """It should Find a Product by Name"""
        products = ProductFactory.create_batch(5)
        for product in products:
            product.create()
        name = products[0].name
        count = len([product for product in products if product.name == name])
        found = Product.find_by_name(name)
        self.assertEqual(found.count(), count)
        for product in found:
            self.assertEqual(product.name, name)
```

</details>

### Test Case to Find a Product by Availability

1. Create a batch of 10 Product objects using the ProductFactory and save them to the database.
2. Retrieve the availability of the first product in the products list
3. Count the number of occurrences of the product availability in the list
4. Retrieve products from the database that have the specified availability.
5. Assert if the count of the found products matches the expected count.
6. Assert that each product\'s availability matches the expected availability.

Overall, this test case should verify if the `Product.find_by_availability()` method correctly retrieves products from the database based on their availability, by creating a batch of products, saving them to the database, finding products by availability, and verifying that the count and availability of the found products match the expected values.

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test finding a product based on its availability:

```python
    def test_find_by_availability(self):
        """It should Find Products by Availability"""
        products = ProductFactory.create_batch(10)
        # Use a for loop to iterate over the products list and call the create() method on each product to save them to the database.
        # Retrieve the availability of the first product in the products list.
        # Use a list comprehension to filter the products based on their availability and then use len() to calculate the length of the filtered list, and use the variable called count to hold the number of products that have the specified availability.
        # Call the find_by_availability() method on the Product class to retrieve products from the database that have the specified availability.
        # Assert if the count of the found products matches the expected count.
        # Use a for loop to iterate over the found products and assert that each product's availability matches the expected availability, to ensure that all the retrieved products have the correct availability.

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for finding a product based on its availability:

```python
      def test_find_by_availability(self):
        """It should Find Products by Availability"""
        products = ProductFactory.create_batch(10)
        for product in products:
            product.create()
        available = products[0].available
        count = len([product for product in products if product.available == available])
        found = Product.find_by_availability(available)
        self.assertEqual(found.count(), count)
        for product in found:
            self.assertEqual(product.available, available)
```

</details>

### Test Case to Find a Product by Category

1. Create a batch of 10 Product objects using the ProductFactory and save them to the database.
2. Retrieve the category of the first product in the products list
3. Count the number of occurrences of the product that have the same category in the list.
4. Retrieve products from the database that have the specified category.
5. Assert if the count of the found products matches the expected count.
6. Assert that each product\'s category matches the expected category.

Overall, this test case should verify if the `Product.find_by_category()` method correctly retrieves products from the database based on their category, by creating a batch of products, saving them to the database, finding products by category, and verifying that the count and categories of the found products match the expected values.

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test finding a product based on its category:

```python
    def test_find_by_availability(self):
        """It should Find Products by Category"""
        products = ProductFactory.create_batch(10)
        # Use a for loop to iterate over the products list and call the create() method on each product to save them to the database.
        # Retrieve the category of the first product in the products list.
        # Use a list comprehension to filter the products based on their category and then use len() to calculate the length of the filtered list, and use the variable called count to hold the number of products that have the specified category.
        # Call the find_by_category() method on the Product class to retrieve products from the database that have the specified category.
        # Assert if the count of the found products matches the expected count.
        # Use a for loop to iterate over the found products and assert that each product's category matches the expected category, to ensure that all the retrieved products have the correct category.

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for finding a product based on its category:

```python
      def test_find_by_category(self):
        """It should Find Products by Category"""
        products = ProductFactory.create_batch(10)
        for product in products:
            product.create()
        category = products[0].category
        count = len([product for product in products if product.category == category])
        found = Product.find_by_category(category)
        self.assertEqual(found.count(), count)
        for product in found:
            self.assertEqual(product.category, category)
```

</details>

## Acceptance Criteria

- Ensure that all tests pass when you run `nosetests`, and maintain at least 95% code coverage.
- There should be no linting errors when you run `make lint`

::page{title="REST API Guidelines Review"}

For your review, these are the guidelines for creating REST APIs that enable you to write the test cases for this lab:

## RESTful API Endpoints

| Action | Method | Return code    | Body                        | URL Endpoint            |
|--------|--------|----------------|-----------------------------|-------------------------|
| List   | GET    | 200_OK         | Array of products `[{...}]` | `GET  /products`        |
| Create | POST   | 201_CREATED    | A product as json `{...}`  | `POST /products`        |
| Read   | GET    | 200_OK         | A product as json `{...}`  | `GET  /products/{id}`   |
| Update | PUT    | 200_OK         | A product as json `{...}`  | `PUT  /products/{id}`   |
| Delete | DELETE | 204_NO_CONTENT | `""`                        | `DELETE /products/{id}` |

Following these guidelines, you can make assumptions about how to call the web service and assert what it should return.

## HTTP Status Codes

Here are some other HTTP status codes that you will need for this lab:

| Code | Status              | Description |
|------|---------------------|-------------|
|  200 | HTTP_200_OK         | Success |
|  201 | HTTP_201_CREATED    | The requested resource has been created |
|  204 | HTTP_204_NO_CONTENT | There is no further content |
|  404 | HTTP_404_NOT_FOUND  | Could not find the resource requested |
|  405 | HTTP_405_METHOD_NOT_ALLOWED | Invalid HTTP method used on an endpoint |
|  409 | HTTP_409_CONFLICT   | There is a conflict with your request |

All of these codes are defined in `service/common/status.py` and are already imported for your use.

::page{title="Exercise 3: Create Test Cases and Code for REST API"}

Now that you know that the model is working, you can move on to developing the REST API which will accept `json` requests, call the model, and return an answer as `json`.

Your REST API must implement the following endpoints:

- Create a Product
- Read a Product
- Update a Product
- Delete a Product
- List all Products
- List Products by Category, Availability, and Name

Note: The Create endpoint is already implemented for you and should serve as an example. Also, there is only one List endpoint that takes optional parameters to filter the data.

## Your Task

Edit the test cases in `tests/test_routes.py` and code in `service/routes.py` for a RESTful endpoint using Flask that contains the following endpoints:

1. Write a test case to **Read** a Product and watch it fail
1. Write the code to make the Read test case pass
1. Write a test case to **Update** a Product and watch it fail
1. Write the code to make the Update test case pass
1. Write a test case to **Delete** a Product and watch it fail
1. Write the code to make the Delete test case pass
1. Write a test case to **List all** Products and watch it fail
1. Write the code to make the List all test case pass
1. Write a test case to **List by name** a Product and watch it fail
1. Write the code to make the List by name test case pass
1. Write a test case to **List by category** a Product and watch it fail
1. Write the code to make the List by category test case pass
1. Write a test case to **List by availability** a Product and watch it fail
1. Write the code to make the List by availability test case pass

Following test driven development, you write a test case to assert that the code you are about to write will have the correct behavior as expected.

### Task 1:  Write a Test Case to **Read** a Product

Write the test case in tests/test_routes.py for **Reading a Product**

::openFile{path="/home/project/tdd-bdd-final-project/tests/test_routes.py"}

**Note:** To open in file explorer go to the location:

`/home/project/tdd-bdd-final-project/tests/test_routes.py`

1. Create a test case called `test_get_product(self)`.
1. Use the `_create_products()` method to create one product, and then assign the first product from the returned list to the `test_product` variable.
1. Make a `GET` request to the API endpoint to retrieve the product and construct the URL by appending the `test_product.id` to the `BASE_URL`.
1. Assert that the return code was `HTTP_200_OK`, to verify that the request was successful and the product was retrieved.
1. Check the `json` that was returned and `assert` that it is equal to the data that you sent.
1. Run `nosetests` and watch it fail because there is no code yet.

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test read a product:

```python
    def test_get_product(self):
         """It should Get a single Product"""
        # get the id of a product
        test_product = self._create_products(1)[0]
        # make a self.client.get request to the API endpoint and store the result in the variable named response
        # assert that the resp.status_code is status.HTTP_200_OK
        # get the data from resp.get_json()
        # assert that data["name"] equals the test_product.name
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for read a product:

```python
    def test_get_product(self):
        """It should Get a single Product"""
        # get the id of a product
        test_product = self._create_products(1)[0]
        response = self.client.get(f"{BASE_URL}/{test_product.id}")
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        data = response.get_json()
        self.assertEqual(data["name"], test_product.name)

```

</details>

### Task 2: Write the Code to make the **Read** Test case pass

Once you have a test case, you can begin to write the code in service/routes.py to make it pass.

::openFile{path="/home/project/tdd-bdd-final-project/service/routes.py"}

**Note:** To open in file explorer go to the location:

`/home/project/tdd-bdd-final-project/service/routes.py`

1. Create a Flask route that responds to the `GET` method for the endpoint `/products/<product_id>`.
1. Create a function called `get_products(product_id)` to hold the implementation.
1. Call the `Product.find()` method which will return a product with the given `product_id`.
1. Abort with a return code `HTTP_404_NOT_FOUND` if the product was not found.
1. Call the `serialize()` method on a product to serialize it to a Python dictionary.
1. Send the serialized data and a return code of `HTTP_200_OK` back to the caller.
1. Run `nosetests` until all of the tests are `green`, which means they passed.

<details>
    <summary>Click here for a hint.</summary>
Here is a starter code for the REST API to read a product:

```python
######################################################################
# READ A PRODUCT
######################################################################
@app.route("/products/<int:product_id>", methods=["GET"])
def get_products(product_id):
    """
    Retrieve a single Product

    This endpoint will return a Product based on it's id
    """
    app.logger.info("Request to Retrieve a product with id [%s]", product_id)

    # use the Product.find() method to find the product
    # abort() with a status.HTTP_404_NOT_FOUND if it cannot be found
    # return the serialize() version of the product with a return code of status.HTTP_200_OK

    return {the product as json here + 200}
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete REST API implementation for reading a product:

```python
######################################################################
# READ A PRODUCT
######################################################################
@app.route("/products/<int:product_id>", methods=["GET"])
def get_products(product_id):
    """
    Retrieve a single Product

    This endpoint will return a Product based on it's id
    """
    app.logger.info("Request to Retrieve a product with id [%s]", product_id)

    product = Product.find(product_id)
    if not product:
        abort(status.HTTP_404_NOT_FOUND, f"Product with id '{product_id}' was not found.")

    app.logger.info("Returning product: %s", product.name)
    return product.serialize(), status.HTTP_200_OK

```

</details>

### Maintain Code Coverage

You must maintain code coverage of **95%** or greater. You will not achieve this by only testing the happy paths. The test case you wrote probably did not test for a product that was not found, so you will need to write another test case that reads a product with an product id that does not exist. This should get your test coverage back up to where it needs to be.

1. Create a test case called `test_get_product_not_found(self):`.
1. Make a `self.client.get()` call to `/products/{id}` passing in an invalid product id `0`
1. Assert that the return code was `HTTP_404_NOT_FOUND`.
1. Run `nosetests` and fix the code in `test_routes.py` until it passes.

<details>
    <summary>Click here for a hint.</summary>
Here is starter code for a product not found:

```python
    def test_get_product_not_found(self):
        """It should not Get a Product thats not found"""
        # send a self.client.get() request to the BASE_URL with an invalid product ID (e.g., 0)
        # assert that the resp.status_code is status.HTTP_404_NOT_FOUND
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for reading a product that was not found:

```python
    def test_get_product_not_found(self):
        """It should not Get a Product thats not found"""
        response = self.client.get(f"{BASE_URL}/0")
        self.assertEqual(response.status_code, status.HTTP_404_NOT_FOUND)
        data = response.get_json()
        self.assertIn("was not found", data["message"])

```

</details>

## Acceptance Criteria

- Ensure that all tests pass when you run `nosetests`, and maintain at least 95% code coverage.
- There should be no linting errors when you run `make lint`

::page{title="TDD Hints and Solutions"}

This page contains the remaining hints and solutions for the **Update**, **Delete** , **List all** , **List By Name**, **List By Category**, **List By Availability** REST APIs, now that you have implemented **Read**.

## Update

First write a test for the **Update** function:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test update a product:

```python
    def test_update_product(self):
         """It should Update an existing Product"""
        # create a product to update
        test_product = ProductFactory()
        # send a self.client.post() request to the BASE_URL with a json payload of test_product.serialize()
        # assert that the resp.status_code is status.HTTP_201_CREATED
        # UPDATE THE PRODUCT
        # get the data from resp.get_json() as new_product
        # change new_account["description"] to unknown
        # send a self.client.put() request to the BASE_URL with a json payload of new_product
        # assert that the resp.status_code is status.HTTP_200_OK
        # get the data from resp.get_json() as updated_product
        # assert that the updated_product["description"] is whatever you changed it to
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for update a product:

```python
    def test_update_product(self):
        """It should Update an existing Product"""
        # create a product to update
        test_product = ProductFactory()
        response = self.client.post(BASE_URL, json=test_product.serialize())
        self.assertEqual(response.status_code, status.HTTP_201_CREATED)

        # update the product
        new_product = response.get_json()
        new_product["description"] = "unknown"
        response = self.client.put(f"{BASE_URL}/{new_product['id']}", json=new_product)
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        updated_product = response.get_json()
        self.assertEqual(updated_product["description"], "unknown")
```

</details>
<br>

Now write the code to make the **Update** test case pass:

<details>
    <summary>Click here for a hint.</summary>
Here is a starter code for the REST API for update a product:

```python
######################################################################
# UPDATE AN EXISTING PRODUCT
######################################################################
@app.route("/products/<int:product_id>", methods=["PUT"])
def update_products(product_id):
    """
    Update an Product
    This endpoint will update a Product based on the body that is posted
    """
    app.logger.info("Request to Update a product with id [%s]", product_id)
    check_content_type("application/json")

    # use the Product.find() method to retrieve the product by the product_id
    # abort() with a status.HTTP_404_NOT_FOUND if it cannot be found
    # call the deserialize() method on the product passing in request.get_json()
    # call product.update() to update the product with the new data
    # return the serialize() version of the product with a return code of status.HTTP_200_OK

    return {product as json + 200}
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete REST API implementation for update a product:

```python
######################################################################
# UPDATE AN EXISTING PRODUCT
######################################################################
@app.route("/products/<int:product_id>", methods=["PUT"])
def update_products(product_id):
    """
    Update a Product

    This endpoint will update a Product based the body that is posted
    """
    app.logger.info("Request to Update a product with id [%s]", product_id)
    check_content_type("application/json")

    product = Product.find(product_id)
    if not product:
        abort(status.HTTP_404_NOT_FOUND, f"Product with id '{product_id}' was not found.")

    product.deserialize(request.get_json())
    product.id = product_id
    product.update()
    return product.serialize(), status.HTTP_200_OK

```

</details>

## Delete

First write a test for the **Delete** function:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test delete a product:

```python
    def test_delete_product(self):
        """It should Delete a Product"""

        # create a list products containing 5 products using the _create_products() method. 
        products = self._create_products(5)
        # call the self.get_product_count() method to retrieve the initial count of products before any deletion
        # assign the first product from the products list to the variable test_product
        # send a self.client.delete() request to the BASE_URL with test_product.id
        # assert that the resp.status_code is status.HTTP_204_NO_CONTENT
        # check if the response data is empty 
        # send a self.client.get request to the same endpoint that was deleted to retrieve the deteled product
        # assert that the resp.status_code is status.HTTP_404_NOT_FOUND to confirm deletion of the product
        # retrieve the count of products after the deletion operation
        # check if the new count of products is one less than the initial count

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for delete a product:

```python
    def test_delete_product(self):
        """It should Delete a Product"""
        products = self._create_products(5)
        product_count = self.get_product_count()
        test_product = products[0]
        response = self.client.delete(f"{BASE_URL}/{test_product.id}")
        self.assertEqual(response.status_code, status.HTTP_204_NO_CONTENT)
        self.assertEqual(len(response.data), 0)
        # make sure they are deleted
        response = self.client.get(f"{BASE_URL}/{test_product.id}")
        self.assertEqual(response.status_code, status.HTTP_404_NOT_FOUND)
        new_count = self.get_product_count()
        self.assertEqual(new_count, product_count - 1)
```

</details>

Now write the code to make the **Delete** test case pass:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code for the REST API for delete a product:

```python
######################################################################
# DELETE A PRODUCT
######################################################################
@app.route("/products/<int:product_id>", methods=["DELETE"])
def delete_products(product_id):
    """
    Delete a Product

    This endpoint will delete a Product based the id specified in the path
    """
    app.logger.info("Request to Delete a product with id [%s]", product_id)

    # use the Product.find() method to retrieve the product by the product_id
    # if found, call the delete() method on the product
    # return and empty body ("") with a return code of status.HTTP_204_NO_CONTENT

    return {empty string + 204}
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete REST API implementation for delete a product:

```python
######################################################################
# DELETE A PRODUCT
######################################################################
@app.route("/products/<int:product_id>", methods=["DELETE"])
def delete_products(product_id):
    """
    Delete a Product

    This endpoint will delete a Product based the id specified in the path
    """
    app.logger.info("Request to Delete a product with id [%s]", product_id)

    product = Product.find(product_id)
    if product:
        product.delete()

    return "", status.HTTP_204_NO_CONTENT

```

</details>

## List All

First write a test for the **List All** function:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test the list for all products:

```python
    def test_get_product_list(self):
        """It should Get a list of Products"""
        self._create_products(5)
        # send a self.client.get() request to the BASE_URL
        # assert that the resp.status_code is status.HTTP_200_OK
        # get the data from resp.get_json()
        # assert that the len() of the data is 5 (the number of products you created)
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for list all products:

```python
    def test_get_product_list(self):
        """It should Get a list of Products"""
        self._create_products(5)
        response = self.client.get(BASE_URL)
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        data = response.get_json()
        self.assertEqual(len(data), 5)
```

</details>
<br>

Now write the code to make the **List All** test case pass:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code for the REST API for list all products:

```python
######################################################################
# LIST PRODUCTS
######################################################################
@app.route("/products", methods=["GET"])
def list_products():
    """Returns a list of Products"""
    app.logger.info("Request to list Products...")

    # use the Product.all() method to retrieve all products
    # create a list of serialize() products
    # log the number of products being returned in the list 
    # return the list with a return code of status.HTTP_200_OK

    return {list of products as json here + 200}
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete REST API implementation for list all products:

```python
######################################################################
# LIST PRODUCTS
######################################################################
@app.route("/products", methods=["GET"])
def list_products():
    """Returns a list of Products"""
    app.logger.info("Request to list Products...")

    products = Product.all()

    results = [product.serialize() for product in products]
    app.logger.info("[%s] Products returned", len(results))
    return results, status.HTTP_200_OK
```

</details>

## List By Name

First write a test for the **List By Name** function:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test the List By Name function:

```python
    def test_query_by_name(self):
        """It should Query Products by name"""
        products = self._create_products(5)
        # extract the name of the first product in the products list and assigns it to the variable test_name
        # count the number of products in the products list that have the same name as the test_name
        # send an HTTP GET request to the URL specified by the BASE_URL variable, along with a query parameter "name"
        # assert that response status code is 200, indicating a successful request (HTTP 200 OK)
        # retrieve the JSON data from the response
        # assert that the length of the data list (i.e., the number of products returned in the response) is equal to name_count
        # use a for loop to iterate through the products in the data list and checks if each product's name matches the test_name
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for List By Name function:

```python
    def test_query_by_name(self):
        """It should Query Products by name"""
        products = self._create_products(5)
        test_name = products[0].name
        name_count = len([product for product in products if product.name == test_name])
        response = self.client.get(
            BASE_URL, query_string=f"name={quote_plus(test_name)}"
        )
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        data = response.get_json()
        self.assertEqual(len(data), name_count)
        # check the data just to be sure
        for product in data:
            self.assertEqual(product["name"], test_name)
```

</details>
<br>

> Note: Please import `quote_plus` by including the below line in the `test_routes.py` to ensure the `query by name` test case passes. Please add it above `import app`

```from urllib.parse import quote_plus```

Now write the code to make the **List By Name** test case pass:

> Note: List by name is an extension of List All. You are going to add a filter to the code that lists all products to check if the `name` parameter has been passed in and filter by name if it is, and return all if it doesn't:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code for the REST API for List By Name function:

```python
######################################################################
# LIST PRODUCTS
######################################################################
@app.route("/products", methods=["GET"])
def list_products():
    """Returns a list of Products"""
    app.logger.info("Request to list Products...")

    # Initialize an empty list to hold the products.
    # Get the `name` parameter from the request (hint: use `request.args.get()`
    # test to see if you received the "name" query parameter
    # If you did, call the Product.find_by_name(name) method to retrieve products that match the specified name
    # If you didn't call list all
    products = Product.all()

    results = [product.serialize() for product in products]
    app.logger.info("[%s] Products returned", len(results))
    return results, status.HTTP_200_OK

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete REST API implementation for List By Name function:

```python
######################################################################
# LIST PRODUCTS
######################################################################
@app.route("/products", methods=["GET"])
def list_products():
    """Returns a list of Products"""
    app.logger.info("Request to list Products...")

    products = []
    name = request.args.get("name")

    if name:
        app.logger.info("Find by name: %s", name)
        products = Product.find_by_name(name)
    else:
        app.logger.info("Find all")
        products = Product.all()

    results = [product.serialize() for product in products]
    app.logger.info("[%s] Products returned", len(results))
    return results, status.HTTP_200_OK

```

</details>

## List By Category

First write a test for the **List By Category** function:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test the List By Category function:

```python
    def test_query_by_category(self):
        """It should Query Products by category"""
        products = self._create_products(10)
        # retrieves the category of the first product in the products list and assigns it to the variable category
        # create a list named found, containing products from the products list whose category matches the category variable
        # check the count of products match the specified category and assign it to the variable found_count
        # Log a debug message indicating the count and details of the products found
        # send an HTTP GET request to the URL specified by the BASE_URL variable, along with a query parameter "category"
        # assert that response status code is 200, indicating a successful request (HTTP 200 OK)
        # retrieve the JSON data from the response
        # assert that the length of the data list (i.e., the number of products returned in the response) is equal to found_count
        # use a for loop to check each product in the data list and verify that all returned products belong to the queried category
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for List By Category function:

```python
    def test_query_by_category(self):
        """It should Query Products by category"""
        products = self._create_products(10)
        category = products[0].category
        found = [product for product in products if product.category == category]
        found_count = len(found)
        logging.debug("Found Products [%d] %s", found_count, found)

        # test for available
        response = self.client.get(BASE_URL, query_string=f"category={category.name}")
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        data = response.get_json()
        self.assertEqual(len(data), found_count)
        # check the data just to be sure
        for product in data:
            self.assertEqual(product["category"], category.name)
```

</details>
<br>

Now write the code to make the **List By Category** test case pass:

> Note: List by Category is an extension of List All. You are going to add a filter to the code that lists all products to check if the `category` parameter has been passed in and filter by category if it is, and return all if it doesn't:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code for the REST API for List By Category function:

```python
######################################################################
# LIST PRODUCTS
######################################################################
@app.route("/products", methods=["GET"])
def list_products():
    """Returns a list of Products"""
    app.logger.info("Request to list Products...")

    products = []
    name = request.args.get("name")
    # Get the `category` parameter from the request (hint: use `request.args.get()`

    if name:
        app.logger.info("Find by name: %s", name)
        products = Product.find_by_name(name)

    # test to see if you received the "category" query parameter
    # If you did, convert the category string retrieved from the query parameters to the corresponding enum value from the Category enumeration
    # call the Product.find_by_category(category_value) method to retrieve products that match the specified category_value

    else:
        app.logger.info("Find all")
        products = Product.all()

    results = [product.serialize() for product in products]
    app.logger.info("[%s] Products returned", len(results))
    return results, status.HTTP_200_OK

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete REST API implementation for List By Category function:

```python
######################################################################
# LIST PRODUCTS
######################################################################
@app.route("/products", methods=["GET"])
def list_products():
    """Returns a list of Products"""
    app.logger.info("Request to list Products...")

    products = []
    name = request.args.get("name")
    category = request.args.get("category")

    if name:
        app.logger.info("Find by name: %s", name)
        products = Product.find_by_name(name)
    elif category:
        app.logger.info("Find by category: %s", category)
        # create enum from string
        category_value = getattr(Category, category.upper())
        products = Product.find_by_category(category_value)
    else:
        app.logger.info("Find all")
        products = Product.all()

    results = [product.serialize() for product in products]
    app.logger.info("[%s] Products returned", len(results))
    return results, status.HTTP_200_OK

```

</details>

> Note: Please import `Category` from `service.models` by including the below line in the `routes.py` to ensure the `query by category` test case passes.

```from service.models import Product, Category```

## List By Availability

First write a test for the **List By Availability** function:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to test the List By Availability function:

```python
    def test_query_by_availability(self):
        """It should Query Products by availability"""
        products = self._create_products(10)
        # list named available_products is initialized to store the products based on their availability status
        # store the  count of available products.
        # Log a debug message indicating the count and details of the available products
        # send an HTTP GET request to the URL specified by the BASE_URL variable, along with a query parameter "available" set to true.
        # assert that response status code is 200, indicating a successful request (HTTP 200 OK)
        # retrieve the JSON data from the response
        # assert that the length of the data list (i.e., the number of products returned in the response) is equal to available_count
        # use a for loop to check each product in the data list and verify that the "available" attribute of each product is set to True
```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete test case for List By Availability function:

```python
    def test_query_by_availability(self):
        """It should Query Products by availability"""
        products = self._create_products(10)
        available_products = [product for product in products if product.available is True]
        available_count = len(available_products)        
        # test for available
        response = self.client.get(
            BASE_URL, query_string="available=true"
        )
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        data = response.get_json()
        self.assertEqual(len(data), available_count)
        # check the data just to be sure
        for product in data:
            self.assertEqual(product["available"], True)
```

</details>
<br>

Now write the code to make the **List By Availability** test case pass:

> Note: List by Availability is an extension of List All. You are going to add a filter to the code that lists all products to check if the `available` parameter has been passed in and filter by available if it is, and return all if it doesn't:

<details>
    <summary>Click here for a hint.</summary>
Here is starter code for the REST API for List By Availability function:

```python
######################################################################
# LIST PRODUCTS
######################################################################
@app.route("/products", methods=["GET"])
def list_products():
    """Returns a list of Products"""
    app.logger.info("Request to list Products...")

    products = []
    name = request.args.get("name")
    category = request.args.get("category")
    # Get the `available` parameter from the request (hint: use `request.args.get()`

    if name:
        app.logger.info("Find by name: %s", name)
        products = Product.find_by_name(name)
    elif category:
        app.logger.info("Find by category: %s", category)
        # create enum from string
        category_value = getattr(Category, category.upper())
        products = Product.find_by_category(category_value)

    # test to see if you received the "available" query parameter
    # If you did, convert the available string retrieved from the query parameters to a boolean value
    # call the Product.find_by_availability(available_value) method to retrieve products that match the specified available_value
    # otherwise list all products

    else:
        app.logger.info("Find all")
        products = Product.all()

    results = [product.serialize() for product in products]
    app.logger.info("[%s] Products returned", len(results))
    return results, status.HTTP_200_OK

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete REST API implementation for List By Availability function:

```python
######################################################################
# LIST PRODUCTS
######################################################################
@app.route("/products", methods=["GET"])
def list_products():
    """Returns a list of Products"""
    app.logger.info("Request to list Products...")

    products = []
    name = request.args.get("name")
    category = request.args.get("category")
    available = request.args.get("available")

    if name:
        app.logger.info("Find by name: %s", name)
        products = Product.find_by_name(name)
    elif category:
        app.logger.info("Find by category: %s", category)
        # create enum from string
        category_value = getattr(Category, category.upper())
        products = Product.find_by_category(category_value)
    elif available:
        app.logger.info("Find by available: %s", available)
        # create bool from string
        available_value = available.lower() in ["true", "yes", "1"]
        products = Product.find_by_availability(available_value)
    else:
        app.logger.info("Find all")
        products = Product.all()

    results = [product.serialize() for product in products]
    app.logger.info("[%s] Products returned", len(results))
    return results, status.HTTP_200_OK

```

</details>

::page{title="Web site User Interface"}

The administrative user interface for this web site has already been provided for you by another team. Unfortunately, that team did not use good Behavior Driven Development techniques and so there are no test cases for the UI.

Your next two exercises involve creating test cases in the form of BDD scenarios to test that the UI behaves as expected. In order to write these test cases, you need to know what the UI looks like. It is a minimalist administrative interface. Below is an image of the web page that you are testing:

![Product Admin UI](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/final-product-ui.png "Product Admin UI")

::page{title="Exercise 4: Load BDD background data"}

The first thing you will need to do for BDD testing, is write the Python code to load the data from the `background:` statement in the `products.feature` file. Remember that the data is stored in the `context.table` attribute and each `row` is a Python dictionary (`dict`) that you can dereference using the names at the top of the columns in the `background:` statement.

## Your Task

Update the `features/steps/load_steps.py` file to load background data from your BDD scenarios into your service before each scenario executes.

The code to delete all of the products is already given to you. You just need to write the code to load the products from `context.table`.

::openFile{path="/home/project/tdd-bdd-final-project/features/steps/load_steps.py"}

**Note:** To open in file explorer go to the location:

`/home/project/tdd-bdd-final-project/features/steps/load_steps.py`

<details>
    <summary>Click here for a hint.</summary>
Here is starter code to load background data:

```python
    # load the database with new products
    #
    for row in context.table:
    # create payload to include product's name, description, price, availability, category.
    # send a POST request to the REST endpoint.
    # assert that the HTTP status code of the response is equal to 201.

```

</details>

<details>
    <summary>Click here to check your solution.</summary>
This is a complete code to load background data:

```python
    for row in context.table:
        payload = {
            "name": row['name'],
            "description": row['description'],
            "price": row['price'],
            "available": row['available'] in ['True', 'true', '1'],
            "category": row['category']
        }
        context.resp = requests.post(rest_endpoint, json=payload)
        assert context.resp.status_code == HTTP_201_CREATED

```

</details>

::page{title="Exercise 5: Create BDD Scenarios"}

Now that the background data is loaded, it's time to write the scenarios to test the UI. The **Create a Product** scenario is already written as an example of what you need to do.

The service already contains a UI that looks like this:

![Product Admin UI](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0241EN-SkillsNetwork/images/final-product-ui.png "Product Admin UI")

## Your Task

1. Update the `features/products.feature` file with BDD Scenarios that prove that the following behaviors of the UI work as expected:
	- Read a Product
	- Update a Product
	- Delete a Product
	- List all Products
	- Search for Products by Category
	- Search for Products by Availability
	- Search for Products by Name

Start by opening the file `petshop.feature`.

::openFile{path="/home/project/tdd-bdd-final-project/features/products.feature"}

**Note:** To open in file explorer go to the location:

`/home/project/tdd-bdd-final-project/features/products.feature`

## BDD Scenario for Reading a Product

Document the steps that the customer needs to take:

1. Use the `Scenario:` keyword with the title **"Read a Product"**
2. Use the `When` keyword to specify to start on the **"Home Page"**
3. Use the `And` keyword to describe the action of setting the **"Name"** to **"Hat"**
4. Use the `And` keyword to describe the action of clicking the **"Search"** button
5. Use the `Then` keyword to describe that they should see the message **"Success"**
6. Use the `When` keyword to specify copy the **"Id"** field
7. Use the `And` keyword to describe the action of pressing the **"Clear"** button
8. Use the `And` keyword to describe the action of pasting the **"Id"** field
9. Use the `And` keyword to describe the action of pressing the **"Retrieve"** button
10. Use the `Then` keyword to describe that they should see the message **"Success"**
11. Use the `And` keyword to state that they should see **"Hat"** in the **"Name"** field
12. Use the `And` keyword to state that they should see **"A red fedora"** in the **"Description"** field
13. Use the `And` keyword to state that they should see **"True"** in the **"Available"** dropdown
14. Use the `And` keyword to state that they should see **"Cloths"** in the **"Category"** dropdown
15. Use the `And` keyword to state that they should see **"59.95"** in the **"Price"** field

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the scenario

```
Scenario: Read a Product
    When {what to do}
    And {more to do}
    Then {what do you see}
    When {what to do}
    And {more to do}
    Then {what do you see}
    And {more things to see}

```

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```
Scenario: Read a Product
    When I visit the "Home Page"
    And I set the "Name" to "Hat"
    And I press the "Search" button
    Then I should see the message "Success"
    When I copy the "Id" field
    And I press the "Clear" button
    And I paste the "Id" field
    And I press the "Retrieve" button
    Then I should see the message "Success"
    And I should see "Hat" in the "Name" field
    And I should see "A red fedora" in the "Description" field
    And I should see "True" in the "Available" dropdown
    And I should see "Cloths" in the "Category" dropdown
    And I should see "59.95" in the "Price" field

```

</details>

Now that you have written the scenario for **Read a Product** follow the same lines  for the remaining scenarios. 

::page{title="BDD Hints and Solutions"}

This page contains the remaining hints and solutions for the **Update**, **Delete** , **Search for Products by Category** , **Search for Products by Availability**, **Search for Products by Name** scenarios.

## BDD Scenario for Updating a Product

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the scenario

```
Scenario: Update a Product
    When I visit the "Home Page"
	And ...
```
What you need to do:
* Type in a **Name** that exists in the **Background** data and press the **Search** button
* Wait for the message **"Success"** to be returned
* Check that a field has an expected value
* Change the one of the fields and press the Update button
* Check for the message **Success**
* Copy the **Id** field, clear the form, paste the **Id** field and press the **Retrieve** button
* Check for the message **Success**
* Check that the field you updated has the new value
* Press the **Clear** button followed by the **Search** button and check that the changed field is in the results

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```
Scenario: Update a Product
    When I visit the "Home Page"
    And I set the "Name" to "Hat"
    And I press the "Search" button
    Then I should see the message "Success"
    And I should see "A red fedora" in the "Description" field
    When I change "Name" to "Fedora"
    And I press the "Update" button
    Then I should see the message "Success"
    When I copy the "Id" field
    And I press the "Clear" button
    And I paste the "Id" field
    And I press the "Retrieve" button
    Then I should see the message "Success"
    And I should see "Fedora" in the "Name" field
    When I press the "Clear" button
    And I press the "Search" button
    Then I should see the message "Success"
    And I should see "Fedora" in the results
    And I should not see "Hat" in the results

```

</details>

## BDD Scenario for Deleting a Product

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the scenario

```
Scenario: Delete a Product
    When I visit the "Home Page"
    And ...
```

What you need to do:
* Type in a **Name** that exists in the **Background** data and press the **Search** button
* Wait for the message **"Success"** to be returned
* Check that a field has an expected value
* Copy the **Id** fieled, clear the form, paste the **Id** field and press the **Delete** button
* Check for the message **"Product has been Deleted!"**
* Press the **Clear** button followed by the **Search** button and check that the product is not in the results

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```
Scenario: Delete a Product
    When I visit the "Home Page"
    And I set the "Name" to "Hat"
    And I press the "Search" button
    Then I should see the message "Success"
    And I should see "A red fedora" in the "Description" field
    When I copy the "Id" field
    And I press the "Clear" button
    And I paste the "Id" field
    And I press the "Delete" button
    Then I should see the message "Product has been Deleted!"
    When I press the "Clear" button
    And I press the "Search" button
    Then I should see the message "Success"
    And I should not see "Hat" in the results

```

</details>

## BDD Scenario for Listing all Products

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the scenario

```
Scenario: List all products
    When I visit the "Home Page"
    And ...
```

What you need to do:
* Press the Clear button to remove the previous entries made.
* Press the Search button
* Wait for the message **"Success"** to be returned
* Check if all the products such as "Hat", "Shoes" , "Big Mac" and "Sheets" are seen the results.

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```
Scenario: List all products
    When I visit the "Home Page"
    And I press the "Clear" button
    And I press the "Search" button
    Then I should see the message "Success"
    And I should see "Hat" in the results
    And I should see "Shoes" in the results
    And I should see "Big Mac" in the results
    And I should see "Sheets" in the results

```

</details>

## BDD Scenario for Searching a Product based on Category

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the scenario

```
Scenario: Search by category
    When I visit the "Home Page"
    And ...
```

What you need to do:
* Clear the page to clear out the default dropdown selections
* Select the **Food** category and press the **Search** button
* Wait for the message **"Success"**
* Check that **"Big Mac"** is in the results and other foods from the **Background** data are not in the results

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```
Scenario: Search by category
    When I visit the "Home Page"
    And I press the "Clear" button
    And I select "Food" in the "Category" dropdown
    And I press the "Search" button
    Then I should see the message "Success"
    And I should see "Big Mac" in the results
    And I should not see "Hat" in the results
    And I should not see "Shoes" in the results
    And I should not see "Sheets" in the results

```

</details>

## BDD Scenario for Searching a Product based on Availability

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the scenario

```
Scenario: Search by available
    When I visit the "Home Page"
    And ...
```

Whet you need to do:
* Clear the page to clear out the default dropdown selections
* Set the **Available** dropdown to **True** and press the **Search** button
* Wait for the message **"Success"**
* Check that available items from the **Background** data re in the results and the unavailable items are not

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```
Scenario: Search by available
    When I visit the "Home Page"
    And I press the "Clear" button
    And I select "True" in the "Available" dropdown
    And I press the "Search" button
    Then I should see the message "Success"
    And I should see "Hat" in the results
    And I should see "Big Mac" in the results
    And I should see "Sheets" in the results
    And I should not see "Shoes" in the results

```

</details>

## BDD Scenario for Searching a Product based on Name

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the scenario

```
Scenario: Search by name
    When I visit the "Home Page"
    And ...

```

What you need to do:
* Type in a **Name** that exists in the **Background** data and press the **Search** button
* Wait for the message **"Success"** to be returned
* Check that the **Name** and **Description** match the item you are seatching for

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```
Scenario: Search by name
    When I visit the "Home Page"
    And I set the "Name" to "Hat"
    And I press the "Search" button
    Then I should see the message "Success"
    And I should see "Hat" in the "Name" field
    And I should see "A red fedora" in the "Description" field

```

</details>

## Your Task

1. Start the service in a Terminal with the command `honcho start`

1. In another Terminal, run the `behave` tool to seewhat steps need to be implemented. You will implement them next.

## Acceptance Criteria

- Ensure that you see suggested step definitions from `behave`.

::page{title="Exercise 6: Implementing Steps"}

In BDD, test scenarios are often written in a human-readable format, such as Gherkin, and these scenarios are translated into automated tests using step definitions.

The `web_steps.py` file contains the step definitions for the web-related actions on the UI.

Please check [Hands-on Lab: Implementing Your First Steps](link to the lab page to be included) for any reference you may need to understand about how step definitions are implemented, before proceeding further.

The step definitions for the first few steps are already given to you.

## Your Task

Update the `features/steps/web_steps.py` file with the remaining step definitions.

Start by opening the file `web_steps.py`.

::openFile{path="/home/project/tdd-bdd-final-project/features/steps/web_steps.py"}

## Button-Click

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the step definition

```python

@when('I press the "{button}" button')
def step_impl(context, button):
    # Generate the button_id by converting the button name to lowercase and appending '-btn'
    # Use context.driver.find_element_by_id(button_id) line to find the button element on the web page based on the generated button_id and call the click() method 
```

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```python
@when('I press the "{button}" button')
def step_impl(context, button):
    button_id = button.lower() + '-btn'
    context.driver.find_element_by_id(button_id).click()

```

</details>

## Verify for a specific name or text to be present

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the step definition

```python

@then('I should see "{name}" in the results')
def step_impl(context, name):
    # Use the WebDriverWait to wait for the specified name to be present in the element with the ID 'search_results
    # Check if the provided name is present in the text content of the element using the expected_conditions.text_to_be_present_in_element method
    # Use the assert(found) statement to verify the name was found in the results.
```

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```python
@then('I should see "{name}" in the results')
def step_impl(context, name):
    found = WebDriverWait(context.driver, context.wait_seconds).until(
        expected_conditions.text_to_be_present_in_element(
            (By.ID, 'search_results'),
            name
        )
    )
    assert(found)

```

</details>

## Verify for a specific name or text to NOT be present

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the step definition

```python

@then('I should not see "{name}" in the results')
def step_impl(context, name):
    # Use context.driver.find_element_by_id('search_results') to locate the element with the ID 'search_results',
    # Use the assert(name not in element.text) statement to check if the provided name is not present in the text content of the element.
    # assert that the name is not found in the results

```

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```python
@then('I should not see "{name}" in the results')
def step_impl(context, name):
    element = context.driver.find_element_by_id('search_results')
    assert(name not in element.text)

```

</details>

## Verify that a specific message is present 

<details>
<summary>Click here for a hint.</summary>
Here is the outline for the step definition

```python

@then('I should see the message "{message}"')
def step_impl(context, message):
    # Use WebDriverWait to wait for the specified message to be present in the element with the ID 'flash_message'
    # Use the expected_conditions.text_to_be_present_in_element method to check if the provided message is present in the text content of the element.
    # Use the assert(found) statement to verify that the message was found in the flash message area.

```

</details>

<details>
	<summary>Click here for the answer.</summary>
	Make sure that your solution looks like this:

```python
@then('I should see the message "{message}"')
def step_impl(context, message):
    found = WebDriverWait(context.driver, context.wait_seconds).until(
        expected_conditions.text_to_be_present_in_element(
            (By.ID, 'flash_message'),
            message
        )
    )
    assert(found)

```

</details>

## Your Task

1. Start the service in a Terminal with the command `honcho start`

1. In another Terminal, run the `behave` tool to make sure that all seven (7) scenarios pass

## Acceptance Criteria

- Ensure that all seven (7) scenarios exist and pass

::page{title="Submission"}

## Commit the code to your Github repository

1. Use `g&#8203;it status` to make sure that you have committed your changes locally in the development environment.

1. Use the `g&#8203;it add` command to add the updated code to the staging area.

1. Commit your changes using `g&#8203;it commit -m <commit message>`

1. Push your local changes to a remote branch using the `g&#8203;it push` command

	> Note: Use your GitHub **Personal Access Token** as your password in the Cloud IDE environment. You may also need to configure Git the first time you use it with:
	```text
	git config --local user.email "you@example.com"
	git config --local user.name "Your Name"
	```

## Assessment

You can complete this assessment using one of the following options:

### Option 1: AI-Graded Submission and Evaluation

Submit the **code for the required functions** by copying and pasting the relevant sections from the files in your GitHub repository into the submission field.

Make sure you include the complete and correct implementation from the appropriate files.

### Option 2: Peer-Graded Submission and Evaluation

Submit the **links to the relevant files** from your GitHub repository that contain the required functions.

Ensure the repository is accessible and the files clearly show your implementation.

## Evaluation

Use the lab environment to clone the project from the GitHub link provided
- Run `nosetests` and ensure that all tests pass and test coverage is 95% or better
- Run the application with `honcho start` in on terminal shell
- In another terminal shell run the `behave`command and ensure that there are seven (7) scenarios (one each for Read a Product, Update a Product, Delete a Product, List all Products, List by Category, List by Available, and List by Name) and that all scenarios pass.

::page{title="Final Project Submission Checklist"}

### Evaluation

Follow the checklist below to verify that your project meets all requirements before submission.

Submit your work through either **Option 1: AI-Graded Submission and Evaluation** or **Option 2: Peer-Graded Submission and Evaluation**, depending on the submission path you choose for project evaluation.

* * *

### Option 1: AI-Graded Submission

1.  Submit the updated fake products code from `tests/factories.py`. 
    
2.  Submit the code from `tests/test_models.py` for the functions: Read, Update, Delete, List All, Find by Name, Find by Category, Find by Availability. 
    
3.  Submit the code from `tests/test_routes.py` for the functions: Read, Update, Delete, List All, List by Name, List by Category, List by Availability. 
    
4.  Submit the code from `service/routes.py` for the functions: Read, Update, Delete, List All, List by Name, List by Category, List by Availability. 
    
5.  Submit the code snippet for loading BDD data from `features/steps/load_steps.py`. 
    
6.  Submit the BDD scenarios from `features/products.feature` for: Read, Update, Delete, List All, Search by Name, Search by Category, Search by Availability. 
    
7.  Submit the step definition code snippets from `features/steps/web_steps.py` for: Read, Update, Delete, List All, Search by Name, Search by Category, Search by Availability. 
    

* * *

### Option 2: Peer-Graded Submission

1.  Provide the GitHub URL of `tests/factories.py` showing the updated fake products code.
    
2.  Provide the GitHub URL of `tests/test_models.py` showing the functions: Read, Update, Delete, List All, Find by Name, Find by Category, Find by Availability.
    
3.  Provide the GitHub URL of `tests/test_routes.py` showing the functions: Read, Update, Delete, List All, List by Name, List by Category, List by Availability.
    
4.  Provide the GitHub URL of `service/routes.py` showing the functions: Read, Update, Delete, List All, List by Name, List by Category, List by Availability.
    
5.  Provide the GitHub URL of `features/steps/load_steps.py` showing the code snippet for loading BDD data.
    
6.  Provide the GitHub URL of `features/products.feature` showing the BDD scenarios: Read, Update, Delete, List All, Search by Name, Search by Category, Search by Availability.
    
7.  Provide the GitHub URL of `features/steps/web_steps.py` showing the step definition code snippets: Read, Update, Delete, List All, Search by Name, Search by Category, Search by Availability.
    

::page{title="Conclusion"}

Congratulations on completing the TDD / BDD Final Project. Hopefully now you have proven to yourself that you understand how to implement good test Driven and behavior Driven Development practices.

## Next Steps

Incorpoate these new practces into your projects an home and at work. Write the test cases for the code you "wish you had" and then write the code to make those tests pass. Describe the behavior of you system from the outside in and then prove that it behaves that way by automating those tests with Behave.

## Author(s)

[John J. Rofrano](https://www.linkedin.com/in/johnrofrano)

### Other Contributor(s)

Lavanya Rajalingam

<!-- ## Changelog

| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2023-06-26 | 0.1 | John Rofrano | Initial version created |
| 2023-08-04 | 0.2 | Lavanya Rajalingam  | Updated Instructions with Hints and Solutions  |
| 2023-08-04 | 0.3 | John Rofrano | Edit hints for clarity |
| 2023-08-04 | 0.4 | John Rofrano | Reverted Selenium syntax |
| 2023-08-09 | 0.5 | Lavanya Rajalingam  | Fixed Images and File Locations  |
| 2023-08-16 | 0.6 | John Rofrano | Rewrote list by solutons |
| 2023-08-21 | 0.7 | Lavanya Rajalingam  | Updated instructions for import statements, included List all for behave and Git Operations |
| 2023-08-22 | 0.8 | Lavanya Rajalingam  | Updated solution for clearing linting errors  |
| 2023-09-26 | 0.9 | John Rofrano  | Added the Clear button to Available search  | 
| 2024-11-27 | 1.0 | Rajashree Patil  | Corrected mislabelled solution codes  | -->

<h3 align="center"> &#169; IBM Corporation. All rights reserved. <h3/>
