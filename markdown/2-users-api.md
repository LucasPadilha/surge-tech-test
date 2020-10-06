# Users API

#### GET /users/profile

This endpoint allows the client to retrieve the authenticated `User` profile details.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 1,
	"name": "Restaurant Owner",
	"username": "test",
	"role": {
		"id": 1,
		"name": "Owner"
	},
	"restaurants": [
		{
			"id": 1,
			"name": "Restaurant"
		}
	]
}
```

#### PUT /users/profile

This endpoint allows the client to update the authenticated `User` profile details.

Currently the only parameters that can be updated using the `PUT /users/profile` endpoint are `name` and `username`. The request body must contain at least one.

##### Example request

Request body
```
{
	"username": "owner"
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"name": "Restaurant Owner",
	"username": "owner",
	"role": {
		"id": 1,
		"name": "Owner"
	},
	"restaurants": [
		{
			"id": 1,
			"name": "Restaurant"
		}
	]
}
```

#### PUT /users/password

This endpoint allows the client to update the authenticated user password.

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

#### GET /users

This endpoint allows the client with an `Owner` role to retrieve all registered users.

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
		"role": {
			"id": 1,
			"name": "Owner"
		},
		"name": "Owner",
		"username": "owner",
		"restaurants": [
			{
				"id": 1,
				"name": "Restaurant 1"
			},
			{
				"id": 2,
				"name": "Restaurant 2"
			}
		]
	},
	{
		"id": 2,
		"role": {
			"id": 2,
			"name": "Manager"
		},
		"name": "Manager",
		"username": "manager",
		"restaurants": [
			{
				"id": 1,
				"name": "Restaurant 1"
			},
			{
				"id": 2,
				"name": "Restaurant 2"
			}
		]
	}
]
```

#### GET /users/:id

This endpoint allows the client with an `Owner` role to view details about an existing `User`.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": "1",
	"role": {
		"id": 1,
		"name": "Owner"
	},
	"name": "Owner",
	"username": "owner",
	"restaurants": [
		{
			"id": 1,
			"name": "Restaurant 1"
		},
		{
			"id": 2,
			"name": "Restaurant 2"
		}
	]
}
```

#### POST /users

This endpoint allows the client with an `Owner` role to create a new `User`.

##### Example request

Request body
```
{
	"name": "Manager 2",
	"username": "manager-2",
	"role": {
		"id": 2
	}
	"restaurants": [
		{
			"id": 1
		},
		{
			"id": 2
		}
	]
}
```

##### Example response

```
HTTP/1.1 201 Created
Content-Type: application/json

{
	"id": 3,
	"role": {
		"id": 2,
		"name": "Manager"
	},
	"name": "Manager 2",
	"username": "manager-2",
	"restaurants": [
		{
			"id": 1,
			"name": "Restaurant 1"
		},
		{
			"id": 2,
			"name": "Restaurant 2"
		}
	]
}
```

#### PUT /users/:id

This endpoint allows the client with an `Owner` role to update an existing `User`.

##### Example request

Request body
```
{
	"name": "Second manager",
	"username": "second-manager",
	"restaurants": [
		{
			"id": 1
		}
	]
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 2,
	"role": {
		"id": 2,
		"name": "Manager"
	},
	"name": "Second manager",
	"username": "second-manager",
	"restaurants": [
		{
			"id": 1,
			"name": "Restaurant 1"
		}
	]
}
```

#### DELETE /users/:id

This endpoint allows the client with an `Owner` role to delete an existing `User`.

##### Example response

```
HTTP/1.1 204 No content
Content-Type: application/json
```
