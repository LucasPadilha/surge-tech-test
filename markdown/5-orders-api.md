# Orders API

#### POST /orders

This endpoint allows the client with a `Customer` role to create a new `Order`.

##### Example request

Request body
```
{
	"restaurant": {
		"id": 1
	},
	"fee": 0,
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
			"quantity": 1
		},
		{
			"id": 2,
			"quantity": 3
		}
	]
}
```

##### Example response

```
HTTP/1.1 201 Created
Content-Type: application/json

{
	"id": 2,
	"customer": {
		"id": 1,
		"name": "Customer #1"
	},
	"restaurant": {
		"id": 1,
		"name": "Restaurant 1"
	},
	"created_at": "2020-10-02 12:00:00",
	"fee": 0,
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
			"quantity": 3,
			"price": 1.29
		}
	],
	"status": "created"
}
```

#### POST /orders/:id/pay

This endpoint allows the client with a `Customer` role to pay an existing `Order`.

##### Example request

Request body
```
{
	"payment": {
		"source": "tok_mastercard"
	}
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 2,
	"customer": {
		"id": 1,
		"name": "Customer #1"
	},
	"restaurant": {
		"id": 1,
		"name": "Restaurant 1"
	},
	"created_at": "2020-10-02 12:00:00",
	"fee": 0,
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
			"quantity": 3,
			"price": 1.29
		}
	],
	"status": "paid"
}
```

#### PUT /orders/:id

This endpoint allows the client with a `Customer` role to update an existing `Order`.

Orders can only be edited if the order status is `created`.

##### Example request

Request body
```
{
	"address": {
		"address": "New address line",
		"address2": "Address line 2",
		"city": "City",
		"country": "Country",
		"zip": "Zip Code"
	},
	"items": [
		{
			"id": 1,
			"quantity": 2
		},
		{
			"id": 2,
			"quantity": 4
		},
	]
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 2,
	"customer": {
		"id": 1,
		"name": "Customer #1"
	},
	"restaurant": {
		"id": 1,
		"name": "Restaurant 1"
	},
	"created_at": "2020-10-02 12:00:00",
	"fee": 0,
	"discount": 0,
	"address": {
		"address": "New address line",
		"address2": "Address line 2",
		"city": "City",
		"country": "Country",
		"zip": "Zip Code"
	},
	"items": [
		{
			"id": 1,
			"name": "Product",
			"quantity": 2,
			"price": 1.99
		},
		{
			"id": 2,
			"name": "Product 2",
			"quantity": 4,
			"price": 1.29
		}
	],
	"status": "created"
}
```

#### DELETE /orders/:id

This endpoint allows the client with a `Customer` role to cancel an existing `Order`.

Orders can only be cancelled if the order status is `created`.

##### Example response

```
HTTP/1.1 204 No content
Content-Type: application/json
```
