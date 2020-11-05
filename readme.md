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
cheese pizza recipe."}'</em></strong>
