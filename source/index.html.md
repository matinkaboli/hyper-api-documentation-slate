---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='http://hyperserver.ir'>Hyper Server API</a>
  - <a href='https://github.com/matinkaboli/hyper'>Hyper Source</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Hyper API! You can use our API to access hyper API endpoints.

This is the first version of Hyper API. So you have to add `v1/` before each endpoint.

# Authentication

```shell
# With shell, you can just pass the header with each request
curl "api_endpoint_here" \
  -H "Authorization: Bearer meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Hyper API uses a key to allow access to the API.

Hyper API expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Users

## Enter a user

```shell
curl "http://hyperserver.ir/v1/users/enter" \
  -d "phone=9127591234&pusheId=pid_20aa-ba40-a0"
```

> The above command returns JSON structured like this:

```json
{
  "isUserNew": false,
  "_id": "5bd312602369091787cd289b",
}
```

This endpoint sends an SMS containing a 6-digit code to user's phone number.

### HTTP Request

`POST http://hyperserver.ir/v1/users/enter`

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
phone | number | 9127591234 | true | User's phone number.
pusheId | string | pid_20aa-ba40-a0 | true | The pushe id of user's device.

<aside class="warning">
Remember — phone number must not have +98, 0098 or 09..
</aside>

### Responses

Status Code | Description
----------- | -----------
422 | When the phone number is invalid.
200 | When everything is OK.

## Login a user

```shell
curl "http://hyperserver.ir/v1/users/login" \
  -d "phone=9127591293&code=123456"
```

> The above command returns JSON structured like this:

```json
{
  "password": true
}
```

> And if the account doesn't have a password:

```json
{
  "password": false,
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1YmQzMTI2MDIzNjkwOTE3ODdjZDI4OWIiLCJpYXQiOjE1NDA1NTk0ODF9.oTLpPdXISHizlxXzbpiZzmcORZQLXx-RAl2OICSl1hQ"
}
```

This endpoint checks the 6-digit code that is sent to your phone number and if it was correct, responses with a JWT token.

### HTTP Request

`POST http://hyperserver.ir/v1/users/login`

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
phone | number | 9127591234 | true | User's phone number.
code | number | 123456 | true | The unique code.

<aside class="warning">
Remember — phone number must not have +98, 0098 or 09..
</aside>

### Responses

Status Code | Description
----------- | -----------
400 | When the code is invalid.
200 | When everything is OK.

## Enter user's password to login

```shell
curl "http://hyperserver.ir/v1/users/password" \
  -d "code=123456&phone=9127591284&password=abcdefghi"
```

> The above command returns JSON structured like this:

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1YmQzMTI2MDIzNjkwOTE3ODdjZDI4OWIiLCJpYXQiOjE1NDA1NTk0ODF9.oTLpPdXISHizlxXzbpiZzmcORZQLXx-RAl2OICSl1hQ"
}
```

This endpoint checks the password of the account and if it was true, it will respond with a JWT token.

### HTTP Request

`POST http://hyperserver.ir/v1/users/password`

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
phone | number | 9127591234 | true | User's phone number.
code | number | 123456 | true | The unique code.
password | string | P@ssw0rD | true | The account's password

<aside class="warning">
Remember — phone number must not have +98, 0098 or 09..
</aside>

### Responses

Status Code | Description
----------- | -----------
400 | When the code is invalid.
400 | When the password is incorrect.
200 | When everything is OK.

## Resend the verification code

```shell
curl "http://hyperserver.ir/v1/users/resend" \
  -d "phone=9127591234"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint sends another OTP code to user's phone number.

### HTTP Request

`POST http://hyperserver.ir/v1/users/resend`

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
phone | number | 9127591234 | true | User's phone number.

<aside class="warning">
Remember — phone number must not have +98, 0098 or 09..
</aside>

### Responses

Status Code | Description
----------- | -----------
204 | When everything is OK.

## Delete a user

```shell
curl "http://hyperserver.ir/v1/users" \
  -H "Authorization: Bearer meowmeowmeow" \
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint delete the user and it's relations in the application.

### HTTP Request

`DELETE http://hyperserver.ir/v1/users`

### Responses

Status Code | Description
----------- | -----------
204 | When everything is OK.

## Check the JWT token

```shell
curl "http://hyperserver.ir/v1/users/tokens/check" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "phone=9127591234"
```

> The above command returns JSON structured like this:

```json
{
  "_id": "5bd312602369091787cd289b"
}
```

This endpoint checks the JWT token.

### HTTP Request

`POST http://hyperserver.ir/v1/users/tokens/check`

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
phone | number | 9127591234 | true | User's phone number.

<aside class="warning">
Remember — phone number must not have +98, 0098 or 09..
</aside>

### Responses

Status Code | Description
----------- | -----------
401 | When the JWT token is wrong.
200 | When everything is OK.

## Delete the JWT token

```shell
curl "http://hyperserver.ir/v1/users/tokens" \
  -H "Authorization: Bearer meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint deletes the JWT token.

### HTTP Request

`DELETE http://hyperserver.ir/v1/users/tokens/`

