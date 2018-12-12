# pirple-homework-assignment-3
#homework-assignment-3 Public repo for the Pirple Homework Assignment #3

API Definition
/users
[POST] http://localhost:3000/users
Example payload request:

{
    "name": "Your Name",
    "emailAddress": "your_address@your_domain.com",
    "streetAddress": "your street address",
    "password": "yourpassword"
}
[GET] http://localhost:3000/users?id=71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

The required id in querystring is the hashed emailAddress, such that the system allows unique users with their unique emailAddress.

[PUT] http://localhost:3000/users
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

{
	"id": "71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970",    //required 
	"name":"New Name",
	"streetAddress":"New Street",
	"password":"NewPassword"
}
[DELETE] http://localhost:3000/users?id=71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

Note: it removes the token associated with the user.

/login
[POST] http://localhost:3000/login
{
	"emailAddress": "your_address@your_domain.com",
	"password": "NewPassword"

}
Note: it doesn't create more tokens if there is already a valid (not expired) token for the user.

/logout
[POST] http://localhost:3000/logout
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

Note: it removes the token from the system itself.

/menu
[GET] http://localhost:3000/menu
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

Returns the list of possible pizza's (item) to select, not hardcoded, but each pizza exist on a separate file called 'menuitems' in the data folder.

/cart
[GET] http://localhost:3000/cart
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

Returns the current list of items in user's cart.

/cart
[PUT] http://localhost:3000/cart
Requires authentication and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: 71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970

{
	"item":"Vegetarian"
}
Note: item should be a valid pizza name from the list of available pizzas. It allows multiple to add multiple pizzas with the same name to the cart. After that the shoppingcart array of the user object is updated.

[DELETE] http://localhost:3000/cart
Requires authentication token and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: 71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970

{
	"item":"Vegetarian"
}
Note: it removes the first single pizza on the shoppingcart array of the user with the same pizza name requested. It doesn't remove nor update if pizza name wasn't found or shopping cart is empty.

/order
[GET] http://localhost:3000/order
Requires authentication token and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: 71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970

Note: Using the id query string, lookup and fetch the order object from the orders data folder.

Example:

{
    "id": "oy7ilik4vual2q9g98ad",
    "userId": "71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970",
    "payed": false,
    "mail_sent": false,
    "totalPrice": 64.99,
    "items": [
        "Vegetarian"
    ]
}
[POST] http://localhost:3000/order
Requires authentication token and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: 71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970

Note: it creates a new order with all the items on user's shopping cart and save it on the system, using the data folder called 'orders', the total price of the order is also calculated based on each price of each pizza on the order. After placing the order the shopping cart gets empty and a new order id goes to the orders array of user object as the following example shows.

Example:

{
    "id": "71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970",
    "name": "Name",
    "emailAddress": "Email Example",
    "streetAddress": "Street Example",
    "orders": [
        "oy7ilik4vual2q9g98ad"
    ],
    "shoppingcart": []
}
/checkout
[POST] http://localhost:3000/checkout
Requires authentication token and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: a688f4dbc11ead7d9902ef10347e2eebec1c9eae38521cfb3e6bc19aa0c1df98

