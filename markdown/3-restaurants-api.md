# Restaurants API

#### GET /restaurants

This endpoint allows the client to retrieve all existing restaurants.

This endpoint can be used both by `Customer` or `Owner` and `Manager`.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json
Pagination-Count: 2
Pagination-Offset: 0
Pagination-Limit: 25

[
	{
		"id": 1,
		"name": "Restaurant 1",
		"address": {
			"address": "Address line 1",
			"address2": "Address line 2",
			"city": "City",
			"country": "Country",
			"zip": "Zip Code"
		}
	},
	{
		"id": 2,
		"name": "Restaurant 2",
		"address": {
			"address": "Address line 1",
			"address2": "Address line 2",
			"city": "City",
			"country": "Country",
			"zip": "Zip Code"
		}
	}
]
```

#### GET /restaurants/:id

This endpoint allows the client to view details about an existing `Restaurant`.

This endpoint can be used both by `Customer` or `Owner` and `Manager`.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 1,
	"name": "Restaurant 1",
	"address": {
		"address": "Address line 1",
		"address2": "Address line 2",
		"city": "City",
		"country": "Country",
		"zip": "Zip Code"
	},
	"menus": [
		{
			"id": 1,
			"name": "Menu 1"
		},
		{
			"id": 2",
			"name": "Menu 2"
		}
	]
}
```

#### GET /restaurant/:id/orders

This endpoint allows the client with either `Owner` or `Manager` role to retrieve all `Orders` for a given `Restaurant`.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json
Pagination-Count: 2
Pagination-Offset: 0
Pagination-Limit: 25

[
	{
		"id": 2,
		"customer": {
			"id": 2,
			"name": "Customer #2"
		},
		"restaurant": {
			"id": 1,
			"name": "Restaurant 1"
		},
		"created_at": "2020-10-01 14:30:00",
		"fee": 0,
		"discount": 3.50,
		"address": {
			"address": "Address line 1",
			"address2": "Address line 2",
			"city": "City",
			"country": "Country",
			"zip": "Zip Code"
		},
		"items": [
			{
				"id": 3,
				"name": "Product",
				"quantity": 3,
				"price": 4.99
			},
			{
				"id": 2,
				"name": "Product 2",
				"quantity": 1,
				"price": 1.29
			}
		],
		"status": "canceled"
	},
	{
		"id": 1,
		"customer": {
			"id": 1,
			"name": "Customer #1"
		},
		"restaurant": {
			"id": 1,
			"name": "Restaurant 1"
		},
		"created_at": "2020-10-01 13:00:00",
		"fee": 0.49,
		"discount": 0,
		"address": {
			"address": "Address line 1",
			"address2": "Address line 2",
			"city": "City",
			"country": "Country",
			"zip": "Zip Code"
		},
		"items": [
			{
				"id": 1,
				"name": "Product",
				"quantity": 1,
				"price": 1.99
			},
			{
				"id": 2,
				"name": "Product 2",
				"quantity": 2,
				"price": 1.29
			}
		],
		"status": "paid"
	}
]
```

#### GET /restaurants/:restaurantId/orders/:orderId

This endpoint allows the client with either an `Owner` or `Manager` role to view details about an existing `Order`.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 1,
	"customer": {
		"id": 1,
		"name": "Customer #1"
	},
	"restaurant": {
		"id": 1,
		"name": "Restaurant 1"
	},
	"created_at": "2020-10-01 13:00:00",
	"fee": 0.49,
	"discount": 0,
	"address": {
		"address": "Address line 1",
		"address2": "Address line 2",
		"city": "City",
		"country": "Country",
		"zip": "Zip Code"
	},
	"items": [
		{
			"id": 1,
			"name": "Product",
			"quantity": 1,
			"price": 1.99
		},
		{
			"id": 2,
			"name": "Product 2",
			"quantity": 2,
			"price": 1.29
		}
	],
	"status": "paid"
}
```

#### PUT /restaurants/:restaurantId/orders/:orderId

This endpoint allows the client with either an `Owner` or `Manager` role to update an existing `Order`.

##### Example request

Request body
```
{
	"discount": 12.99
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 1,
	"customer": {
		"id": 1,
		"name": "Customer #1"
	},
	"restaurant": {
		"id": 1,
		"name": "Restaurant 1"
	},
	"created_at": "2020-10-01 13:00:00",
	"fee": 0.49,
	"discount": 12.99,
	"address": {
		"address": "Address line 1",
		"address2": "Address line 2",
		"city": "City",
		"country": "Country",
		"zip": "Zip Code"
	},
	"items": [
		{
			"id": 1,
			"name": "Product",
			"quantity": 1,
			"price": 1.99
		},
		{
			"id": 2,
			"name": "Product 2",
			"quantity": 2,
			"price": 1.29
		}
	],
	"status": "paid"
}
```

#### GET /restaurants/:id/customers

This endpoint allows the client with either an `Owner` or `Manager` role to retrieve all `Customers` from a given `Restaurant`.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json
Pagination-Count: 3
Pagination-Offset: 0
Pagination-Limit: 25

[
	{
		"id": 1,
		"email": "customer@email.com",
		"first_name": "Customer",
		"last_name": "Name"
	},
	{
		"id": 2,
		"email": "customer2@email.com",
		"first_name": "Customer #2",
		"last_name": "Name"
	},
	{
		"id": 3,
		"email": "customer3@email.com",
		"first_name": "Customer #3",
		"last_name": "Name"
	}
]
```

#### POST /restaurants

This endpoint allows the client with an `Owner` role to create a new `Restaurant`.

##### Example request

Request body
```
{
	"name": "New Restaurant",
	"address": {
		"address": "Address line 1",
		"address2": "Address line 2",
		"city": "City",
		"country": "Country",
		"zip": "Zip Code"
	}
}
```

##### Example response

```
HTTP/1.1 201 Created
Content-Type: application/json

{
	"id": 3,
	"name": "New Restaurant",
	"address": {
		"address": "Address line 1",
		"address2": "Address line 2",
		"city": "City",
		"country": "Country",
		"zip": "Zip Code"
	}
}
```

#### PUT /restaurants/:id

This endpoint allows the client with an `Owner` role to update an existing `Restaurant`.

##### Example request

Request body
```
{
	"name": "Restaurant new",
	"address": {
		"address": "Address line 1",
		"address2": "Address line 2",
		"city": "City",
		"country": "Country",
		"zip": "Zip Code"
	}
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 3,
	"name": "Restaurant new",
	"address": {
		"address": "Address line 1",
		"address2": "Address line 2",
		"city": "City",
		"country": "Country",
		"zip": "Zip Code"
	}
}
```

#### DELETE /restaurants/:id

This endpoint allows the client with an `Owner` role to delete an existing `Restaurant`.

##### Example response

```
HTTP/1.1 204 No content
Content-Type: application/json
```