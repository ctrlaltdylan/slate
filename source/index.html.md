---
title: Zenvst API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Zenvst API! This documentation describes how to implement to the API with a mobile client.

# Authentication

TBD. Laravel Passport can use a Bearer Token through a Grant Provider. Needs documentation.

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

# Account Management


## Add Coinbase Access Token to Current User

When the currently logged in user finishes the Coinbase OAuth handshake via the Mobile Client, the Mobile Client will receive 3 pieces of information to communicate on behalf of the user: `access_token`, `refresh_token` and `expires`. Each of these are required to permanently act on behalf of the user.

### HTTP Request

`POST https://zenvst.com/api/v1/self/coinbase/token`

### Body JSON Parameters

Parameter | Required | Type | Description
--------- | -------  | ---- | ----------- 
coinbase_token | true | string | The Coinbase `access_token` provided from the OAuth handshake
refresh_token | true | string |  `refresh_token` provided from the OAuth handshake
expires | true | int | The unix timestamp of when the access_token expires




> The above command returns JSON structured like this:

```json
{
     "message": "Access token and refresh token saved."
}
```

This endpoint stores the Coinbase OAuth tokens after the handshake is complete.

*Note:* you can begin the OAuth handshake on `https://zenvst.com/coinbase/auth`

## Add Plaid Item to Current User

### HTTP Request

`POST https://zenvst.com/api/v1/self/plaid/item`

### Body JSON Parameters

Parameter | Required | Type | Description
--------- | -------  | ---- | ----------- 
public_token | true | string | The Plaid `public_token` provided from the OAuth handshake
metadata | optional | object | A object containing the accounts belonging to the user

> The above command returns JSON structured like this:

```json
{
     "message": "Public token stored.",
     "plaid_item_id": 4,
     "public_token": "oaiwje-aowiefj-aoiwejf-aoiejf"
}
```

## Generate a new Plaid Public Token on behalf of a Item

### HTTP Request

`POST https://zenvst.com/api/v1/plaid/item/{item}/token`

> The above command returns JSON structured like this:

```json
{
  "message": "Plaid token generated",
  "id": 2,
  "public_token": "oawijef-awoeifj-aweoifj-awofeij"
}
```

This endpoint retrieves a specific kitten.

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve



