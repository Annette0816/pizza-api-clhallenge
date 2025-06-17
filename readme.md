#  Pizza Restaurant API

This is a RESTful API for managing a pizza restaurant using Flask, SQLAlchemy, and Flask-Migrate. It follows the MVC (Model-View-Controller) pattern.

 

## Project Structure

pizza-api-challenge/
├── server/
│ ├── app.py
│ ├── config.py
│ ├── seed.py
│ ├── models/
│ ├── controllers/
├── migrations/
├── challenge-1-pizzas.postman_collection.json
└── README.md




##  Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/Annette0816/pizza-api-clhallenge


### 2. Install the dependencies and activate shell
pipenv install flask flask_sqlalchemy flask_migrate
pipenv shell


### 3.Set up environment variable
export FLASK_APP=server/app.py

### 4.Database migration
flask db init
flask db migrate -m "Initial migration"
flask db upgrade

### 5.Seed the database
python server/seed.py

## API Endpoints
 Restaurants
GET /restaurants
Returns a list of all restaurants.

Response

json
Copy
Edit
[
  {
    "id": 1,
    "name": "Kiki's Pizza",
    "address": "123 Pizza Street"
  },
  ...
]
GET /restaurants/<int:id>
Returns a specific restaurant and its pizzas.

Success Response

json
Copy
Edit
{
  "id": 1,
  "name": "Kiki's Pizza",
  "address": "123 Pizza Street",
  "pizzas": [
    {
      "id": 1,
      "name": "Emma",
      "ingredients": "Dough, Tomato Sauce, Cheese"
    }
  ]
}
Error Response

json
Copy
Edit
{
  "error": "Restaurant not found"
}
DELETE /restaurants/<int:id>
Deletes a restaurant and all its restaurant_pizzas.

Success Response → 204 No Content

Error Response

json
Copy
Edit
{
  "error": "Restaurant not found"
}
 Pizzas
GET /pizzas
Returns a list of all pizzas.

Response

json
Copy
Edit
[
  {
    "id": 1,
    "name": "Emma",
    "ingredients": "Dough, Tomato Sauce, Cheese"
  }
]
 Restaurant Pizzas
POST /restaurant_pizzas
Creates a new association between a pizza and a restaurant.

Request

json
Copy
Edit
{
  "price": 5,
  "pizza_id": 1,
  "restaurant_id": 3
}
Success Response

json
Copy
Edit
{
  "id": 4,
  "price": 5,
  "pizza_id": 1,
  "restaurant_id": 3,
  "pizza": {
    "id": 1,
    "name": "Emma",
    "ingredients": "Dough, Tomato Sauce, Cheese"
  },
  "restaurant": {
    "id": 3,
    "name": "Kiki's Pizza",
    "address": "address3"
  }
}
Validation Error Response

json
Copy
Edit
{
  "errors": ["Price must be between 1 and 30"]
}
✅ Validations
Field	Validation
price	Must be between 1 and 30
name	Required (non-null string)
address	Required (non-null string)
pizza_id	Must reference an existing pizza
restaurant_id	Must reference an existing restaurant

 Testing with Postman
1.Open Postman

2.Click Import

3.Upload the challenge-1-pizzas.postman_collection.json file from the repo

4.Test all available routes