### Responses

Status Code | Description
----------- | -----------
204 | When everything is OK.

## Change user's name

```shell
curl "http://hyperserver.ir/v1/users/settings/name" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=abcdefghi"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint changes the name of the user.

### HTTP Request

`PATCH http://hyperserver.ir/v1/users/settings/name`

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
name | string | Ahmad | true | The account's name

### Responses

Status Code | Description
----------- | -----------
204 | When everything is OK.

## Change user's password

```shell
curl "http://hyperserver.ir/v1/users/settings/password" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "oldPassword=1234&newPassword=4321&passwordHint=something"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint changes the password and password hint of the user.

### HTTP Request

`PATCH http://hyperserver.ir/v1/users/settings/password`

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
newPassword | string | somethingCool | true | The account's new password
oldPassword | setting | somethingOld | false | The account's old password
passwordHint | string | rememberYourFather | false | Passsword Hint

### Responses

Status Code | Description
----------- | -----------
400 | When the old password is incorrect
204 | When everything is OK.

# Shelves

## Create a shelf

```shell
curl "http://hyperserver.ir/v1/shelves" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=oneshelf"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint creates a new shelf.

### HTTP Request

`POST http://hyperserver.ir/v1/shelves`

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
name | string | Mahsool | true | The shelf's name
isbn | string | 123-456-789-0 | false | The shelf's ISBN
expiration | string | 2 days from now | false | The shelf's expiration time
description | string | One Product | false | The shelf's description
manufacturer | string | Pegah | false | The shelf's manufacturer

### Responses

Status Code | Description
----------- | -----------
201 | When everything is OK.

## Delete a shelf

```shell
curl "http://hyperserver.ir/v1/shelves/:shelfId" \
  -H "Authorization: Bearer meowmeowmeow" \
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint deletes the specified shelf.

### HTTP Request

`DELETE http://hyperserver.ir/v1/shelves/:shelfId`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shelfId | string | 395746irfhjdhgf | true | Shelf's id

### Responses

Status Code | Description
----------- | -----------
404 | When the shelf is not found. 
204 | When everything is OK.

## Update a shelf

```shell
curl "http://hyperserver.ir/v1/shelves/:shelfId" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint updates a shelf.

### HTTP Request

`PATCH http://hyperserver.ir/v1/shelves/:shelfId`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shelfId | string | 395746irfhjdhgf | true | Shelf's id

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
name | string | Mahsool | true | The shelf's name
isbn | string | 123-456-789-0 | false | The shelf's ISBN
expiration | string | 2 days from now | false | The shelf's expiration time
description | string | One Product | false | The shelf's description
manufacturer | string | Pegah | false | The shelf's manufacturer

### Responses

Status Code | Description
----------- | -----------
404 | When the shelf is not found.
200 | When everything is OK.

# Shops

## Create a shop

```shell
curl "http://hyperserver.ir/v1/shops" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint creates a new shop.

### HTTP Request

`POST http://hyperserver.ir/v1/shops`

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
lat | float | 35.2 | true | Shop's latitude
lng | float | 50 | true | Shop's longtitude
name | string | Forooshgah | true | Shop's name
address | string | here | false | Shop's address
description | string | One Product | false | Shop's description
minimumOrderPrice | integer | 20000 | true | Shop's minimum order price
maximumDeliveryTime | integer | 30 | true | Shop's maximum delivery time

### Responses

Status Code | Description
----------- | -----------
201 | When everything is OK.

## Update a shop

```shell
curl "http://hyperserver.ir/v1/shops/:shopId" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint updates the specified shop.

### HTTP Request

`PATCH http://hyperserver.ir/v1/shops`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
lat | float | 35.2 | true | Shop's latitude
lng | float | 50 | true | Shop's longtitude
name | string | Forooshgah | true | Shop's name
address | string | here | false | Shop's address
username | string | irtn34545fgf | false | Shop's username
description | string | One Product | false | Shop's description
minimumOrderPrice | integer | 20000 | true | Shop's minimum order price
maximumDeliveryTime | integer | 30 | true | Shop's maximum delivery time

### Responses

Status Code | Description
----------- | -----------
404 | When shop is not found.
200 | When everything is OK.

## Delete a shop

```shell
curl "http://hyperserver.ir/v1/shops/:shopId" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint deletes the specified shop.

### HTTP Request

`DELETE http://hyperserver.ir/v1/shops/:shopId`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id

### Responses

Status Code | Description
----------- | -----------
404 | When shop is not found.
200 | When everything is OK.

## Follow a shop

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/follow" \
  -H "Authorization: Bearer meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint let the user follow the specified shop.

### HTTP Request

`POST http://hyperserver.ir/v1/shops/:shopId/follow`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id

### Responses

Status Code | Description
----------- | -----------
404 | When shop is not found.
200 | When you have already followed the shop.
201 | When everything is OK.

