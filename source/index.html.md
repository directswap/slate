---
title: Direct Swap Deals and Terms API Reference

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Direct Swap API! You can use our API to access Deals and Terms
API endpoints, which you can use to populate and fetch information on Deals,
their associated Terms, and the status of those entities in our database.

We have language bindings in Shell, Ruby, and Python. You can view code examples
in the dark area to the right, and you can switch the programming language of
the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```ruby
require 'direct_swap'

api = DirectSwap::APIClient.authorize!('my-api-key')
```

```python
import directswap

api = directswap.authorize('my-api-key')
```

```shell
# With shell, you can just pass the correct header with each request
curl "users/sign_in"
  -H "Authorization: my-api-key"
```

> Make sure to replace `my-api-key` with your API key.

Direct Swap uses API keys to allow access to the API. You can register a new
Direct Swap API key at our [developer portal](http://directswap.com/developers).

Direct Swap expects for the API key to be included in all API requests to the
server in a header that looks like the following:

`Authorization: my-api-token`

<aside class="notice">
You must replace <code>my-api-token</code> with your personal API key.
</aside>

# Deals

## Get All Deals

```ruby
require 'direct_swap'

api = DirectSwap::APIClient.authorize!('my-api-token')
api.deals.get
```

```python
import directswap

api = directswap.authorize('my-api-token')
api.deals.get()
```

```shell
curl "http://directswap.com/api/deals"
  -H "Authorization: my-api-token"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "",
  },
  {
    "id": 2,
    "name": "",
  }
]
```

This endpoint retrieves all Deals.

### HTTP Request

`GET http://directswap.com/api/deals`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_terms | true | If set to true, the result will also include the term(s) on the deal.

## Get a Specific Deal

```ruby
require 'direct_swap'

api = DirectSwap::APIClient.authorize!('meowmeowmeow')
api.deals.get(2)
```

```python
import directswap

api = directswap.authorize('my-api-token')
api.deals.get(2)
```

```shell
curl "http://directswap.com/api/deals/2"
  -H "Authorization: my-api-token"
```
> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "",
}
```

This endpoint retrieves a specific Deal.

### HTTP Request

`GET http://directswap.com/deals/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Deal to retrieve

## Create a New Deal

```ruby
require 'direct_swap'

api = DirectSwap::APIClient.authorize!('meowmeowmeow')
api.deals.create(deal_hash)
```

```shell
curl "http://directswap.com/api/deals"
  -H "Authorization: my-api-token"
  --data 'param1=a&param2=b&param3=c'
```

```python
import directswap

api = directswap.authorize('my-api-token')
api.deals.create(deal_hash)
```

> The above command returns a JSON representation of the deal that was just
created, structured like this:

```json
{
  "id": 2,
  "name": "",
}
```

### HTTP Request

`POST http://directswap.com/deals`

### URL Parameters

Parameter | Description
--------- | -----------
state | The state of the deal. Deafults to "draft"
product_id | Direct Swap ProductID for the instrument you are offerring
instrument_id | Direct Swap InstrumentID for the instrument you are offering
alternate_id | Your internal reference number for the deal, e.g. "TMS_11235813",
description | Human Readable description of the deal, e.g. "10,000 mmBtu NATURAL GAS-HENRY HUB-NYMEX",
euce_reduces_risk | Affirmation that the deal qualifies for the End User Clearing Exception clause for Reducing Risk, defaults to false
euce_not_subject_to_position_limits | Affirmation that the deal qualifies for the End User Clearing Exception clause for Not Subject To Position Limits, defaults to false
euce_not_speculative | Affirmation that the deal qualifies for the End User Clearing Exception clause with respect to position limits, defaults to false
euce_not_hedging_another_swap |Affirmation that the deal qualifies for the End User Clearing Exception clause with respect to prohibition on hedging another swap, defaults to false
expires_at | Expiration date and time, e.g. Wed, 03 May 2017 00:00:00 UTC +00:00,
name | Name of the deal
sdr_reportable | Whether the deal is currently SDR Reportable, defaults to false




# Terms
## Get Specific Terms
## Add Terms to a deal

# Products
## List All Products

### HTTP Request

`GET http://directswap.com/api/products`

> The above command returns a JSON representation of the deal that was just
created, structured like this:

```json
{ products:
    [
      {
        "id":1,
        "name":"Commodities",
        "parent_id":null,
        "created_at":"2017-05-01T16:45:22.166Z",
        "updated_at":"2017-05-01T16:45:22.166Z"
      },
      {
        "id":2,
        "name":"Agricultural",
        "parent_id":1,
        "created_at":"2017-05-01T16:45:22.167Z",
        "updated_at":"2017-05-01T16:45:22.167Z"
      },
      {
        "id":3,
        "name":"Dairy",
        "parent_id":2,
        "created_at":"2017-05-01T16:45:22.169Z",
        "updated_at":"2017-05-01T16:45:22.169Z"},{"id":4,
          "name":"Butter",
          "parent_id":3,
          "created_at":"2017-05-01T16:45:22.170Z",
          "updated_at":"2017-05-01T16:45:22.170Z"
      },
      {
        "id":5,
        "name":"Cheese",
        "parent_id":3,
        "created_at":"2017-05-01T16:45:22.170Z",
        "updated_at":"2017-05-01T16:45:22.170Z"
      }
    ]
  }
```

## Show a specific Product  

# Instruments
## List all Instruments


### HTTP Request

`GET http://directswap.com/api/instruments`

> The above command returns a JSON representation of the deal that was just
created, structured like this:

```json
{ instruments:
  [
    {
      "id":1,
      "name":"Swap",
      "created_at":"2017-05-01T16:45:22.148Z",
      "updated_at":"2017-05-01T16:45:22.148Z"},
    {
      "id":2,
      "name":"Cap/Floor",
      "created_at":"2017-05-01T16:45:22.150Z",
      "updated_at":"2017-05-01T16:45:22.150Z"
    },{
      "id":3,
      "name":"Forward",
      "created_at":"2017-05-01T16:45:22.151Z",
      "updated_at":"2017-05-01T16:45:22.151Z"
    },{
      "id":4,
      "name":"ISDA Master Agreement",
      "created_at":"2017-05-01T16:45:22.152Z",
      "updated_at":"2017-05-01T16:45:22.152Z"
    }
  ]
}
```

## Show a specific Instrument
