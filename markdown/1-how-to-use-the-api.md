# How to use the API

## Authentication

This API uses a combination of `Access Token` and `Refresh Token` to authorize access to endpoints.

#### Generating the Tokens

In order to generate the required tokens, the client must make a `POST` request to `/tokens` with the `username` and `password` in a JSON-formatted body.

##### Example request

```
curl -X "POST" "https://api.restaurantmanager.com/tokens" \
	-H "Accept: application/json" \
	-H "Content-Type: application/json" \
	-d "{ \"username\": \"admin\", \"password\": \"password\" }"
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json
Set-Cookie: refresh_token=<<refresh-token>>; expires:...; Secure; HttpOnly

{
	"token": "<<access_token>>"
}
```

#### Authorization Header

To authenticate, the client has to add an `Authorization` header to all API requests with the previously generated `Access Token`.

#### Access Token

To use the `Access Token`, the client must set a plain text header named `Authorization` with the contents of the header being `Bearer XXX` where `XXX` is your `Access Token`. The `Access Token` expires in **60 minutes**.

##### Example Header

```
GET https://api.restaurantmanager.com/resource HTTP/1.1
Authorization: Bearer <<Your-Access-Token-Here>>
```

```
curl -X "GET" "https://api.restaurantmanager.com/resource" \
	-H "Authorization: Bearer <<Your-Access-Token-Here>>" \
	-H "Content-Type: application/json"
```

#### Refresh Token

The `Refresh Token` is generated with the `Access Token` and has a expiration time of **30 days**. During that time, if a request is sent using an expired `Access Token` but with a valid `Refresh Token`, a `401` response will be sent to the client.

##### Example response

```
HTTP/1.1 401 UNAUTHORIZED
Content-Type: application/json

{
	"errors": [
		{
			"field": null,
			"message": "access token needs refresh"
		}
	]
}
```

#### Requesting a new Access Token

In order to request a new `Access Token` the client must make a `GET` request to `/tokens/refresh` with the old `Access Token` in the request headers.

##### Example request

```
GET https://api.restaurantmanager.com/tokens/refresh
Authorization: Bearer <<Your-Expired-Access-Token-Here>>
```

```
curl -X "GET" "https://api.restaurantmanager.com/tokens/refresh" \
	-H "Authorization: Bearer <<Your-Expired-Access-Token-Here>>" \
	-H "Content-Type: application/json"
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json
Set-Cookie: refresh_token=<<refresh-token>>; expires:...; Secure; HttpOnly

{
	"token": "<<new-access-token>>"
}
```

## Authorization

#### Access Token Permissions

The `Access Token` grants the client full access to the API endpoints in behalf of the associated user.

## Requests

#### Making a request

##### Host

The host for the API requests is always `https://api.restaurantmanager.com`

**All requests must be made over HTTPS. The API does not support HTTP.**

##### Authorization header

The client must provide an authorization header as described in `Authentication`.

##### HTTP verbs

| Verb   | Description                               |
|--------|-------------------------------------------|
| GET    | Retrieve a resource or group of resources |
| POST   | Create a new resource                     |
| PUT    | Update an existing resource               |
| DELETE | Delete an existing resource               |

##### Accept header

The API provides JSON responses and expects an `accept` header. If not set, the API will use `application/json`.

```
GET https://api.restaurantmanager.com/resource HTTP/1.1
Accept: application/json
```

#### Formatting your request

##### Request body

When submitting data to a resource via `POST` or `PUT`, the client must submit the payload in JSON.

```
POST https://api.restaurantmanager.com/resource HTTP/1.1
Content-type: application/json
```

```
{
	"name": "new name"
}
```

##### Pagination

Some `GET` resources allow for retrieval of information in batches. The query args are provided in the resource documentation when available to consume.

When requesting multiple items, the API will default the request limit to 25 items. The client can specify a different limit but cannot exceed the default limit.

Below is a basic pagination example.

```
GET https://api.restaurantmanager.com/resource?limit=15&offset=10 HTTP/1.1
```

| Parameter | Description                     |
|-----------|---------------------------------|
| limit     | The number of records to return |
| offset    | The number of records to skip   |

##### Search & Parameters

Some resources allow to search by a specific field. In this example, we will display a paginated URI example, searching for resources where the name contains `foo`.

```
GET https://api.restaurantmanager.com/resource?name=foo&bar=baz HTTP/1.1
```

#### Successful requests

Below is a general overview of what resource objects return with successful API requests.

| Verb   | Description                                                   |
|--------|---------------------------------------------------------------|
| GET    | Returns a single resource object or array of resource objects |
| POST   | Returns the newly created resource object                     |
| PUT    | Returns the updated resource object                           |
| DELETE | No content is returned                                        |

## Responses

#### Content-Type header

All responses are returned in JSON format. We specify this by sending the `content-type` header.

```
GET https://api.restaurantmanager.com/resource HTTP/1.1
```

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"foo": "bar"
}
```

#### Status codes

Below is a table containing descriptions of the various status codes we currently support against various resources.

| Status code | Description             |
|-------------|-------------------------|
| 200         | No error                |
| 201         | Successfully created    |
| 204         | Successfully deleted    |
| 400         | Bad request             |
| 401         | Requires authentication |
| 403         | Requires permission     |
| 404         | Not Found               |
| 500         | Internal server error   |

#### Pagination

When a request is made with a pagination query, the following data is included in the header to allow for easy traversal of previous, current, first and last page of the data set.

```
GET https://api.restaurantmanager.com/resource?limit=5&offset=0 HTTP/1.1
```

```
HTTP/1.1 200 OK
Content-Type: application/json

Pagination-Count: 100
Pagination-Offset: 0
Pagination-Limit: 5
```

## Errors

#### Response codes

| Status code | Description             |
|-------------|-------------------------|
| 400         | Bad request             |
| 401         | Requires authentication |
| 403         | Requires permission     |
| 404         | Not Found               |
| 500         | Internal server error   |

#### Failed requests

```
GET https://api.restaurantmanager.com/resource HTTP/1.1
```

```
HTTP/1.1 400 BAD REQUEST
Content-Type: application/json

{
	"errors": [
		{"field": "identifier", "message": "error message"}
	]
}
```
