# Marketing Campaign API

The marketing campaign API works alongside `Sendgrid's` API to send bulk email marketing campaigns. Through this API the `User` can queue email marketing campaigns to be sent.

Every **15 minutes** a `CRON` script goes through the queue and sends all the scheduled emails.

#### GET /campaigns

This endpoint allows the client with an `Owner` role to retrieve all `Campaigns`.

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
		"name": "Marketing Campaign #1",
		"created_at": "2020-10-02 13:00:00",
		"published_at": "2020-10-04 14:30:00",
		"is_sent": false,
		"template": "<<SENDGRID_TEMPLATE_ID>>"
	},
	{
		"id": 2,
		"name": "Marketing Campaign #2",
		"created_at": "2020-10-02 17:23:00",
		"published_at": "2020-10-08 14:15:00",
		"is_sent": false,
		"template": "<<SENDGRID_TEMPLATE_ID>>"
	}
]
```

#### GET /campaigns/:id

This endpoint allows the client with an `Owner` role to view details about an existing `Campaign`.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 1,
	"name": "Marketing Campaign #1",
	"created_at": "2020-10-02 13:00:00",
	"published_at": "2020-10-04 14:30:00",
	"is_sent": false,
	"template": "<<SENDGRID_TEMPLATE_ID>>",
	"recipients": [
		{
			"id": 1,
			"email": "customer@email.com",
			"first_name": "Customer",
			"last_name": "Name",
		},
		{
			"id": 2,
			"email": "customer2@email.com",
			"first_name": "Customer #2",
			"last_name": "Name",
		}
	]
}
```

#### POST /campaigns

This endpoint allows the client with an `Owner` role to create a new `Campaign`.

##### Example request

Request body
```
{
	"name": "New Campaign",
	"created_at": "2020-10-03 12:25:00",
	"published_at": "2020-10-03 12:25:00",
	"is_sent": false,
	"template": "<<SENDGRID_TEMPLATE_ID>>",
	"recipients": [
		{
			"id": 1
		},
		{
			"id": 2
		},
		{
			"id": 3
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
	"name": "New Campaign",
	"created_at": "2020-10-03 12:25:00",
	"published_at": "2020-10-03 12:25:00",
	"is_sent": false,
	"template": "<<SENDGRID_TEMPLATE_ID>>",
	"recipients": [
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
}
```

#### PUT /campaigns/:id

This endpoint allows the client with an `Owner` role to update an existing `Campaign`.

##### Example request

Request body
```
{
	"name": "New campaign name",
	"recipients": [
		{
			"id": 2
		},
		{
			"id": 3
		}
	]
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json


{
	"id": 3,
	"name": "New campaign name",
	"created_at": "2020-10-03 12:25:00",
	"published_at": "2020-10-03 12:25:00",
	"is_sent": false,
	"template": "<<SENDGRID_TEMPLATE_ID>>",
	"recipients": [
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
}
```

#### DELETE /campaigns/:id

This endpoint allows the client with an `Owner` role to delete an existing `Campaign`.

##### Example response

```
HTTP/1.1 204 No content
Content-Type: application/json
```