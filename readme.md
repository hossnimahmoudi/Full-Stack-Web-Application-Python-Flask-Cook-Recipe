### This project is designed to build a Simple Recipe Management Application using Python and Flask 
#### 1. Create a virtual environment.
#### 2. Install the necessary packages in our virtual environment.
 pip install -r requirements.txt
#### 3. To test all Endpoints we need to use command "curl". Note that
we have different parameters here: -i is for showing the header in the response
and -X is for specifying the HTTP method : <br>
<strong><em> curl -i -X GET localhost:5000/recipes </em></strong>
Or
<strong><em> http GET localhost:5000/recipes </em></strong>
#### 4. After that, let's create a recipe. This time, use the HTTP POST method, as we have
lots of information that cannot be encoded in the URL. Please take a look at the
following httpie command: <br>
<strong><em> http POST localhost:5000/recipes name="Cheese Pizza" description="This is
a lovely cheese pizza" </em></strong>
Or <br>
<strong><em> curl -i -X POST localhost:5000/recipes -H "Content-Type: application/
json" -d '{"name":"Cheese Pizza", "description":"This is a lovely cheese
pizza"}' </em></strong>

#### 5. Let's try to modify the recipe with ID 3. Use the HTTP PUT method and send over the modified name and description of the recipe to localhost:
<strong><em>http PUT localhost:5000/recipes/3 name="Lovely Cheese Pizza"
description="This is a lovely cheese pizza recipe." </em></strong>
Or <br>
<strong><em>curl -i -X PUT localhost:5000/recipes/3 -H "Content-Type: application/
json" -d '{"name":"Lovely Cheese Pizza", "description":"This is a lovely
cheese pizza recipe."}'</em></strong><br>
#########################################################################################<br>
### Creating a Recipe Model
##### 1. create a Python Package. Name it Models:
##### 2. Then, create a file called recipe.py under models
##### 3. Define the recipe class using recipe.py
##### 4. In the same Recipe class, define the data method for returning the data asa dictionary object.
### Defining an API Endpoint for the Recipe Model
To build an API endpoint, we need to define a class that inherits from flask_restful.
Resource. Then, we can declare the get and post methods inside the class. <br>
##### 1.Create a folder called resources under the project and then create a file called recipe.py under the resources folder.
##### 2. Import the necessary packages
##### 3. Right after the preceding code import, create the RecipeListResource class. This class has GET and POST methods, which are used to get and create the recipe's resources, respectively.
##### 4. Add the post method. This is used to create the recipe:
### Defining the Recipe Resource
##### 1.Define the RecipeResource resource and implement the get method.
##### 2. Implement the put method.
### Publishing and Unpublishing the Recipes
##### 1.Define the RecipePublic resource and implement the put method that will handle the HTTP PUT request.
##### 2. Implement the delete method, which will handle the HTTP DELETE request.
## Configuring Endpoints
### Creating the Main Application File
##### 1.Create the app.py file under the project folder.
##### 2. Import the necessary classes
from flask import Flask <br>
from flask_restful import Api <br>
from resources.recipe import RecipeListResource, RecipeResource, RecipePublishResource <br>
##### 3. Set up Flask and initialize flask_restful.API with our Flask app.
app = Flask(__name__) <br>
api = Api(app) <br>
##### 4. Add resource routing by passing in the URL so that it will route to our resources. Each resource will have its own HTTP method defined:
api.add_resource(RecipeListResource, '/recipes') <br>
api.add_resource(RecipeResource, '/recipes/<int:recipe_id>') <br>
api.add_resource(RecipePublishResource, '/recipes/<int:recipe_id>/publish') <br>
if __name__ == '__main__': <br>
    app.run(port=5000, debug=True) <br>

