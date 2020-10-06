# Customer API

#### GET /customers/profile

This endpoint allows the client to retrieve the authenticated `Customer` profile details.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 1,
	"email": "test@customer.com",
	"first_name": "Test",
	"last_name": Customer"
}
```

#### PUT /customers/profile

This endpoint allows the client to update the authenticated `Customer` profile details.

Currently the only parameters that can be updated using the `PUT /customers/profile` endpoint are `first_name` and `last_name`. The request body must contain at least one.

##### Example request

Request body
```
{
	"first_name": "Name",
	"last_name": "Change"
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 1,
	"email": "test@customer.com",
	"first_name": "Name",
	"last_name": "Change"
}
```

#### PUT /customers/password

This endpoint allows the client to update the authenticated `Customer` password.

##### Example request

Request body
```
{
	"old_password": "old_password",
	"new_password": "new_password"
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json
```

#### POST /customers

This endpoint allows the client to create a `Customer`.

If the `Customer` is successfully created, the API will return the `Access Token` and set the `Refresh Token` http-cookie.

##### Example request

Request body
```
{
	"email": "user@email.com",
	"first_name": "User",
	"last_name": "Test",
	"password": "password"
	"confirm_password": "confirm_password"
}
```

##### Example response

```
HTTP/1.1 201 Created
Content-Type: application/json
Set-Cookie: refresh_token=<<refresh-token>>; expires:...; Secure; HttpOnly

{
	"id": 2,
	"email": "user@email.com",
	"first_name": "User",
	"last_name": "Test",
	"token": "access_token"
}
```

#### DELETE /customers

This endpoint allows the client with a `Customer` role to delete his account.

##### Example response

```
HTTP/1.1 204 No content
Content-Type: application/json
```

#### GET /customers/orders

This endpoint allows the client with a `Customer` role to retrieve his order history.

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

#### GET /customers/orders/:id

This endpoint allows the client with a `Customer` role to view details about an existing `Order`.

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