Also requires the following data on body (json), the id of the order to checkout and the stripe token to apply the charge (in this case it's a test token)

{
	"orderId":"wr5pwe84uqbayywbytqe",
	"stripeToken":"tok_mastercard_debit"
}
After charging an email is sent to the user, and the variables regarding 'payment' and 'email sent' of the order are updated depending on the success of both operations. Example of a order in which both payment and email were sent with success:

{
    "id": "oy7ilik4vual2q9g98ad",
    "userId": "71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970",
    "payed": true,
    "mail_sent": true,
    "totalPrice": 64.99,
    "items": [
        "Vegetarian"
    ]
#homework-assignment-2 Public repo for the Pirple Homework Assignment #2

API Definition
/users
[POST] http://localhost:3000/users
Example payload request:

{
    "name": "Your Name",
    "emailAddress": "your_address@your_domain.com",
    "streetAddress": "your street address",
    "password": "yourpassword"
}
[GET] http://localhost:3000/users?id=71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

The required id in querystring is the hashed emailAddress, such that the system allows unique users with their unique emailAddress.

[PUT] http://localhost:3000/users
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

{
	"id": "71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970",    //required 
	"name":"New Name",
	"streetAddress":"New Street",
	"password":"NewPassword"
}
[DELETE] http://localhost:3000/users?id=71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

Note: it removes the token associated with the user.

/login
[POST] http://localhost:3000/login
{
	"emailAddress": "your_address@your_domain.com",
	"password": "NewPassword"

}
Note: it doesn't create more tokens if there is already a valid (not expired) token for the user.

/logout
[POST] http://localhost:3000/logout
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

Note: it removes the token from the system itself.

/menu
[GET] http://localhost:3000/menu
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

Returns the list of possible pizza's (item) to select, not hardcoded, but each pizza exist on a separate file called 'menuitems' in the data folder.

/cart
[GET] http://localhost:3000/cart
Requires authentication token in header, the token key like this:

token : 3606rzf8nbu9djv6ny1e

Returns the current list of items in user's cart.

/cart
[PUT] http://localhost:3000/cart
Requires authentication and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: 71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970

{
	"item":"Vegetarian"
}
Note: item should be a valid pizza name from the list of available pizzas. It allows multiple to add multiple pizzas with the same name to the cart. After that the shoppingcart array of the user object is updated.

[DELETE] http://localhost:3000/cart
Requires authentication token and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: 71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970

{
	"item":"Vegetarian"
}
Note: it removes the first single pizza on the shoppingcart array of the user with the same pizza name requested. It doesn't remove nor update if pizza name wasn't found or shopping cart is empty.

/order
[GET] http://localhost:3000/order
Requires authentication token and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: 71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970

Note: Using the id query string, lookup and fetch the order object from the orders data folder.

Example:

{
    "id": "oy7ilik4vual2q9g98ad",
    "userId": "71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970",
    "payed": false,
    "mail_sent": false,
    "totalPrice": 64.99,
    "items": [
        "Vegetarian"
    ]
}
[POST] http://localhost:3000/order
Requires authentication token and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: 71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970

Note: it creates a new order with all the items on user's shopping cart and save it on the system, using the data folder called 'orders', the total price of the order is also calculated based on each price of each pizza on the order. After placing the order the shopping cart gets empty and a new order id goes to the orders array of user object as the following example shows.

Example:

{
    "id": "71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970",
    "name": "Name",
    "emailAddress": "Email Example",
    "streetAddress": "Street Example",
    "orders": [
        "oy7ilik4vual2q9g98ad"
    ],
    "shoppingcart": []
}
/checkout
[POST] http://localhost:3000/checkout
Requires authentication token and userid in header, like this:

token : 3606rzf8nbu9djv6ny1e userid: a688f4dbc11ead7d9902ef10347e2eebec1c9eae38521cfb3e6bc19aa0c1df98

Also requires the following data on body (json), the id of the order to checkout and the stripe token to apply the charge (in this case it's a test token)

{
	"orderId":"wr5pwe84uqbayywbytqe",
	"stripeToken":"tok_mastercard_debit"
}
After charging an email is sent to the user, and the variables regarding 'payment' and 'email sent' of the order are updated depending on the success of both operations. Example of a order in which both payment and email were sent with success:

{
    "id": "oy7ilik4vual2q9g98ad",
    "userId": "71b3f9655c365332a874452d17944a41aa48ba5a68ab25888e0472d366082970",
    "payed": true,
    "mail_sent": true,
    "totalPrice": 64.99,
    "items": [
        "Vegetarian"
    ]
}

# All images thanks to google.
