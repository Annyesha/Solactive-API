## Product and Service APIs
This application exposes 4 API endpoits. The application based on python 3. Flask is used for the web framework and SQLAlchemy is used as ORM to communicate with the database.
SQLite3 has been used as the database.

## Architecture
	
	- Main.py : Main class where the endpoints of the services are defined
	- DBAccess.py : This is the class which communicates with the database using static methods and ORM support from SQLAlchemy.
	- Model.py : This defines the model classes which is used by the controller to communicate with the SQLite database using ORM.
	
	Scope of Imrovements : Handling concurrent requests, exception handling , handling negative test cases

## Set up Local development environment

1- Download Python3.9.6:
    
   Install Python3.9.6 using this link - (https://www.python.org/downloads/).
	
   Please make sure the environment variables are set properly by cheking the option while installing python
    
2- Install Flask using the command in command prompt:

   pip install flask
    
3- Install SQLAlchemy using the command in command prompt:

    pip install sqlalchemy
	
4 - Download the project from https://github.com/Annyesha/Solactive-Challenge
	

4 - Host the api services
	
	Open the command prompt and switch to the directory where the project has been downloaded
	Execute the command in command prompt :  python Main.py

SQLite Solcative.db will be autmoatically created when the services will be hosted.
It will not get created if it already exists in the project directory.
	

	
## Assumptions:
	- The product will have an asOf date which determines from when the product will be valid
	- The api to create new product will also create the service by reading the service name from the service attributes. It is assumed that all service attribute names
	  will have the service name as a prefix and separted by a ".". The service will not get created if it already exists in the database.
	- The asOf date of a service is set by default to 7 days prior to the current date. This can be read from the input in next iteration.
	- The currency code is expected to be provided in the correct format. A check for validating the currency code is not implemented.
	- The product will not be returned if the requested timestamp provided is behind the asOf date of the product
	- Service attributes of a product will not be returned if the requested timestamp is behind the service asOf date.
	- Products created in last 7 days are considered as newly created products.
	- The api to update the service attribute of a product based on the requested service id and product id is able to recieve and update one attribute at a time.
		
## Brief Description of the APIs
	
	API 1 : http://localhost:6000/products/newproduct [request body : A json with product details]
	
	This will create the product in the database with its properties along with the created timestamp. It will also read the service attributes from the request and will create the unique services in
	the databsae. The asOf date for the the service are now set to 7 days prior to current date time. This can be read from an user input in next iteration.
	The service attribute name and values will get mapped to the newly created product.
	
	API 2 : http://localhost:6000/products/<prod_id>?timestamp=<unix_timestamp>

	This api will look into the database and will fetch the product when the product_id is matched and also the product asOf date is lesser than the
	requested unix_timestamp. It will also fetch the service attributes from the database for the correspondig product also when the service asOf 
	the respective service attributes are lesser than the timestamp.
	
	API 3 : http://localhost:6000/services/<service_id>?timestamp=<unix_timestamp>

	This service fetches all the newly created (created in last 7 days) products along with the service attribute details for the requested service where the products are mapped to attributes of this service. 
	Asof dates are checked for the service and for the product and compared with the requested unix_timestamp before returning the products.
	
	API 4 : http://localhost:6000/services/<service_id>/product/<product_id> [request body : A json with the attribute name and value]

	This api will identifiy the product with the product id and will then read the service attributes of the service_id which are already mapped to this product.
	Then the api will update the service attribute value of the product after matching it with the name and value of the attribute which is received over request body.
	
## Install Postman to invoke the APIS
    
    Please import the request json file to your postman
    Invoke each of the 4 apis with proper parameter and json request from Postman


	

	


	
	
    