##### 5. Save app.py and right-click on it to run the application. Flask will then start up and run on the localhost (127.0.0.1) at port 5000:
## Making HTTP Requests to the Flask API using curl and httpie
### Testing the Endpoints Using curl and httpie
##### 1.Open the Terminal in PyCharm and type in the following commands. You can use either the httpie or curl command. The following is the httpie command (= is for string and := is for non-string):
<strong><em>http POST localhost:5000/recipes name="Cheese Pizza" description="This is a lovely cheese pizza" num_of_servings:=2 cook_time:=30 directions="This is how you make it" </em></strong> <br>
The following is the curl command. The -H argument is used to specify the header in the client request. We will set Content-Type: application/json as the header here. The -d argument is used for HTTP POST data, that is, the recipe in JSON format: <br>
<strong><em>curl -i -X POST localhost:5000/recipes -H "Content-Type: application/json" -d '{"name":"Cheese Pizza", "description":"This is a lovely cheese pizza","num_of_servings":2, "cook_time":30, "directions":"This is how you make it" }'</em></strong> <br>
### Testing the Auto-Incremented Recipe ID
##### 1.Create a second recipe and note that the ID is automatically incremented. Send the following client request using httpie:
<strong><em>http POST localhost:5000/recipes name="Tomato Pasta" description="This is a lovely tomato pasta recipe" num_of_servings:=3 cook_time:=20 directions="This is how you make it" </em></strong> <br>
Alternatively, send the request using curl. Again, the -H argument is used to specify the header in the client request. We will set "Content-Type: application/json" as the header here. The -d argument is used for HTTP POST data, meaning that the recipe is in JSON format: <br>
<strong><em>curl -i -X POST localhost:5000/recipes -H "Content-Type: application/json" -d '{"name":"Tomato Pasta", "description":"This is a lovely tomato pasta recipe", "num_of_servings":3, "cook_time":20, "directions":"This is how you make it"}' </em></strong> <br>
### Getting All the Recipes Back
##### 1.Retrieve all the recipes by sending the following client request using httpie:
<strong><em>http GET localhost:5000/recipes </em></strong> <br>
Alternatively, send the following request using curl. The -i argument is used to state that we want to see the response header. -X GET means that we are sending the client request using the HTTP GET method:<br>
<strong><em>curl -i -X GET localhost:5000/recipes </em></strong> <br>
Note <br>
We should see an empty list in the HTTP response because all the recipes we have created in the previous steps are in draft form (not published). <br>
{ <br>
    "data": [] <br>
} <br>
### Testing the Recipe Resources
##### 1.Modify the publish status of the recipe with ID 1. We can send the following client request using the httpie command:
<strong><em>http PUT localhost:5000/recipes/1/publish </em></strong> <br>
Alternatively, we can use the following curl command: <br>
<strong><em>curl -i -X PUT localhost:5000/recipes/1/publish </em></strong> <br>
Note <br>
Once the preceding client request has been sent to the server using the HTTP PUT method, the put method in RecipePublishResource will pick up the request and assign recipe_id to be 1. The application will look for the recipe with ID = 1 and update its publish status to True . <br>
##### 2. You should see the following response. Please examine it carefully:
HTTP/1.0 204 NO CONTENT <br>
Content-Type: application/json <br>
Date: Tue, 10 Nov 2020 09:53:48 GMT <br>
Server: Werkzeug/0.16.0 Python/3.7.0 <br>
##### 3. Now, retrieve all the published recipes and examine them. Then, send the following client request using httpie:
<strong><em>http GET localhost:5000/recipes </em></strong> <br>
Alternatively, send the following request using curl. The -i argument is used to say that we want to see the response header. -X GET means that we are sending the client request using the HTTP GET method: <br>
<strong><em>curl -i -X GET localhost:5000/recipes </em></strong> <br>
##### 4. You should see the following response. Please examine it carefully:
{ <br>
    "data": [ <br>
        { <br>
            "id": 1, <br> 
            "name": "Cheese Pizza", <br> 
            "description": "This is a lovely cheese pizza", <br> 
            "num_of_servings": 2, <br> 
            "cook_time": 30, <br> 
            "directions": "This is how you make it" <br>
        } <br> 
    ] <br> 
} <br> 
### Negative Testing