## Unfollow a shop

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/follow" \
  -H "Authorization: Bearer meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint let the user unfollow the specified shop.

### HTTP Request

`DELETE http://hyperserver.ir/v1/shops/:shopId/follow`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id

### Responses

Status Code | Description
----------- | -----------
404 | When shop is not found.
200 | When you have already unfollowed the shop.
201 | When everything is OK.

## Add a photo for a shop

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/photo" \
  -H "Authorization: Bearer meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint adds an image to the specified shop.

### HTTP Request

`POST http://hyperserver.ir/v1/shops/:shopId/photo`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
photo | file | PNG file | true | Shop's photo

### Responses

Status Code | Description
----------- | -----------
404 | When shop is not found.
201 | When everything is OK.

## Remove a photo for a shop

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/photo/:photoId" \
  -H "Authorization: Bearer meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint removes an image from the specified shop.

### HTTP Request

`DELETE http://hyperserver.ir/v1/shops/:shopId/photo/:photoId`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id
photoId | string | 395746irfhjdhgf | true | Photo's id

### Responses

Status Code | Description
----------- | -----------
404 | When shop is not found.
404 | When photo is not found.
200 | When everything is OK.

# Orders

## Create a new order

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/orders" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint creates a new order for the specified shop.

### HTTP Request

`POST http://hyperserver.ir/v1/shops/:shopId/orders`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
lat | float | 35.2 | true | Order's latitude
lng | float | 50 | true | Order's longtitude
time | string | Tomorrow | true | Order's time
address | string | here | true | Order's address
items | JSON | `{ "items": [{count: 5, showcase: "khkghkf"}, {}, {}] }` | true | Order's items

### Responses

Status Code | Description
----------- | -----------
404 | When shop is not found.
404 | When a showcase ID is not found in the items property.
403 | User must follow the shop in order to create orders.
201 | When everything is OK.

## Update a status of an order

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/orders/:orderId/status" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint creates a new order for the specified shop.

### HTTP Request

`PATCH http://hyperserver.ir/v1/shops/:shopId/orders/:orderId/status`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id
orderId | string | 395746irfhjdhgf | true | Order's id

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
status | string | submitted | true | Order's status

### Responses

Status Code | Description
----------- | -----------
404 | When order is not found.
400 | When status is not valid.
200 | When everything is OK.

# Showcases

## Create a showcase

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/showcases" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint creates a new showcase for the specified shop.

### HTTP Request

`POST http://hyperserver.ir/v1/shops/:shopId/showcases`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
price | number| 2000 | false | The price of the shelf.
shelfId | string | 23947kdkgfkgh | true | Shelf ID.
discountedPrice | number | 1500 | false | The discounted price of the shelf.

### Responses

Status Code | Description
----------- | -----------
404 | When shelf is not found.
404 | When shop is not found.
201 | When everything is OK.

## Delete a showcase

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/showcases/:showcaseId" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint deletes a showcase for the specified shop.

### HTTP Request

`DELETE http://hyperserver.ir/v1/shops/:shopId/showcases/:showcaseId`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id
showcaseId | string | 395746irfhjdhgf | true | Showcase's id

### Responses

Status Code | Description
----------- | -----------
404 | When showcase is not found.
404 | When shop is not found.
200 | When everything is OK.

## Update a showcase

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/showcases/:showcaseId" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint updates a showcase for the specified shop.

### HTTP Request

`PATCH http://hyperserver.ir/v1/shops/:shopId/showcases/:showcaseId`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id
showcaseId | string | 395746irfhjdhgf | true | Showcase's id

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
price | number| 2000 | false | The price of the shelf.
discountedPrice | number | 1500 | false | The discounted price of the shelf.
name | string | Mahsool | true | The shelf's name
isbn | string | 123-456-789-0 | false | The shelf's ISBN
expiration | string | 2 days from now | false | The shelf's expiration time
description | string | One Product | false | The shelf's description
manufacturer | string | Pegah | false | The shelf's manufacturer

### Responses

Status Code | Description
----------- | -----------
404 | When shelf is not found.
404 | When shop is not found.
200 | When everything is OK.

## Create multiple showcases

```shell
curl "http://hyperserver.ir/v1/shops/:shopId/showcases/multi" \
  -H "Authorization: Bearer meowmeowmeow" \
  -d "name=newName"
```

> The above command returns JSON structured like this:

```json
{
}
```

This endpoint creates multiple showcases for the specified shop.

### HTTP Request

`POST http://hyperserver.ir/v1/shops/:shopId/showcases/multi`

### Query Parameteres

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shopId | string | 395746irfhjdhgf | true | Shop's id

### Body Parameters

Parameter | Type | Example | Required | Description
--------- | ---- | ------- | -------- | -----------
shelves | JSON | `{"shelves": [{ shelfId: "aaa", price: 200, discountedPrice: 100 }, {}]}` | true | Multiple shelves in JSON format

### Responses

Status Code | Description
----------- | -----------
404 | When shelf is not found.
404 | When shop is not found.
200 | When everything is OK.
