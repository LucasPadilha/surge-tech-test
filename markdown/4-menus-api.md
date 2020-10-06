# Menus API

#### GET /menus/:id

This endpoint allows the client to view details about an existing `Menu`.

This endpoint can be used both by `Customer` or `Owner` and `Manager`.

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 1,
	"name": "Menu 1",
	"items": [
		{
			"id": 1,
			"sku": "sku",
			"name": "Product 1",
			"price": 3.99,
			"description": null,
			"picture": null
		},
		{
			"id": 2,
			"sku": "sku-2",
			"name": "Product 2",
			"price": 9.5,
			"description": "Super product!",
			"picture": "product-2.jpg"
		}
	]
}
```

#### POST /menus

This endpoint allows the client with either an `Owner` or `Manager` role to create a new `Menu`.

##### Example request

Request body
```
{
	"restaurant": {
		"id": 1
	},
	"name": "New Menu",
	"items": [
		{
			"sku": "sku-product",
			"name": "New Product",
			"price": 1.99,
			"description": null,
			"picture": null
		}
	]
}
```

##### Example response

```
HTTP/1.1 201 Created
Content-Type: application/json

{
	"id": 4,
	"restaurant": {
		"id": 1,
		"name": "Restaurant 1"
	},
	"name": "New Menu",
	"items": [
		{
			"id": 5,
			"sku": "sku-product",
			"name": "New Product",
			"price": 1.99,
			"description": null,
			"picture": null
		}
	]
}
```

#### PUT /menus/:id

This endpoint allows the client with either an `Owner` or `Manager` role to update an existing `Menu`.

If the given items have an `id`, the API will look for the given `Product` within the current `Menu`, if the product cannot be found, an `404` error will be thrown.

If no `id` is given, a new `Product` will be created and associated with the `Menu`.

##### Example request

Request body
```
{
	"name": "Menu new name",
	"items": [
		{
			"id": 5,
			"sku": "sku-product",
			"name": "New Product",
			"price": 1.99,
			"description": null,
			"picture": null
		},
		{
			"sku": "sku-new",
			"name": "Newest product",
			"price": 19.99,
			"description": "Super new product",
			"picture": "super-new-product.jpg"
		}
	]
}
```

##### Example response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": 4,
	"name": "Menu new name",
	"items": [
		{
			"id": 5,
			"sku": "sku-product",
			"name": "New Product",
			"price": 1.99,
			"description": null,
			"picture": null
		},
		{
			"id": 6,
			"sku": "sku-new",
			"name": "Newest product",
			"price": 19.99,
			"description": "Super new product",
			"picture": "super-new-product.jpg"
		}
	]
}
```

#### DELETE /menus/:id

This endpoint allows the client with either an `Owner` or `Manager` role to delete an existing `Menu`.

##### Example response

```
HTTP/1.1 204 No content
Content-Type: application/json
```
