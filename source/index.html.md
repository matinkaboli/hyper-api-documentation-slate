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
curl "api_endpoint_here"
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
curl "http://hyperserver.ir/users/enter"
  -H "Authorization: meowmeowmeow"
  -d "phone=9127591234&pusheId=pid_20aa-ba40-a0"
```

> The above command returns JSON structured like this:

```json
{
  "isUserNew": false,
  "_id": "5bd312602369091787cd289b",
}
```

This endpoint sends a sms containing a 6-digit code to user's phone number.

### HTTP Request

`POST http://hyperserver.ir/users/enter`

### Body Parameters

Parameter | Type | Example | Description
--------- | ---- | ------- | -----------
phone | number | 9127591234 | User's phone number.
pusheId | string | pid_20aa-ba40-a0 | The pushe id of user's device.

<aside class="warning">
Remember — phone number must not have +98, 0098 or 09..
</aside>

### Responses

Status Code | Description
----------- | -----------
422 | When the phone number is invalid.
200 | When everything is OK.

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete
