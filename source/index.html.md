---
title: C-Trade API 

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the official documentation for the C-Trade APIs and Websocket! Here you can find details on how to access all of our endpoints, their respective expected outputs, and possible errors you may encounter.

# Authentication

> To authorize, use this code:

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Market Data Endpoints

## Get Contracts Menu

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/contracts-menu' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "XBT (Bitcoin)": [
        {
          "name": "XBTUSD",
          "description": "XBTUSD is a XBT/USD perpetual contract priced on the .BXBT Index. Each contract is worth 1 USD of Bitcoin. \n\nFunding is paid and received every 8 hours. The next payout event is at 5:30 PM UTC+5:30.",
          "type": "InversePerpetual",
          "expiryTS": 0,
          "settledIn": "BTC",
          "dependentOnIndex": ".BXBT",
          "underlyingBaseCurrency": "BTC",
          "underlyingQuoteCurrency": "USD",
          "minPriceINC": 0.5,
          "makerFee": -0.025,
          "takerFee": 0.011,
          "maxSize": 10000000,
          "minSize": 1
        },
        {
          "name": "XBTH20",
          "description": "XBTH20 is a XBT/USD futures contract settling on the .BXBT30M Index. Each contract is worth 1 USD of Bitcoin. This contract is ideal for speculation.",
          "type": "Future",
          "expiryTS": 1584642600000,
          "settledIn": "ETH",
          "dependentOnIndex": ".BXBT",
          "underlyingBaseCurrency": "BTC",
          "underlyingQuoteCurrency": "USD",
          "minPriceINC": 0.5,
          "makerFee": -0.025,
          "takerFee": 0.075,
          "maxSize": 100000,
          "minSize": 1
        },
        {
          "name": "XBTM20",
          "description": "XBTM20 is a XBT/USD futures contract settling on the .BXBT30M Index. Each contract is worth 1 USD of Bitcoin. This contract is ideal for speculation.",
          "type": "InverseFuture",
          "expiryTS": 1593109800000,
          "settledIn": "BTC",
          "dependentOnIndex": ".BXBT",
          "underlyingBaseCurrency": "BTC",
          "underlyingQuoteCurrency": "USD",
          "minPriceINC": 1,
          "makerFee": -0.025,
          "takerFee": 0.075,
          "maxSize": 1000000,
          "minSize": 1
        }
      ],
      "gg": [
        {
          "name": "TEST",
          "description": "testing",
          "type": "Perpetual",
          "expiryTS": 0,
          "settledIn": "ETH",
          "dependentOnIndex": ".USDBON",
          "underlyingBaseCurrency": "EE",
          "underlyingQuoteCurrency": "E",
          "minPriceINC": 1,
          "makerFee": 1,
          "takerFee": 1,
          "maxSize": 100000,
          "minSize": 1
        }
      ]
    }
  }
}
```

This endpoint retrieves contracts menu.

### HTTP Request

`GET https://bff.goesoteric.com/public/contracts-menu`

## Get Contract Detail

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/contracts/ETHBTC' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "name": "ETHBTC",
      "aliasName": "EthBitcoin",
      "groupName": "Bitcoin",
      "underlyingQuoteCurrency": "BTC",
      "underlyingBaseCurrency": "ETH",
      "type": "Vanila Futures",
      "currentPrice": 0,
      "fairPrice": 0,
      "changePerc": 0,
      "initialMargin": 50,
      "maintainceMargin": 25,
      "maxLeverage": 1,
      "makerFee": 0,
      "takerFee": 0,
      "settlementFee": 0,
      "maxOrderQuantity": 0,
      "minOrderQuantity": 0,
      "maxPrice": 0,
      "minPrice": 0,
      "dailyTurnOver": 0,
      "totalVolume": 0,
      "refrenceUrl": "https://example.com/",
      "nextFundingTS": 946684800000,
      "interestBase": 0,
      "interestQuote": 0,
      "premium": 0,
      "longFundingRate": 0,
      "shortFundingRate": 0,
      "fundingInterval": 6,
      "addedOnTS": 946684800000,
      "validTillTS": 32503593600000,
      "status": false
    }
  }
}
```

This endpoint retrieves a specific contract detail.

### HTTP Request

`GET https://bff.goesoteric.com/public/contracts/<contractsymbol>`

### URL Parameters

Parameter | Description
--------- | -----------
contractsymbol | The symbol of the contract

## Get Charts

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/charts/ETHBTC/1M?limit=100&ts=1574813820000'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      [
        1575352620000,
        0.02034625,
        0.0203485,
        0.02035075,
        0.0203445,
        0
      ],
      [
        1575352560000,
        0.0203465,
        0.02034625,
        0.0203465,
        0.02033875,
        0
      ],
      [
        1575352500000,
        0.0203465,
        0.0203465,
        0.020355,
        0.020346,
        0
      ],
      [
        1575352440000,
        0.020346,
        0.0203465,
        0.0203475,
        0.020342,
        0
      ],
      [
        1575352380000,
        0.02034725,
        0.020346,
        0.02035025,
        0.020346,
        0
      ],
      [
        1575352320000,
        0.020349,
        0.02034725,
        0.02034875,
        0.020346,
        0
      ],
      [
        1575352260000,
        0.0203465,
        0.020349,
        0.02034925,
        0.020345,
        0
      ],
      [
        1575352200000,
        0.02034175,
        0.0203465,
        0.02034775,
        0.020341,
        0
      ],
      [
        1575352140000,
        0.020332,
        0.02034175,
        0.0203445,
        0.02033175,
        0
      ],
      [
        1575352080000,
        0.0203315,
        0.020332,
        0.02033375,
        0.02033025,
        0
      ],
      [
        1575352020000,
        0.020336,
        0.0203315,
        0.0203335,
        0.020331,
        0
      ],
      [
        1575351960000,
        0.02033325,
        0.020336,
        0.0203375,
        0.02033225,
        0
      ],
      [
        1575351900000,
        0.020333,
        0.02033325,
        0.02033525,
        0.02033325,
        0
      ],
      [
        1575351840000,
        0.0203355,
        0.020333,
        0.020336,
        0.02033075,
        0
      ],
      [
        1575351780000,
        0.02033775,
        0.0203355,
        0.020337,
        0.020331,
        0
      ],
      [
        1575351720000,
        0.020341,
        0.02033775,
        0.02034225,
        0.020337,
        0
      ],
      [
        1575351660000,
        0.0203882,
        0.020341,
        0.020343,
        0.02033575,
        0
      ],
      [
        1575351600000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351540000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351480000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351420000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351360000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351300000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351240000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351180000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351120000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351060000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575351000000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350940000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350880000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350820000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350760000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350700000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350640000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350580000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350520000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350460000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350400000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350340000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350280000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350220000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350160000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350100000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575350040000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349980000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349920000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349860000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349800000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349740000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349680000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349620000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349560000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349500000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349440000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349380000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349320000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349260000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349200000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349140000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349080000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575349020000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348960000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348900000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348840000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348780000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348720000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348660000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348600000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348540000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348480000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348420000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348360000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348300000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348240000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348180000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348120000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348060000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575348000000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347940000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347880000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347820000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347760000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347700000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347640000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347580000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347520000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347460000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347400000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347340000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347280000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347220000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347160000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347100000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575347040000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575346980000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575346920000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575346860000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575346800000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575346740000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ],
      [
        1575346680000,
        0.0203882,
        0.0203882,
        0.0203882,
        0.0203882,
        0
      ]
    ]
  }
}
```

This endpoint retrieves charts of a specific contract detail.

### HTTP Request

`GET https://bff.goesoteric.com/public/charts/<contractsymbol>/<interval>`

### URL Parameters

Parameter | Description
--------- | -----------
contractsymbol | The symbol of the contract
interval | The interval of charts

### Request Parameters

Parameter | Required | Description
--------- | ----------- | -----------
limit | false | Limit for data size per page
ts | false | From timestamp in milliseconds

## Get Indices List

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/indices-hierarchy' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "ASED": [
        {
          "name": "ASED",
          "aliasName": "ASED"
        }
      ],
      "AESR": [
        {
          "name": "AESR",
          "aliasName": "AESR"
        }
      ],
      "LTC Group": [
        {
          "name": "LTCUTC",
          "aliasName": "LTC Name"
        },
        {
          "name": "LTCWTC",
          "aliasName": "LTC Name"
        }
      ],
      "Bitcoin": [
        {
          "name": "LTCBTC",
          "aliasName": "LtcBitcoin"
        },
        {
          "name": "ETHBTC",
          "aliasName": "EthBitcoin"
        }
      ],
      "NTX": [
        {
          "name": "NTX",
          "aliasName": "NTX"
        }
      ],
      "BTCR Group": [
        {
          "name": "BTCR",
          "aliasName": "BTCR Name"
        }
      ],
      "UTHBTC Group": [
        {
          "name": "UTHBTC",
          "aliasName": "UTHBTC Name"
        }
      ],
      "AAWE": [
        {
          "name": "AAWE",
          "aliasName": "AAWE"
        }
      ],
      "ASDF group": [
        {
          "name": "ASDF",
          "aliasName": "ASDF name"
        }
      ],
      "AZZ": [
        {
          "name": "AZZ",
          "aliasName": "AZZ"
        }
      ],
      "BTHX": [
        {
          "name": "BTHX",
          "aliasName": "BTHX"
        }
      ],
      "WETR Group": [
        {
          "name": "WETR",
          "aliasName": "WETR Name"
        }
      ],
      "ERT": [
        {
          "name": "ERT",
          "aliasName": "ERT"
        },
        {
          "name": "ERTR",
          "aliasName": "ERT"
        }
      ],
      "AXZ": [
        {
          "name": "AXZ",
          "aliasName": "AXZ"
        }
      ],
      "ETHBTH Group": [
        {
          "name": "ETHBTH",
          "aliasName": "ETHBTH Name"
        }
      ],
      "GTX": [
        {
          "name": "GTX",
          "aliasName": "GTX"
        }
      ],
      "XRT": [
        {
          "name": "XRT",
          "aliasName": "XRT"
        }
      ],
      "AZX": [
        {
          "name": "AZX",
          "aliasName": "AZX"
        }
      ],
      "AST Group": [
        {
          "name": "AST",
          "aliasName": "AST Name"
        }
      ],
      "AASE": [
        {
          "name": "AASE",
          "aliasName": "AASE"
        }
      ],
      "BTCET Group": [
        {
          "name": "BTCET",
          "aliasName": "BTCET name"
        }
      ],
      "ERXCR Group": [
        {
          "name": "ERXCR",
          "aliasName": "ERXCR Name"
        }
      ],
      "ETTX": [
        {
          "name": "ETTX",
          "aliasName": "ETTX"
        }
      ],
      "Bitcoin Update": [
        {
          "name": "ETHBIC",
          "aliasName": "EthBitcoin"
        }
      ],
      "ATHBTC Group": [
        {
          "name": "ATHBTC",
          "aliasName": "ATHBTC"
        }
      ],
      "ASD": [
        {
          "name": "ASD",
          "aliasName": "ASD"
        }
      ]
    }
  }
}
```

This endpoint retrieves indices list.

### HTTP Request

`GET https://bff.goesoteric.com/public/indices-hierarchy`

### URL Parameters

Parameter | Description
--------- | -----------
contractsymbol | The symbol of the contract

## Get Indices Details

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/indices-detailed-breakdown/.BXBT/1'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "composite_breakdown": [
        {
          "ts": 1580131620000,
          "exchange": "okex",
          "price": 0.0193736667,
          "weightage": 30
        },
        {
          "ts": 1580131620000,
          "exchange": "kraken",
          "price": 0.0193803333,
          "weightage": 20
        },
        {
          "ts": 1580131620000,
          "exchange": "coinbase",
          "price": 0.01937,
          "weightage": 10
        },
        {
          "ts": 1580131620000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131620000,
          "exchange": "binance",
          "price": 0.0193796333,
          "weightage": 20
        },
        {
          "ts": 1580131560000,
          "exchange": "okex",
          "price": 0.0193703333,
          "weightage": 30
        },
        {
          "ts": 1580131560000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131560000,
          "exchange": "coinbase",
          "price": 0.01937,
          "weightage": 10
        },
        {
          "ts": 1580131560000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131560000,
          "exchange": "binance",
          "price": 0.0193778833,
          "weightage": 20
        },
        {
          "ts": 1580131500000,
          "exchange": "okex",
          "price": 0.0193728333,
          "weightage": 30
        },
        {
          "ts": 1580131500000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131500000,
          "exchange": "coinbase",
          "price": 0.0193786667,
          "weightage": 10
        },
        {
          "ts": 1580131500000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131500000,
          "exchange": "binance",
          "price": 0.0193794167,
          "weightage": 20
        },
        {
          "ts": 1580131440000,
          "exchange": "okex",
          "price": 0.0193683333,
          "weightage": 30
        },
        {
          "ts": 1580131440000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131440000,
          "exchange": "coinbase",
          "price": 0.0193866667,
          "weightage": 10
        },
        {
          "ts": 1580131440000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131440000,
          "exchange": "binance",
          "price": 0.0193773667,
          "weightage": 20
        },
        {
          "ts": 1580131380000,
          "exchange": "okex",
          "price": 0.0193775,
          "weightage": 30
        },
        {
          "ts": 1580131380000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131380000,
          "exchange": "coinbase",
          "price": 0.0194003333,
          "weightage": 10
        },
        {
          "ts": 1580131380000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131380000,
          "exchange": "binance",
          "price": 0.0193811667,
          "weightage": 20
        },
        {
          "ts": 1580131320000,
          "exchange": "okex",
          "price": 0.0193793333,
          "weightage": 30
        },
        {
          "ts": 1580131320000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131320000,
          "exchange": "coinbase",
          "price": 0.0194036667,
          "weightage": 10
        },
        {
          "ts": 1580131320000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131320000,
          "exchange": "binance",
          "price": 0.0193896667,
          "weightage": 20
        },
        {
          "ts": 1580131260000,
          "exchange": "okex",
          "price": 0.0193838333,
          "weightage": 30
        },
        {
          "ts": 1580131260000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131260000,
          "exchange": "coinbase",
          "price": 0.019393,
          "weightage": 10
        },
        {
          "ts": 1580131260000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131260000,
          "exchange": "binance",
          "price": 0.0193934,
          "weightage": 20
        },
        {
          "ts": 1580131200000,
          "exchange": "okex",
          "price": 0.0193891667,
          "weightage": 30
        },
        {
          "ts": 1580131200000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131200000,
          "exchange": "coinbase",
          "price": 0.0193936667,
          "weightage": 10
        },
        {
          "ts": 1580131200000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131200000,
          "exchange": "binance",
          "price": 0.0193959,
          "weightage": 20
        },
        {
          "ts": 1580131140000,
          "exchange": "okex",
          "price": 0.0193968333,
          "weightage": 30
        },
        {
          "ts": 1580131140000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131140000,
          "exchange": "coinbase",
          "price": 0.0194013333,
          "weightage": 10
        },
        {
          "ts": 1580131140000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131140000,
          "exchange": "binance",
          "price": 0.0194010833,
          "weightage": 20
        },
        {
          "ts": 1580131080000,
          "exchange": "okex",
          "price": 0.0193973333,
          "weightage": 30
        },
        {
          "ts": 1580131080000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131080000,
          "exchange": "coinbase",
          "price": 0.0194011667,
          "weightage": 10
        },
        {
          "ts": 1580131080000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131080000,
          "exchange": "binance",
          "price": 0.0194073167,
          "weightage": 20
        },
        {
          "ts": 1580131020000,
          "exchange": "okex",
          "price": 0.0193921667,
          "weightage": 30
        },
        {
          "ts": 1580131020000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580131020000,
          "exchange": "coinbase",
          "price": 0.0193941667,
          "weightage": 10
        },
        {
          "ts": 1580131020000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580131020000,
          "exchange": "binance",
          "price": 0.0194010667,
          "weightage": 20
        },
        {
          "ts": 1580130960000,
          "exchange": "okex",
          "price": 0.0193783333,
          "weightage": 30
        },
        {
          "ts": 1580130960000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580130960000,
          "exchange": "coinbase",
          "price": 0.01937,
          "weightage": 10
        },
        {
          "ts": 1580130960000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580130960000,
          "exchange": "binance",
          "price": 0.0193880167,
          "weightage": 20
        },
        {
          "ts": 1580130900000,
          "exchange": "okex",
          "price": 0.01937,
          "weightage": 30
        },
        {
          "ts": 1580130900000,
          "exchange": "kraken",
          "price": 0.019389,
          "weightage": 20
        },
        {
          "ts": 1580130900000,
          "exchange": "coinbase",
          "price": 0.01937,
          "weightage": 10
        },
        {
          "ts": 1580130900000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580130900000,
          "exchange": "binance",
          "price": 0.0193811167,
          "weightage": 20
        },
        {
          "ts": 1580130840000,
          "exchange": "okex",
          "price": 0.0193673333,
          "weightage": 30
        },
        {
          "ts": 1580130840000,
          "exchange": "kraken",
          "price": 0.019378,
          "weightage": 20
        },
        {
          "ts": 1580130840000,
          "exchange": "coinbase",
          "price": 0.0193796667,
          "weightage": 10
        },
        {
          "ts": 1580130840000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580130840000,
          "exchange": "binance",
          "price": 0.0193730833,
          "weightage": 20
        },
        {
          "ts": 1580130780000,
          "exchange": "okex",
          "price": 0.019369,
          "weightage": 30
        },
        {
          "ts": 1580130780000,
          "exchange": "kraken",
          "price": 0.01939,
          "weightage": 20
        },
        {
          "ts": 1580130780000,
          "exchange": "coinbase",
          "price": 0.0193798333,
          "weightage": 10
        },
        {
          "ts": 1580130780000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580130780000,
          "exchange": "binance",
          "price": 0.0193760333,
          "weightage": 20
        },
        {
          "ts": 1580130720000,
          "exchange": "okex",
          "price": 0.0193716667,
          "weightage": 30
        },
        {
          "ts": 1580130720000,
          "exchange": "kraken",
          "price": 0.0193825,
          "weightage": 20
        },
        {
          "ts": 1580130720000,
          "exchange": "coinbase",
          "price": 0.01937,
          "weightage": 10
        },
        {
          "ts": 1580130720000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580130720000,
          "exchange": "binance",
          "price": 0.0193776833,
          "weightage": 20
        },
        {
          "ts": 1580130660000,
          "exchange": "okex",
          "price": 0.0193698333,
          "weightage": 30
        },
        {
          "ts": 1580130660000,
          "exchange": "kraken",
          "price": 0.01938,
          "weightage": 20
        },
        {
          "ts": 1580130660000,
          "exchange": "coinbase",
          "price": 0.0193756667,
          "weightage": 10
        },
        {
          "ts": 1580130660000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580130660000,
          "exchange": "binance",
          "price": 0.01937735,
          "weightage": 20
        },
        {
          "ts": 1580130600000,
          "exchange": "okex",
          "price": 0.0193718333,
          "weightage": 30
        },
        {
          "ts": 1580130600000,
          "exchange": "kraken",
          "price": 0.01938,
          "weightage": 20
        },
        {
          "ts": 1580130600000,
          "exchange": "coinbase",
          "price": 0.0193733333,
          "weightage": 10
        },
        {
          "ts": 1580130600000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580130600000,
          "exchange": "binance",
          "price": 0.0193820833,
          "weightage": 20
        },
        {
          "ts": 1580130540000,
          "exchange": "okex",
          "price": 0.0193716667,
          "weightage": 30
        },
        {
          "ts": 1580130540000,
          "exchange": "kraken",
          "price": 0.0193801667,
          "weightage": 20
        },
        {
          "ts": 1580130540000,
          "exchange": "coinbase",
          "price": 0.0193715,
          "weightage": 10
        },
        {
          "ts": 1580130540000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580130540000,
          "exchange": "binance",
          "price": 0.01938025,
          "weightage": 20
        },
        {
          "ts": 1580130480000,
          "exchange": "okex",
          "price": 0.0193706667,
          "weightage": 30
        },
        {
          "ts": 1580130480000,
          "exchange": "kraken",
          "price": 0.01938,
          "weightage": 20
        },
        {
          "ts": 1580130480000,
          "exchange": "coinbase",
          "price": 0.01938,
          "weightage": 10
        },
        {
          "ts": 1580130480000,
          "exchange": "bitfinix",
          "price": 0.019223,
          "weightage": 20
        },
        {
          "ts": 1580130480000,
          "exchange": "binance",
          "price": 0.0193805167,
          "weightage": 20
        }
      ],
      "indices_using_this": [
        ".BXBTJPY",
        ".BXBT30M",
        ".BXBTJPY30M",
        ".XBTJPY30M"
      ],
      "contracts_using_this": [
        "TRXH20",
        "XBTH20",
        "BCHH20",
        "EOSH20",
        "ETHUSD",
        "ETHH20",
        "LTCH20",
        "XRPH20"
      ]
    }
  }
}
```

This endpoint retrieves details of a specific index.

### HTTP Request

`GET https://bff.goesoteric.com/public/indices-detailed-breakdown/<index>/<todo>`

### URL Parameters

Parameter | Description
--------- | -----------
index | The index 
todo | todo

## Get Index Data

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/indices/ETHBTC/1?limit=500&ts=1575465605000'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "1575526080000": 0.0198514792,
      "1575526020000": 0.0198466875,
      "1575525960000": 0.0198418708,
      "1575525900000": 0.0198365833,
      "1575525840000": 0.0198352625,
      "1575525780000": 0.0198287083,
      "1575525720000": 0.0198319167,
      "1575525660000": 0.0198282167,
      "1575525600000": 0.0198256625,
      "1575525540000": 0.0198257458,
      "1575525480000": 0.0198243708,
      "1575525420000": 0.0198236875,
      "1575525360000": 0.0198235625,
      "1575525300000": 0.0198266958,
      "1575525240000": 0.019828125,
      "1575525180000": 0.0198328417,
      "1575525120000": 0.0198271958,
      "1575525060000": 0.0198272042,
      "1575525000000": 0.0198370917,
      "1575524940000": 0.0198313875,
      "1575524880000": 0.0198276125,
      "1575524820000": 0.0198266375,
      "1575524760000": 0.0198385833,
      "1575524700000": 0.0198413958,
      "1575524640000": 0.0198425208,
      "1575524580000": 0.0198431195,
      "1575524520000": 0.0198418417,
      "1575524460000": 0.0198356,
      "1575524400000": 0.0198286375,
      "1575524340000": 0.0198197583,
      "1575524280000": 0.0198210417,
      "1575524220000": 0.0198323792,
      "1575524160000": 0.0198252208,
      "1575524100000": 0.0198542208,
      "1575524040000": 0.01986355,
      "1575523980000": 0.0198738333,
      "1575523920000": 0.0198844333,
      "1575523860000": 0.0198860583,
      "1575523800000": 0.019871975,
      "1575523740000": 0.0198679417,
      "1575523680000": 0.0198751417,
      "1575523620000": 0.0199085375,
      "1575523560000": 0.01990945,
      "1575523500000": 0.0199156792,
      "1575523440000": 0.0199241458,
      "1575523380000": 0.0199197708,
      "1575523320000": 0.0199178398,
      "1575523260000": 0.0199185208,
      "1575523200000": 0.0199219375,
      "1575523140000": 0.0199163292,
      "1575523080000": 0.0199166583,
      "1575523020000": 0.0199264625,
      "1575522960000": 0.0199235667,
      "1575522900000": 0.0199263667,
      "1575522840000": 0.019928525,
      "1575522780000": 0.0199307345,
      "1575522720000": 0.0199307125,
      "1575522660000": 0.0199334667,
      "1575522600000": 0.0199384083,
      "1575522540000": 0.0199475083,
      "1575522480000": 0.0199523292,
      "1575522420000": 0.0199524333,
      "1575522360000": 0.0199568125,
      "1575522300000": 0.0199632833,
      "1575522240000": 0.0199645833,
      "1575522180000": 0.0199654583,
      "1575522120000": 0.0199655833,
      "1575522060000": 0.0199659792,
      "1575522000000": 0.0199686237,
      "1575521940000": 0.0199656583,
      "1575521880000": 0.0199667708,
      "1575521820000": 0.0199686208,
      "1575521760000": 0.0199684958,
      "1575521700000": 0.0199709958,
      "1575521640000": 0.0199754333,
      "1575521580000": 0.0199739917,
      "1575521520000": 0.0199738059,
      "1575521460000": 0.0199823875,
      "1575521400000": 0.0199816292,
      "1575521340000": 0.0199809417,
      "1575521280000": 0.0199867708,
      "1575521220000": 0.0199894754,
      "1575521160000": 0.019993875,
      "1575521100000": 0.0199865208,
      "1575521040000": 0.0199746125,
      "1575520980000": 0.0199477375,
      "1575520920000": 0.0199017593,
      "1575520860000": 0.0198870917,
      "1575520800000": 0.0198566125,
      "1575520740000": 0.0199382125,
      "1575520680000": 0.0199431042,
      "1575520620000": 0.0199511625,
      "1575520560000": 0.0199533,
      "1575520500000": 0.0199543,
      "1575520440000": 0.0199504792,
      "1575520380000": 0.0199505292,
      "1575520320000": 0.0199489833,
      "1575520260000": 0.0199479042,
      "1575520200000": 0.0199485042,
      "1575520140000": 0.0199487042,
      "1575520080000": 0.0199487542,
      "1575520020000": 0.0199485667,
      "1575519960000": 0.0199485417,
      "1575519900000": 0.0199490625,
      "1575519840000": 0.019951575,
      "1575519780000": 0.019953025,
      "1575519720000": 0.0199519583,
      "1575519660000": 0.0199456208,
      "1575519600000": 0.0199489042,
      "1575519540000": 0.0199564042,
      "1575519480000": 0.0199604625,
      "1575519420000": 0.0199637708,
      "1575519360000": 0.019964325,
      "1575519300000": 0.0199664,
      "1575519240000": 0.0199680875,
      "1575519180000": 0.0199703208,
      "1575519120000": 0.0199738875,
      "1575519060000": 0.0199756625,
      "1575519000000": 0.0199743458,
      "1575518940000": 0.0199719875,
      "1575518880000": 0.0199670708,
      "1575518820000": 0.0199630958,
      "1575518760000": 0.0199653,
      "1575518700000": 0.0199692833,
      "1575518640000": 0.0199684625,
      "1575518580000": 0.0199680208,
      "1575518520000": 0.0199628792,
      "1575518460000": 0.0199647792,
      "1575518400000": 0.0199631667,
      "1575518340000": 0.01996045,
      "1575518280000": 0.0199631875,
      "1575518220000": 0.01996605,
      "1575518160000": 0.0199649458,
      "1575518100000": 0.0199640583,
      "1575518040000": 0.0199585583,
      "1575517980000": 0.0199569208,
      "1575517920000": 0.0199556833,
      "1575517860000": 0.0199525417,
      "1575517800000": 0.0199528542,
      "1575517740000": 0.01995325,
      "1575517680000": 0.0199486915,
      "1575517620000": 0.0199499625,
      "1575517560000": 0.0199548417,
      "1575517500000": 0.0199582208,
      "1575517440000": 0.0199739833,
      "1575517380000": 0.0199776875,
      "1575517320000": 0.0199801292,
      "1575517260000": 0.0199813125,
      "1575517200000": 0.01998,
      "1575517140000": 0.019981375,
      "1575517080000": 0.0199819,
      "1575517020000": 0.0199857583,
      "1575516960000": 0.0199901625,
      "1575516900000": 0.01998735,
      "1575516840000": 0.0199858,
      "1575516780000": 0.0199839875,
      "1575516720000": 0.0199798708,
      "1575516660000": 0.0199682292,
      "1575516600000": 0.0199642208,
      "1575516540000": 0.0199606042,
      "1575516480000": 0.0199529875,
      "1575516420000": 0.0199522708,
      "1575516360000": 0.0199503992,
      "1575516300000": 0.0199466583,
      "1575516240000": 0.01994815,
      "1575516180000": 0.0199468017,
      "1575516120000": 0.0199456292,
      "1575516060000": 0.0199415167,
      "1575516000000": 0.0199365,
      "1575515940000": 0.0199355542,
      "1575515880000": 0.0199356458,
      "1575515820000": 0.0199380542,
      "1575515760000": 0.0199378583,
      "1575515700000": 0.0199372542,
      "1575515640000": 0.0199340583,
      "1575515580000": 0.0199334625,
      "1575515520000": 0.0199359331,
      "1575515460000": 0.019937175,
      "1575515400000": 0.0199373,
      "1575515340000": 0.0199380833,
      "1575515280000": 0.0199393833,
      "1575515220000": 0.0199455208,
      "1575515160000": 0.019945825,
      "1575515100000": 0.0199419,
      "1575515040000": 0.0199420458,
      "1575514980000": 0.019946525,
      "1575514920000": 0.0199408458,
      "1575514860000": 0.0199337625,
      "1575514800000": 0.0199335958,
      "1575514740000": 0.0199382542,
      "1575514680000": 0.0199468708,
      "1575514620000": 0.0199578458,
      "1575514560000": 0.0199613708,
      "1575514500000": 0.0199601542,
      "1575514440000": 0.0199622,
      "1575514380000": 0.0199594458,
      "1575514320000": 0.0199569917,
      "1575514260000": 0.019958,
      "1575514200000": 0.0199559458,
      "1575514140000": 0.019953975,
      "1575514080000": 0.0199537542,
      "1575514020000": 0.0199563208,
      "1575513960000": 0.0199565833,
      "1575513900000": 0.0199567212,
      "1575513840000": 0.0199575898,
      "1575513780000": 0.0199607792,
      "1575513720000": 0.0199606292,
      "1575513660000": 0.01996165,
      "1575513600000": 0.0199581792,
      "1575513540000": 0.0199588167,
      "1575513480000": 0.0199630583,
      "1575513420000": 0.0199634155,
      "1575513360000": 0.0199632417,
      "1575513300000": 0.0199623583,
      "1575513240000": 0.0199640542,
      "1575513180000": 0.0199636333,
      "1575513120000": 0.0199595,
      "1575513060000": 0.019957025,
      "1575513000000": 0.0199549458,
      "1575512940000": 0.0199541625,
      "1575512880000": 0.0199529373,
      "1575512820000": 0.0199538875,
      "1575512760000": 0.0199573667,
      "1575512700000": 0.0199571125,
      "1575512640000": 0.0199596208,
      "1575512580000": 0.0199620917,
      "1575512520000": 0.0199652625,
      "1575512460000": 0.01997005,
      "1575512400000": 0.0199743356,
      "1575512340000": 0.0199792625,
      "1575512280000": 0.019983775,
      "1575512220000": 0.0199867875,
      "1575512160000": 0.0199912424,
      "1575512100000": 0.0199927167,
      "1575512040000": 0.019998075,
      "1575511980000": 0.0200009583,
      "1575511920000": 0.0200009167,
      "1575511860000": 0.020003775,
      "1575511800000": 0.0200082875,
      "1575511740000": 0.020012925,
      "1575511680000": 0.0200205625,
      "1575511620000": 0.0200246333,
      "1575511560000": 0.0200284833,
      "1575511500000": 0.020028175,
      "1575511440000": 0.02003,
      "1575511380000": 0.0200332417,
      "1575511320000": 0.0200393875,
      "1575511260000": 0.0200447,
      "1575511200000": 0.0200456375,
      "1575511140000": 0.0200417792,
      "1575511080000": 0.0200382542,
      "1575511020000": 0.0200420208,
      "1575510960000": 0.0200426458,
      "1575510900000": 0.0200385958,
      "1575510840000": 0.0200426167,
      "1575510780000": 0.0200442333,
      "1575510720000": 0.0200458833,
      "1575510660000": 0.0200463625,
      "1575510600000": 0.020051875,
      "1575510540000": 0.0200542292,
      "1575510480000": 0.0200603417,
      "1575510420000": 0.020064375,
      "1575510360000": 0.0200676407,
      "1575510300000": 0.0200702833,
      "1575510240000": 0.0200697375,
      "1575510180000": 0.0200674292,
      "1575510120000": 0.0200625917,
      "1575510060000": 0.0200638042,
      "1575510000000": 0.0200627667,
      "1575509940000": 0.0200613708,
      "1575509880000": 0.0200609585,
      "1575509820000": 0.0200605875,
      "1575509760000": 0.0200585792,
      "1575509700000": 0.0200569333,
      "1575509640000": 0.02005715,
      "1575509580000": 0.0200627583,
      "1575509520000": 0.0200632833,
      "1575509460000": 0.0200591792,
      "1575509400000": 0.0200581375,
      "1575509340000": 0.020057775,
      "1575509280000": 0.0200545458,
      "1575509220000": 0.0200534875,
      "1575509160000": 0.0200534083,
      "1575509100000": 0.0200523417,
      "1575509040000": 0.0200523042,
      "1575508980000": 0.0200518292,
      "1575508920000": 0.0200495708,
      "1575508860000": 0.0200462083,
      "1575508800000": 0.0200419417,
      "1575508740000": 0.0200414625,
      "1575508680000": 0.020040275,
      "1575508620000": 0.0200406833,
      "1575508560000": 0.0200412958,
      "1575508500000": 0.0200424288,
      "1575508440000": 0.0200392792,
      "1575508380000": 0.0200361417,
      "1575508320000": 0.0200363708,
      "1575508260000": 0.0200331875,
      "1575508200000": 0.0200290292,
      "1575508140000": 0.020030975,
      "1575508080000": 0.0200326833,
      "1575508020000": 0.0200311458,
      "1575507960000": 0.0200318042,
      "1575507900000": 0.0200353375,
      "1575507840000": 0.0200395093,
      "1575507780000": 0.0200384542,
      "1575507720000": 0.0200382583,
      "1575507660000": 0.0200393375,
      "1575507600000": 0.020042325,
      "1575507540000": 0.0200428333,
      "1575507480000": 0.0200425542,
      "1575507420000": 0.02004015,
      "1575507360000": 0.0200394542,
      "1575507300000": 0.0200372958,
      "1575507240000": 0.0200405958,
      "1575507180000": 0.0200404119,
      "1575507120000": 0.0200381125,
      "1575507060000": 0.02003675,
      "1575507000000": 0.0200405208,
      "1575506940000": 0.0200422333,
      "1575506880000": 0.0200421,
      "1575506820000": 0.02004155,
      "1575506760000": 0.020040725,
      "1575506700000": 0.0200405333,
      "1575506640000": 0.0200422125,
      "1575506580000": 0.0200434958,
      "1575506520000": 0.020044475,
      "1575506460000": 0.0200408417,
      "1575506400000": 0.0200389458,
      "1575506340000": 0.0200383208,
      "1575506280000": 0.0200361917,
      "1575506220000": 0.0200399333,
      "1575506160000": 0.0200346167,
      "1575506100000": 0.0200368822,
      "1575506040000": 0.0200425542,
      "1575505980000": 0.0200441583,
      "1575505920000": 0.0200502,
      "1575505860000": 0.0200519208,
      "1575505800000": 0.02005735,
      "1575505740000": 0.0200579583,
      "1575505680000": 0.0200564,
      "1575505620000": 0.0200545167,
      "1575505560000": 0.0200520941,
      "1575505500000": 0.0200585083,
      "1575505440000": 0.0200651095,
      "1575505380000": 0.0200611195,
      "1575505320000": 0.0200648583,
      "1575505260000": 0.0200669042,
      "1575505200000": 0.0200724583,
      "1575505140000": 0.0200643208,
      "1575505080000": 0.0200580458,
      "1575505020000": 0.020056775,
      "1575504960000": 0.0200517458,
      "1575504900000": 0.0200492458,
      "1575504840000": 0.020058625,
      "1575504780000": 0.0200603625,
      "1575504720000": 0.0200616708,
      "1575504660000": 0.0200620167,
      "1575504600000": 0.0200686042,
      "1575504540000": 0.0200702932,
      "1575504480000": 0.0200703083,
      "1575504420000": 0.0200717,
      "1575504360000": 0.0200785792,
      "1575504300000": 0.0200813333,
      "1575504240000": 0.0200881333,
      "1575504180000": 0.0200915208,
      "1575504120000": 0.0200867625,
      "1575504060000": 0.0200853708,
      "1575504000000": 0.0200737958,
      "1575503940000": 0.0200718333,
      "1575503880000": 0.0200714167,
      "1575503820000": 0.0200704417,
      "1575503760000": 0.020065675,
      "1575503700000": 0.0200610083,
      "1575503640000": 0.0200623458,
      "1575503580000": 0.0200611208,
      "1575503520000": 0.0200585792,
      "1575503460000": 0.0200552167,
      "1575503400000": 0.0200544292,
      "1575503340000": 0.0200504083,
      "1575503280000": 0.0200475167,
      "1575503220000": 0.0200474203,
      "1575503160000": 0.0200486208,
      "1575503100000": 0.0200513992,
      "1575503040000": 0.0200531875,
      "1575502980000": 0.0200520208,
      "1575502920000": 0.0200511917,
      "1575502860000": 0.020049375,
      "1575502800000": 0.0200458792,
      "1575502740000": 0.0200499958,
      "1575502680000": 0.0200508083,
      "1575502620000": 0.0200626458,
      "1575502560000": 0.0200651583,
      "1575502500000": 0.0200686708,
      "1575502440000": 0.0200700083,
      "1575502380000": 0.02006965,
      "1575502320000": 0.0200650958,
      "1575502260000": 0.0200630167,
      "1575502200000": 0.0200580458,
      "1575502140000": 0.0200536333,
      "1575502080000": 0.0200523042,
      "1575502020000": 0.0200514125,
      "1575501960000": 0.0200544083,
      "1575501900000": 0.02005435,
      "1575501840000": 0.0200545958,
      "1575501780000": 0.0200546208,
      "1575501720000": 0.0200541458,
      "1575501660000": 0.0200539125,
      "1575501600000": 0.0200541125,
      "1575501540000": 0.0200534458,
      "1575501480000": 0.02005345,
      "1575501420000": 0.0200557458,
      "1575501360000": 0.0200520458,
      "1575501300000": 0.020046175,
      "1575501240000": 0.0200451458,
      "1575501180000": 0.0200453333,
      "1575501120000": 0.02004355,
      "1575501060000": 0.0200391958,
      "1575501000000": 0.0200343958,
      "1575500940000": 0.0200322083,
      "1575500880000": 0.0200325125,
      "1575500820000": 0.0200331458,
      "1575500760000": 0.0200362167,
      "1575500700000": 0.0200338875,
      "1575500640000": 0.0200305208,
      "1575500580000": 0.0200223542,
      "1575500520000": 0.0200265875,
      "1575500460000": 0.0200331708,
      "1575500400000": 0.0200340333,
      "1575500340000": 0.020037075,
      "1575500280000": 0.0200330167,
      "1575500220000": 0.0200352958,
      "1575500160000": 0.0200378208,
      "1575500100000": 0.0200357958,
      "1575500040000": 0.0200372833,
      "1575499980000": 0.0200368875,
      "1575499920000": 0.0200343458,
      "1575499860000": 0.020030628,
      "1575499800000": 0.0200292458,
      "1575499740000": 0.0200231042,
      "1575499680000": 0.0200208625,
      "1575499620000": 0.0200325875,
      "1575499560000": 0.020035425,
      "1575499500000": 0.0200366708,
      "1575499440000": 0.0200384458,
      "1575499380000": 0.0200383833,
      "1575499320000": 0.0200303917,
      "1575499260000": 0.0200247875,
      "1575499200000": 0.0200295333,
      "1575499140000": 0.0200356958,
      "1575499080000": 0.0200371083,
      "1575499020000": 0.020036725,
      "1575498960000": 0.0200457333,
      "1575498900000": 0.020052975,
      "1575498840000": 0.0200593375,
      "1575498780000": 0.0200615,
      "1575498720000": 0.0200543083,
      "1575498660000": 0.020066825,
      "1575498600000": 0.02007445,
      "1575498540000": 0.0200770125,
      "1575498480000": 0.0200767458,
      "1575498420000": 0.0200816458,
      "1575498360000": 0.0200864667,
      "1575498300000": 0.0200852292,
      "1575498240000": 0.0200873708,
      "1575498180000": 0.02008815,
      "1575498120000": 0.0200908292,
      "1575498060000": 0.0200907708,
      "1575498000000": 0.020095325,
      "1575497940000": 0.0200954417,
      "1575497880000": 0.0200855517,
      "1575497820000": 0.020078425,
      "1575497760000": 0.0200827,
      "1575497700000": 0.0200835167,
      "1575497640000": 0.0200871292,
      "1575497580000": 0.0200849375,
      "1575497520000": 0.0200816042,
      "1575497460000": 0.0200776333,
      "1575497400000": 0.0200624417,
      "1575497340000": 0.0200564042,
      "1575497280000": 0.0200632958,
      "1575497220000": 0.0200646208,
      "1575497160000": 0.0200649375,
      "1575497100000": 0.020062175,
      "1575497040000": 0.0200636708,
      "1575496980000": 0.0200711833,
      "1575496920000": 0.0200750856,
      "1575496860000": 0.020070675,
      "1575496800000": 0.0200656458,
      "1575496740000": 0.0200655917,
      "1575496680000": 0.0200674966,
      "1575496620000": 0.0200649708,
      "1575496560000": 0.0200635417,
      "1575496500000": 0.0200650667,
      "1575496440000": 0.0200653917,
      "1575496380000": 0.0200740292,
      "1575496320000": 0.0200789875,
      "1575496260000": 0.0200945083,
      "1575496200000": 0.0201003333,
      "1575496140000": 0.020088275
    }
  }
}
```

This endpoint retrieves data of a specific index.

### HTTP Request

`GET https://bff.goesoteric.com/public/indices-detailed-breakdown/<index>/<todo>`

### URL Parameters

Parameter | Description
--------- | -----------
index | The index 
todo | todo

### Request Parameters

Parameter | Required | Description
--------- | ----------- | -----------
limit | false | Limit for data size per page
ts | false | From timestamp in milliseconds

## Get Index Chart OHLC

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/indices-charts/ETHBTC/1M?limit=1000&ts=1575465605000'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      [
        1575465540000,
        0.0201525,
        0.02013525,
        0.0201535,
        0.020135
      ],
      [
        1575465480000,
        0.020147,
        0.0201525,
        0.0201525,
        0.0201455
      ],
      [
        1575465420000,
        0.02016475,
        0.020147,
        0.0201645,
        0.020147
      ],
      [
        1575465360000,
        0.020161,
        0.02016475,
        0.020165,
        0.020161
      ],
      [
        1575465300000,
        0.0201675,
        0.020161,
        0.0201675,
        0.020161
      ],
      [
        1575465240000,
        0.02017075,
        0.0201675,
        0.02017075,
        0.02016525
      ],
      [
        1575465180000,
        0.02018025,
        0.02017075,
        0.020182,
        0.02017075
      ],
      [
        1575465120000,
        0.02018775,
        0.02018025,
        0.02018775,
        0.02018025
      ],
      [
        1575465060000,
        0.020189,
        0.02018775,
        0.02019,
        0.020185
      ],
      [
        1575465000000,
        0.020187,
        0.020189,
        0.02018925,
        0.0201845
      ],
      [
        1575464940000,
        0.02019525,
        0.020187,
        0.02019525,
        0.0201855
      ],
      [
        1575464880000,
        0.0202,
        0.02019525,
        0.020203,
        0.020195
      ],
      [
        1575464820000,
        0.02019975,
        0.0202,
        0.0202015,
        0.0201965
      ],
      [
        1575464760000,
        0.02019875,
        0.02019975,
        0.02020175,
        0.0201985
      ],
      [
        1575464700000,
        0.0201955,
        0.02019875,
        0.020199,
        0.02019525
      ],
      [
        1575464640000,
        0.020195,
        0.0201955,
        0.020196,
        0.0201945
      ],
      [
        1575464580000,
        0.020197,
        0.020195,
        0.02019775,
        0.02019325
      ],
      [
        1575464520000,
        0.02018725,
        0.020197,
        0.020197,
        0.020186
      ],
      [
        1575464460000,
        0.02019175,
        0.02018725,
        0.020195,
        0.020184
      ],
      [
        1575464400000,
        0.0201865,
        0.02019175,
        0.02019175,
        0.02018375
      ],
      [
        1575464340000,
        0.02019175,
        0.0201865,
        0.02019225,
        0.020184
      ],
      [
        1575464280000,
        0.02019275,
        0.02019175,
        0.020194,
        0.020191
      ],
      [
        1575464220000,
        0.02019025,
        0.02019275,
        0.02019275,
        0.0201885
      ],
      [
        1575464160000,
        0.0201915,
        0.02019025,
        0.02019175,
        0.020188
      ],
      [
        1575464100000,
        0.020199,
        0.0201915,
        0.020199,
        0.0201915
      ],
      [
        1575464040000,
        0.0202005,
        0.020199,
        0.02020125,
        0.02019725
      ],
      [
        1575463980000,
        0.020201,
        0.0202005,
        0.020201,
        0.02019775
      ],
      [
        1575463920000,
        0.020207,
        0.020201,
        0.020206,
        0.020201
      ],
      [
        1575463860000,
        0.02020875,
        0.020207,
        0.0202085,
        0.0202025
      ],
      [
        1575463800000,
        0.020203,
        0.02020875,
        0.02020925,
        0.02020225
      ],
      [
        1575463740000,
        0.020206,
        0.020203,
        0.02020575,
        0.02020175
      ],
      [
        1575463680000,
        0.02020525,
        0.020206,
        0.020206,
        0.0202035
      ],
      [
        1575463620000,
        0.02020475,
        0.02020525,
        0.0202065,
        0.020202
      ],
      [
        1575463560000,
        0.0202055,
        0.02020475,
        0.02020675,
        0.0202045
      ],
      [
        1575463500000,
        0.02020425,
        0.0202055,
        0.02020725,
        0.020204
      ],
      [
        1575463440000,
        0.02020325,
        0.02020425,
        0.02020425,
        0.0202025
      ],
      [
        1575463380000,
        0.02020425,
        0.02020325,
        0.02020475,
        0.02020325
      ],
      [
        1575463320000,
        0.02020125,
        0.02020425,
        0.02020425,
        0.0202005
      ],
      [
        1575463260000,
        0.02020125,
        0.02020125,
        0.02020225,
        0.0202005
      ],
      [
        1575463200000,
        0.02020725,
        0.02020125,
        0.0202095,
        0.020201
      ],
      [
        1575463140000,
        0.02020075,
        0.02020725,
        0.02020775,
        0.0202
      ],
      [
        1575463080000,
        0.020198,
        0.02020075,
        0.02020275,
        0.02019675
      ],
      [
        1575463020000,
        0.02019925,
        0.020198,
        0.020199,
        0.020196
      ],
      [
        1575462960000,
        0.02019225,
        0.02019925,
        0.02019925,
        0.02019175
      ],
      [
        1575462900000,
        0.02018625,
        0.02019225,
        0.0201935,
        0.02018625
      ],
      [
        1575462840000,
        0.0201825,
        0.02018625,
        0.0201865,
        0.02018175
      ],
      [
        1575462780000,
        0.02018425,
        0.0201825,
        0.020185,
        0.0201825
      ],
      [
        1575462720000,
        0.020184,
        0.02018425,
        0.02018575,
        0.02018325
      ],
      [
        1575462660000,
        0.020186,
        0.020184,
        0.020187,
        0.020184
      ],
      [
        1575462600000,
        0.02018675,
        0.020186,
        0.02018975,
        0.020185
      ],
      [
        1575462540000,
        0.02018175,
        0.02018675,
        0.02018675,
        0.02018175
      ],
      [
        1575462480000,
        0.02018225,
        0.02018175,
        0.02018375,
        0.0201815
      ],
      [
        1575462420000,
        0.02018275,
        0.02018225,
        0.02018475,
        0.020179
      ],
      [
        1575462360000,
        0.02018175,
        0.02018275,
        0.020183,
        0.02018075
      ],
      [
        1575462300000,
        0.02019325,
        0.02018175,
        0.02019325,
        0.02018175
      ],
      [
        1575462240000,
        0.02019625,
        0.02019325,
        0.02019625,
        0.02018875
      ],
      [
        1575462180000,
        0.02018975,
        0.02019625,
        0.02019675,
        0.020189
      ],
      [
        1575462120000,
        0.020187,
        0.02018975,
        0.02018975,
        0.020187
      ],
      [
        1575462060000,
        0.02018675,
        0.020187,
        0.0201915,
        0.0201855
      ],
      [
        1575462000000,
        0.02018975,
        0.02018675,
        0.0201905,
        0.020186
      ],
      [
        1575461940000,
        0.020181,
        0.02018975,
        0.02019,
        0.020179
      ],
      [
        1575461880000,
        0.0201755,
        0.020181,
        0.020181,
        0.020173
      ],
      [
        1575461820000,
        0.020175,
        0.0201755,
        0.02017675,
        0.02017375
      ],
      [
        1575461760000,
        0.02017975,
        0.020175,
        0.02017975,
        0.0201735
      ],
      [
        1575461700000,
        0.02018175,
        0.02017975,
        0.02018175,
        0.02017825
      ],
      [
        1575461640000,
        0.02018175,
        0.02018175,
        0.02018225,
        0.020177
      ],
      [
        1575461580000,
        0.0201815,
        0.02018175,
        0.020182,
        0.02018
      ],
      [
        1575461520000,
        0.02018025,
        0.0201815,
        0.020182,
        0.02018025
      ],
      [
        1575461460000,
        0.02017875,
        0.02018025,
        0.02018175,
        0.02017875
      ],
      [
        1575461400000,
        0.020182,
        0.02017875,
        0.02018525,
        0.02017875
      ],
      [
        1575461340000,
        0.0201805,
        0.020182,
        0.02018275,
        0.020179
      ],
      [
        1575461280000,
        0.020181,
        0.0201805,
        0.020181,
        0.0201795
      ],
      [
        1575461220000,
        0.02018,
        0.020181,
        0.020181,
        0.0201795
      ],
      [
        1575461160000,
        0.0201795,
        0.02018,
        0.02018075,
        0.02017875
      ],
      [
        1575461100000,
        0.02018275,
        0.0201795,
        0.020183,
        0.0201785
      ],
      [
        1575461040000,
        0.02018975,
        0.02018275,
        0.0201895,
        0.02018275
      ],
      [
        1575460980000,
        0.02018925,
        0.02018975,
        0.02019125,
        0.02018825
      ],
      [
        1575460920000,
        0.02019075,
        0.02018925,
        0.02019175,
        0.02018925
      ],
      [
        1575460860000,
        0.02018925,
        0.02019075,
        0.02019125,
        0.020188
      ],
      [
        1575460800000,
        0.02019325,
        0.02018925,
        0.020198,
        0.020189
      ],
      [
        1575460740000,
        0.020194,
        0.02019325,
        0.02019575,
        0.0201905
      ],
      [
        1575460680000,
        0.02019075,
        0.020194,
        0.02019775,
        0.02019025
      ],
      [
        1575460620000,
        0.02019925,
        0.02019075,
        0.02020075,
        0.02019025
      ],
      [
        1575460560000,
        0.020203,
        0.02019925,
        0.0202035,
        0.02019825
      ],
      [
        1575460500000,
        0.020209,
        0.020203,
        0.02021,
        0.02020225
      ],
      [
        1575460440000,
        0.0202005,
        0.020209,
        0.02021025,
        0.02020025
      ],
      [
        1575460380000,
        0.020198,
        0.0202005,
        0.02020375,
        0.02019725
      ],
      [
        1575460320000,
        0.02018825,
        0.020198,
        0.020199,
        0.02018825
      ],
      [
        1575460260000,
        0.02018925,
        0.02018825,
        0.02019025,
        0.020188
      ],
      [
        1575460200000,
        0.020187,
        0.02018925,
        0.0201895,
        0.0201865
      ],
      [
        1575460140000,
        0.020191,
        0.020187,
        0.02019275,
        0.0201855
      ],
      [
        1575460080000,
        0.020196,
        0.020191,
        0.020196,
        0.0201905
      ],
      [
        1575460020000,
        0.02020125,
        0.020196,
        0.02020375,
        0.0201955
      ],
      [
        1575459960000,
        0.020199,
        0.02020125,
        0.020202,
        0.02019775
      ],
      [
        1575459900000,
        0.02019925,
        0.020199,
        0.02020125,
        0.02019775
      ],
      [
        1575459840000,
        0.02020225,
        0.02019925,
        0.020205,
        0.02019775
      ],
      [
        1575459780000,
        0.0202075,
        0.02020225,
        0.02020875,
        0.02020075
      ],
      [
        1575459720000,
        0.0202105,
        0.0202075,
        0.0202115,
        0.020207
      ],
      [
        1575459660000,
        0.020206,
        0.0202105,
        0.0202105,
        0.02020425
      ],
      [
        1575459600000,
        0.020206,
        0.020206,
        0.0202065,
        0.0202045
      ],
      [
        1575459540000,
        0.02020375,
        0.020206,
        0.02020625,
        0.0202025
      ],
      [
        1575459480000,
        0.0202025,
        0.02020375,
        0.0202055,
        0.0202
      ],
      [
        1575459420000,
        0.020198,
        0.0202025,
        0.02020425,
        0.020198
      ],
      [
        1575459360000,
        0.02019825,
        0.020198,
        0.02019825,
        0.0201975
      ],
      [
        1575459300000,
        0.020198,
        0.02019825,
        0.02019975,
        0.02019775
      ],
      [
        1575459240000,
        0.020198,
        0.020198,
        0.02020025,
        0.02019725
      ],
      [
        1575459180000,
        0.02020075,
        0.020198,
        0.02020125,
        0.02019675
      ],
      [
        1575459120000,
        0.02020125,
        0.02020075,
        0.0202025,
        0.0201995
      ],
      [
        1575459060000,
        0.020202,
        0.02020125,
        0.0202015,
        0.020199
      ],
      [
        1575459000000,
        0.02019675,
        0.020202,
        0.0202025,
        0.020196
      ],
      [
        1575458940000,
        0.02020425,
        0.02019675,
        0.0202095,
        0.02019675
      ],
      [
        1575458880000,
        0.02021275,
        0.02020425,
        0.020213,
        0.02020425
      ],
      [
        1575458820000,
        0.02020925,
        0.02021275,
        0.02021275,
        0.02020775
      ],
      [
        1575458760000,
        0.02020975,
        0.02020925,
        0.0202125,
        0.02020775
      ],
      [
        1575458700000,
        0.02020875,
        0.02020975,
        0.02021025,
        0.02020775
      ],
      [
        1575458640000,
        0.0202035,
        0.02020875,
        0.0202095,
        0.02019925
      ],
      [
        1575458580000,
        0.020201,
        0.0202035,
        0.0202035,
        0.020198
      ],
      [
        1575458520000,
        0.020202,
        0.020201,
        0.02020475,
        0.020201
      ],
      [
        1575458460000,
        0.02020025,
        0.020202,
        0.02020325,
        0.0201995
      ],
      [
        1575458400000,
        0.0201995,
        0.02020025,
        0.02020375,
        0.020199
      ],
      [
        1575458340000,
        0.02019725,
        0.0201995,
        0.02020225,
        0.02019725
      ],
      [
        1575458280000,
        0.02019625,
        0.02019725,
        0.02019725,
        0.02019425
      ],
      [
        1575458220000,
        0.02019225,
        0.02019625,
        0.02019625,
        0.02019175
      ],
      [
        1575458160000,
        0.020189,
        0.02019225,
        0.0201945,
        0.020189
      ],
      [
        1575458100000,
        0.02018425,
        0.020189,
        0.02018975,
        0.02018625
      ],
      [
        1575458040000,
        0.0201895,
        0.02018425,
        0.0201895,
        0.02018325
      ],
      [
        1575457980000,
        0.02019125,
        0.0201895,
        0.020192,
        0.0201885
      ],
      [
        1575457920000,
        0.02019225,
        0.02019125,
        0.0201935,
        0.0201885
      ],
      [
        1575457860000,
        0.02019525,
        0.02019225,
        0.020196,
        0.02019125
      ],
      [
        1575457800000,
        0.0201965,
        0.02019525,
        0.0201965,
        0.02019325
      ],
      [
        1575457740000,
        0.02019475,
        0.0201965,
        0.02019875,
        0.02019475
      ],
      [
        1575457680000,
        0.0201975,
        0.02019475,
        0.0201995,
        0.02019425
      ],
      [
        1575457620000,
        0.02020175,
        0.0201975,
        0.0202025,
        0.020197
      ],
      [
        1575457560000,
        0.020204,
        0.02020175,
        0.020204,
        0.02020125
      ],
      [
        1575457500000,
        0.02020275,
        0.020204,
        0.0202095,
        0.02020275
      ],
      [
        1575457440000,
        0.02019825,
        0.02020275,
        0.020212,
        0.02019825
      ],
      [
        1575457380000,
        0.02019525,
        0.02019825,
        0.02020025,
        0.020198
      ],
      [
        1575457320000,
        0.02019075,
        0.02019525,
        0.02020325,
        0.02018925
      ],
      [
        1575457260000,
        0.020189,
        0.02019075,
        0.02019225,
        0.020185
      ],
      [
        1575457200000,
        0.020182,
        0.020189,
        0.020189,
        0.020182
      ],
      [
        1575457140000,
        0.020183,
        0.020182,
        0.0201845,
        0.020182
      ],
      [
        1575457080000,
        0.0201845,
        0.020183,
        0.020185,
        0.02018125
      ],
      [
        1575457020000,
        0.0201705,
        0.0201845,
        0.0201885,
        0.020172
      ],
      [
        1575456960000,
        0.02017225,
        0.0201705,
        0.02017575,
        0.0201705
      ],
      [
        1575456900000,
        0.0201765,
        0.02017225,
        0.02017825,
        0.02017125
      ],
      [
        1575456840000,
        0.020181,
        0.0201765,
        0.020183,
        0.02017625
      ],
      [
        1575456780000,
        0.0201835,
        0.020181,
        0.020184,
        0.020181
      ],
      [
        1575456720000,
        0.02018375,
        0.0201835,
        0.02018425,
        0.02018275
      ],
      [
        1575456660000,
        0.02018375,
        0.02018375,
        0.0201845,
        0.020182
      ],
      [
        1575456600000,
        0.02018125,
        0.02018375,
        0.020185,
        0.02017975
      ],
      [
        1575456540000,
        0.020183,
        0.02018125,
        0.02018475,
        0.02018125
      ],
      [
        1575456480000,
        0.020179,
        0.020183,
        0.020184,
        0.020179
      ],
      [
        1575456420000,
        0.02018075,
        0.020179,
        0.02018125,
        0.02017875
      ],
      [
        1575456360000,
        0.0201775,
        0.02018075,
        0.02018275,
        0.02017675
      ],
      [
        1575456300000,
        0.0201755,
        0.0201775,
        0.02017875,
        0.0201755
      ],
      [
        1575456240000,
        0.02017325,
        0.0201755,
        0.02017675,
        0.02017125
      ],
      [
        1575456180000,
        0.020171,
        0.02017325,
        0.02017325,
        0.02017075
      ],
      [
        1575456120000,
        0.02016975,
        0.020171,
        0.02017275,
        0.020169
      ],
      [
        1575456060000,
        0.02017125,
        0.02016975,
        0.0201725,
        0.02016875
      ],
      [
        1575456000000,
        0.02016625,
        0.02017125,
        0.0201745,
        0.0201665
      ],
      [
        1575455940000,
        0.020167,
        0.02016625,
        0.0201685,
        0.02016575
      ],
      [
        1575455880000,
        0.0201655,
        0.020167,
        0.020167,
        0.02016325
      ],
      [
        1575455820000,
        0.02016875,
        0.0201655,
        0.02016925,
        0.020165
      ],
      [
        1575455760000,
        0.02017425,
        0.02016875,
        0.02017425,
        0.02016825
      ],
      [
        1575455700000,
        0.02017525,
        0.02017425,
        0.02017525,
        0.0201735
      ],
      [
        1575455640000,
        0.02017025,
        0.02017525,
        0.0201755,
        0.02017025
      ],
      [
        1575455580000,
        0.020172,
        0.02017025,
        0.0201755,
        0.02017025
      ],
      [
        1575455520000,
        0.0201685,
        0.020172,
        0.02017575,
        0.0201685
      ],
      [
        1575455460000,
        0.02017525,
        0.0201685,
        0.02017525,
        0.0201685
      ],
      [
        1575455400000,
        0.02016875,
        0.02017525,
        0.020178,
        0.02016875
      ],
      [
        1575455340000,
        0.02017,
        0.02016875,
        0.02017375,
        0.02016875
      ],
      [
        1575455280000,
        0.02017275,
        0.02017,
        0.02017275,
        0.020168
      ],
      [
        1575455220000,
        0.0201745,
        0.02017275,
        0.02017525,
        0.02017025
      ],
      [
        1575455160000,
        0.020177,
        0.0201745,
        0.02017975,
        0.0201725
      ],
      [
        1575455100000,
        0.02018225,
        0.020177,
        0.02018275,
        0.020177
      ],
      [
        1575455040000,
        0.020182,
        0.02018225,
        0.0201835,
        0.020181
      ],
      [
        1575454980000,
        0.02018175,
        0.020182,
        0.02018375,
        0.020181
      ],
      [
        1575454920000,
        0.020183,
        0.02018175,
        0.0201835,
        0.0201805
      ],
      [
        1575454860000,
        0.020185,
        0.020183,
        0.02018625,
        0.020182
      ],
      [
        1575454800000,
        0.0201865,
        0.020185,
        0.0201865,
        0.02018225
      ],
      [
        1575454740000,
        0.02018725,
        0.0201865,
        0.02018875,
        0.02018625
      ],
      [
        1575454680000,
        0.020195,
        0.02018725,
        0.020195,
        0.02018725
      ],
      [
        1575454620000,
        0.020196,
        0.020195,
        0.02019625,
        0.02019325
      ],
      [
        1575454560000,
        0.02019525,
        0.020196,
        0.02019675,
        0.02019475
      ],
      [
        1575454500000,
        0.020195,
        0.02019525,
        0.0201965,
        0.02019475
      ],
      [
        1575454440000,
        0.0201955,
        0.020195,
        0.02019625,
        0.02019375
      ],
      [
        1575454380000,
        0.02019425,
        0.0201955,
        0.02019575,
        0.02019375
      ],
      [
        1575454320000,
        0.0201945,
        0.02019425,
        0.02019575,
        0.0201935
      ],
      [
        1575454260000,
        0.02019425,
        0.0201945,
        0.02019525,
        0.020192
      ],
      [
        1575454200000,
        0.020196,
        0.02019425,
        0.020197,
        0.020194
      ],
      [
        1575454140000,
        0.0201925,
        0.020196,
        0.0201965,
        0.0201925
      ],
      [
        1575454080000,
        0.02019675,
        0.0201925,
        0.02019775,
        0.0201925
      ],
      [
        1575454020000,
        0.02019175,
        0.02019675,
        0.02019675,
        0.02019075
      ],
      [
        1575453960000,
        0.0201875,
        0.02019175,
        0.020193,
        0.02018725
      ],
      [
        1575453900000,
        0.0201875,
        0.0201875,
        0.02018925,
        0.020186
      ],
      [
        1575453840000,
        0.02018975,
        0.0201875,
        0.02018975,
        0.02018325
      ],
      [
        1575453780000,
        0.02019125,
        0.02018975,
        0.020192,
        0.02018925
      ],
      [
        1575453720000,
        0.0201925,
        0.02019125,
        0.020193,
        0.02019025
      ],
      [
        1575453660000,
        0.020193,
        0.0201925,
        0.020194,
        0.02019225
      ],
      [
        1575453600000,
        0.02019225,
        0.020193,
        0.020193,
        0.02019075
      ],
      [
        1575453540000,
        0.020191,
        0.02019225,
        0.020193,
        0.02019075
      ],
      [
        1575453480000,
        0.02019125,
        0.020191,
        0.02019275,
        0.02019
      ],
      [
        1575453420000,
        0.02019,
        0.02019125,
        0.02019275,
        0.02019
      ],
      [
        1575453360000,
        0.02019125,
        0.02019,
        0.020192,
        0.0201875
      ],
      [
        1575453300000,
        0.0201925,
        0.02019125,
        0.020195,
        0.02019075
      ],
      [
        1575453240000,
        0.02019275,
        0.0201925,
        0.020194,
        0.02019125
      ],
      [
        1575453180000,
        0.020189,
        0.02019275,
        0.02019275,
        0.020188
      ],
      [
        1575453120000,
        0.020188,
        0.020189,
        0.02019375,
        0.0201875
      ],
      [
        1575453060000,
        0.02019525,
        0.020188,
        0.02019525,
        0.020188
      ],
      [
        1575453000000,
        0.0201965,
        0.02019525,
        0.02019775,
        0.020194
      ],
      [
        1575452940000,
        0.0201955,
        0.0201965,
        0.0201975,
        0.0201935
      ],
      [
        1575452880000,
        0.020194,
        0.0201955,
        0.02019725,
        0.0201935
      ],
      [
        1575452820000,
        0.0201955,
        0.020194,
        0.02019525,
        0.020193
      ],
      [
        1575452760000,
        0.02019125,
        0.0201955,
        0.02019625,
        0.02018825
      ],
      [
        1575452700000,
        0.02019725,
        0.02019125,
        0.02019825,
        0.02019125
      ],
      [
        1575452640000,
        0.0202,
        0.02019725,
        0.0202025,
        0.020196
      ],
      [
        1575452580000,
        0.02020425,
        0.0202,
        0.02020525,
        0.02019975
      ],
      [
        1575452520000,
        0.02020525,
        0.02020425,
        0.0202055,
        0.0202025
      ],
      [
        1575452460000,
        0.02021,
        0.02020525,
        0.020211,
        0.020205
      ],
      [
        1575452400000,
        0.020213,
        0.02021,
        0.02021525,
        0.02020925
      ],
      [
        1575452340000,
        0.02021525,
        0.020213,
        0.02021525,
        0.02021175
      ],
      [
        1575452280000,
        0.02021975,
        0.02021525,
        0.02021975,
        0.0202135
      ],
      [
        1575452220000,
        0.0202235,
        0.02021975,
        0.020226,
        0.02021925
      ],
      [
        1575452160000,
        0.02022625,
        0.0202235,
        0.020226,
        0.02022325
      ],
      [
        1575452100000,
        0.020231,
        0.02022625,
        0.02023075,
        0.02022525
      ],
      [
        1575452040000,
        0.02022225,
        0.020231,
        0.020231,
        0.02022225
      ],
      [
        1575451980000,
        0.02022275,
        0.02022225,
        0.0202235,
        0.02022075
      ],
      [
        1575451920000,
        0.0202275,
        0.02022275,
        0.0202315,
        0.02022275
      ],
      [
        1575451860000,
        0.02022925,
        0.0202275,
        0.02023025,
        0.02022725
      ],
      [
        1575451800000,
        0.02023025,
        0.02022925,
        0.0202315,
        0.020227
      ],
      [
        1575451740000,
        0.02023575,
        0.02023025,
        0.02023675,
        0.02023025
      ],
      [
        1575451680000,
        0.0202385,
        0.02023575,
        0.02023875,
        0.02023575
      ],
      [
        1575451620000,
        0.02024075,
        0.0202385,
        0.02024075,
        0.02023825
      ],
      [
        1575451560000,
        0.02024025,
        0.02024075,
        0.020244,
        0.02023925
      ],
      [
        1575451500000,
        0.0202365,
        0.02024025,
        0.020242,
        0.0202365
      ],
      [
        1575451440000,
        0.02023875,
        0.0202365,
        0.0202435,
        0.02023575
      ],
      [
        1575451380000,
        0.0202375,
        0.02023875,
        0.02023975,
        0.0202375
      ],
      [
        1575451320000,
        0.020243,
        0.0202375,
        0.020244,
        0.020236
      ],
      [
        1575451260000,
        0.0202455,
        0.020243,
        0.0202455,
        0.020241
      ],
      [
        1575451200000,
        0.02024675,
        0.0202455,
        0.02025025,
        0.02024525
      ],
      [
        1575451140000,
        0.0202465,
        0.02024675,
        0.0202495,
        0.02024525
      ],
      [
        1575451080000,
        0.02023775,
        0.0202465,
        0.02025,
        0.0202375
      ],
      [
        1575451020000,
        0.020235,
        0.02023775,
        0.0202395,
        0.020235
      ],
      [
        1575450960000,
        0.02023425,
        0.020235,
        0.0202365,
        0.0202295
      ],
      [
        1575450900000,
        0.020228,
        0.02023425,
        0.02023425,
        0.02022825
      ],
      [
        1575450840000,
        0.020233,
        0.020228,
        0.020234,
        0.02022575
      ],
      [
        1575450780000,
        0.02023375,
        0.020233,
        0.020234,
        0.02022975
      ],
      [
        1575450720000,
        0.0202325,
        0.02023375,
        0.020236,
        0.02023225
      ],
      [
        1575450660000,
        0.020235,
        0.0202325,
        0.020235,
        0.020232
      ],
      [
        1575450600000,
        0.0202375,
        0.020235,
        0.02023925,
        0.02023375
      ],
      [
        1575450540000,
        0.020224,
        0.0202375,
        0.02024325,
        0.02022425
      ],
      [
        1575450480000,
        0.0202135,
        0.020224,
        0.0202255,
        0.0202135
      ],
      [
        1575450420000,
        0.020212,
        0.0202135,
        0.0202155,
        0.02021175
      ],
      [
        1575450360000,
        0.020217,
        0.020212,
        0.020218,
        0.020212
      ],
      [
        1575450300000,
        0.020213,
        0.020217,
        0.020217,
        0.020212
      ],
      [
        1575450240000,
        0.02021425,
        0.020213,
        0.02021975,
        0.02021225
      ],
      [
        1575450180000,
        0.0202035,
        0.02021425,
        0.020215,
        0.020203
      ],
      [
        1575450120000,
        0.02021025,
        0.0202035,
        0.02021125,
        0.0202025
      ],
      [
        1575450060000,
        0.020206,
        0.02021025,
        0.02021275,
        0.020206
      ],
      [
        1575450000000,
        0.0202,
        0.020206,
        0.02021475,
        0.02019975
      ],
      [
        1575449940000,
        0.0202085,
        0.0202,
        0.0202085,
        0.02019875
      ],
      [
        1575449880000,
        0.0202165,
        0.0202085,
        0.02021925,
        0.020204
      ],
      [
        1575449820000,
        0.0202135,
        0.0202165,
        0.02021725,
        0.02021325
      ],
      [
        1575449760000,
        0.0202105,
        0.0202135,
        0.020218,
        0.0202095
      ],
      [
        1575449700000,
        0.0202125,
        0.0202105,
        0.02021575,
        0.02020225
      ],
      [
        1575449640000,
        0.02020975,
        0.0202125,
        0.0202125,
        0.02020425
      ],
      [
        1575449580000,
        0.02020925,
        0.02020975,
        0.02020975,
        0.02020025
      ],
      [
        1575449520000,
        0.0202305,
        0.02020925,
        0.02023325,
        0.020209
      ],
      [
        1575449460000,
        0.02023975,
        0.0202305,
        0.02023975,
        0.0202305
      ],
      [
        1575449400000,
        0.02024375,
        0.02023975,
        0.02024375,
        0.020236
      ],
      [
        1575449340000,
        0.02023825,
        0.02024375,
        0.02024375,
        0.02023825
      ],
      [
        1575449280000,
        0.0202365,
        0.02023825,
        0.02023975,
        0.02023375
      ],
      [
        1575449220000,
        0.020234,
        0.0202365,
        0.0202365,
        0.02023275
      ],
      [
        1575449160000,
        0.02023525,
        0.020234,
        0.02023875,
        0.020234
      ],
      [
        1575449100000,
        0.02023375,
        0.02023525,
        0.020236,
        0.02022625
      ],
      [
        1575449040000,
        0.02023375,
        0.02023375,
        0.02023575,
        0.02023375
      ],
      [
        1575448980000,
        0.020232,
        0.02023375,
        0.020235,
        0.02023025
      ],
      [
        1575448920000,
        0.02021575,
        0.020232,
        0.02023675,
        0.02021675
      ],
      [
        1575448860000,
        0.0202255,
        0.02021575,
        0.02022625,
        0.0202135
      ],
      [
        1575448800000,
        0.02022675,
        0.0202255,
        0.0202285,
        0.02022475
      ],
      [
        1575448740000,
        0.0202285,
        0.02022675,
        0.02022925,
        0.02022625
      ],
      [
        1575448680000,
        0.02022625,
        0.0202285,
        0.02022975,
        0.0202235
      ],
      [
        1575448620000,
        0.020224,
        0.02022625,
        0.020227,
        0.02022275
      ],
      [
        1575448560000,
        0.020224,
        0.020224,
        0.02022775,
        0.02022225
      ],
      [
        1575448500000,
        0.02021775,
        0.020224,
        0.02022825,
        0.02021825
      ],
      [
        1575448440000,
        0.02021425,
        0.02021775,
        0.02021775,
        0.0202125
      ],
      [
        1575448380000,
        0.02021625,
        0.02021425,
        0.02021925,
        0.02021275
      ],
      [
        1575448320000,
        0.0202125,
        0.02021625,
        0.0202185,
        0.0202125
      ],
      [
        1575448260000,
        0.02021625,
        0.0202125,
        0.0202195,
        0.0202125
      ],
      [
        1575448200000,
        0.020215,
        0.02021625,
        0.0202205,
        0.0202145
      ],
      [
        1575448140000,
        0.0202225,
        0.020215,
        0.0202225,
        0.020215
      ],
      [
        1575448080000,
        0.0202125,
        0.0202225,
        0.020223,
        0.0202125
      ],
      [
        1575448020000,
        0.0202015,
        0.0202125,
        0.0202135,
        0.02020175
      ],
      [
        1575447960000,
        0.0202025,
        0.0202015,
        0.02020425,
        0.02020125
      ],
      [
        1575447900000,
        0.020201,
        0.0202025,
        0.020207,
        0.02020175
      ],
      [
        1575447840000,
        0.02020375,
        0.020201,
        0.020205,
        0.02019625
      ],
      [
        1575447780000,
        0.02019375,
        0.02020375,
        0.02020475,
        0.0201925
      ],
      [
        1575447720000,
        0.02020575,
        0.02019375,
        0.02020925,
        0.02019375
      ],
      [
        1575447660000,
        0.020208,
        0.02020575,
        0.02021,
        0.02020575
      ],
      [
        1575447600000,
        0.0202105,
        0.020208,
        0.0202105,
        0.02020675
      ],
      [
        1575447540000,
        0.0202105,
        0.0202105,
        0.0202115,
        0.02020925
      ],
      [
        1575447480000,
        0.02021325,
        0.0202105,
        0.0202145,
        0.02021025
      ],
      [
        1575447420000,
        0.02021475,
        0.02021325,
        0.020215,
        0.0202115
      ],
      [
        1575447360000,
        0.0202165,
        0.02021475,
        0.0202205,
        0.0202145
      ],
      [
        1575447300000,
        0.02021375,
        0.0202165,
        0.02021825,
        0.02021225
      ],
      [
        1575447240000,
        0.020211,
        0.02021375,
        0.02021925,
        0.02020975
      ],
      [
        1575447180000,
        0.02020425,
        0.020211,
        0.02021525,
        0.0202055
      ],
      [
        1575447120000,
        0.02019875,
        0.02020425,
        0.0202105,
        0.02020075
      ],
      [
        1575447060000,
        0.02018925,
        0.02019875,
        0.020204,
        0.02018825
      ],
      [
        1575447000000,
        0.0201925,
        0.02018925,
        0.02019425,
        0.0201875
      ],
      [
        1575446940000,
        0.02019225,
        0.0201925,
        0.02019475,
        0.02019125
      ],
      [
        1575446880000,
        0.02019075,
        0.02019225,
        0.02019475,
        0.02018925
      ],
      [
        1575446820000,
        0.020193,
        0.02019075,
        0.0201935,
        0.020188
      ],
      [
        1575446760000,
        0.020196,
        0.020193,
        0.02019625,
        0.02019275
      ],
      [
        1575446700000,
        0.0201975,
        0.020196,
        0.02019825,
        0.020194
      ],
      [
        1575446640000,
        0.02019775,
        0.0201975,
        0.02019975,
        0.0201955
      ],
      [
        1575446580000,
        0.02018925,
        0.02019775,
        0.02019825,
        0.020189
      ],
      [
        1575446520000,
        0.0201865,
        0.02018925,
        0.0201895,
        0.0201855
      ],
      [
        1575446460000,
        0.02018875,
        0.0201865,
        0.0201895,
        0.0201855
      ],
      [
        1575446400000,
        0.02018975,
        0.02018875,
        0.0201905,
        0.020188
      ],
      [
        1575446340000,
        0.02018875,
        0.02018975,
        0.02019125,
        0.02018775
      ],
      [
        1575446280000,
        0.02017925,
        0.02018875,
        0.02018875,
        0.02017925
      ],
      [
        1575446220000,
        0.02018325,
        0.02017925,
        0.02018325,
        0.0201785
      ],
      [
        1575446160000,
        0.02018075,
        0.02018325,
        0.0201855,
        0.02018075
      ],
      [
        1575446100000,
        0.02019775,
        0.02018075,
        0.020198,
        0.02018
      ],
      [
        1575446040000,
        0.0202005,
        0.02019775,
        0.02020325,
        0.020196
      ],
      [
        1575445980000,
        0.020211,
        0.0202005,
        0.020211,
        0.02020025
      ],
      [
        1575445920000,
        0.02021175,
        0.020211,
        0.0202125,
        0.02020925
      ],
      [
        1575445860000,
        0.0202105,
        0.02021175,
        0.02021275,
        0.0202105
      ],
      [
        1575445800000,
        0.02021125,
        0.0202105,
        0.02021275,
        0.0202095
      ],
      [
        1575445740000,
        0.0202115,
        0.02021125,
        0.020212,
        0.02020925
      ],
      [
        1575445680000,
        0.0202145,
        0.0202115,
        0.02021675,
        0.0202115
      ],
      [
        1575445620000,
        0.02020975,
        0.0202145,
        0.02021825,
        0.0202085
      ],
      [
        1575445560000,
        0.02020925,
        0.02020975,
        0.02021175,
        0.020208
      ],
      [
        1575445500000,
        0.020212,
        0.02020925,
        0.02021125,
        0.02020875
      ],
      [
        1575445440000,
        0.02021275,
        0.020212,
        0.02021575,
        0.02021125
      ],
      [
        1575445380000,
        0.02021325,
        0.02021275,
        0.02021375,
        0.0202125
      ],
      [
        1575445320000,
        0.0202095,
        0.02021325,
        0.02021575,
        0.02020825
      ],
      [
        1575445260000,
        0.0202085,
        0.0202095,
        0.02021,
        0.02020775
      ],
      [
        1575445200000,
        0.02020925,
        0.0202085,
        0.02021575,
        0.0202085
      ],
      [
        1575445140000,
        0.02020575,
        0.02020925,
        0.0202135,
        0.0202045
      ],
      [
        1575445080000,
        0.02020825,
        0.02020575,
        0.02020925,
        0.02020475
      ],
      [
        1575445020000,
        0.02020275,
        0.02020825,
        0.02020925,
        0.02020075
      ],
      [
        1575444960000,
        0.020207,
        0.02020275,
        0.02020775,
        0.02020275
      ],
      [
        1575444900000,
        0.02020575,
        0.020207,
        0.0202075,
        0.0202055
      ],
      [
        1575444840000,
        0.02019975,
        0.02020575,
        0.020206,
        0.02019975
      ],
      [
        1575444780000,
        0.02019375,
        0.02019975,
        0.02019975,
        0.0201935
      ],
      [
        1575444720000,
        0.02019125,
        0.02019375,
        0.020197,
        0.02019125
      ],
      [
        1575444660000,
        0.02019675,
        0.02019125,
        0.02019775,
        0.02019125
      ],
      [
        1575444600000,
        0.02019425,
        0.02019675,
        0.02019875,
        0.02019325
      ],
      [
        1575444540000,
        0.0201965,
        0.02019425,
        0.02019675,
        0.0201935
      ],
      [
        1575444480000,
        0.020196,
        0.0201965,
        0.020198,
        0.0201945
      ],
      [
        1575444420000,
        0.02019575,
        0.020196,
        0.020196,
        0.02019325
      ],
      [
        1575444360000,
        0.02019375,
        0.02019575,
        0.020196,
        0.02019225
      ],
      [
        1575444300000,
        0.020187,
        0.02019375,
        0.02019775,
        0.0201865
      ],
      [
        1575444240000,
        0.02018775,
        0.020187,
        0.02018775,
        0.020184
      ],
      [
        1575444180000,
        0.0201835,
        0.02018775,
        0.02018775,
        0.0201835
      ],
      [
        1575444120000,
        0.02018375,
        0.0201835,
        0.0201845,
        0.0201805
      ],
      [
        1575444060000,
        0.02018375,
        0.02018375,
        0.02018475,
        0.02018325
      ],
      [
        1575444000000,
        0.02017925,
        0.02018375,
        0.02018425,
        0.020178
      ],
      [
        1575443940000,
        0.02017925,
        0.02017925,
        0.0201805,
        0.02017825
      ],
      [
        1575443880000,
        0.02017625,
        0.02017925,
        0.02018025,
        0.020176
      ],
      [
        1575443820000,
        0.020177,
        0.02017625,
        0.02017925,
        0.02017525
      ],
      [
        1575443760000,
        0.020175,
        0.020177,
        0.020177,
        0.020175
      ],
      [
        1575443700000,
        0.02018,
        0.020175,
        0.020179,
        0.02017375
      ],
      [
        1575443640000,
        0.0201865,
        0.02018,
        0.02018675,
        0.020179
      ],
      [
        1575443580000,
        0.0201905,
        0.0201865,
        0.020191,
        0.0201865
      ],
      [
        1575443520000,
        0.0201905,
        0.0201905,
        0.02019075,
        0.02018875
      ],
      [
        1575443460000,
        0.0201875,
        0.0201905,
        0.0201905,
        0.020186
      ],
      [
        1575443400000,
        0.02018725,
        0.0201875,
        0.02018825,
        0.02018625
      ],
      [
        1575443340000,
        0.02018625,
        0.02018725,
        0.0201875,
        0.02018575
      ],
      [
        1575443280000,
        0.020185,
        0.02018625,
        0.02018775,
        0.0201845
      ],
      [
        1575443220000,
        0.02018525,
        0.020185,
        0.02018675,
        0.0201825
      ],
      [
        1575443160000,
        0.02017675,
        0.02018525,
        0.02018625,
        0.02017625
      ],
      [
        1575443100000,
        0.02017375,
        0.02017675,
        0.02017675,
        0.02017375
      ],
      [
        1575443040000,
        0.020166,
        0.02017375,
        0.02017675,
        0.02016725
      ],
      [
        1575442980000,
        0.020165,
        0.020166,
        0.02016675,
        0.020163
      ],
      [
        1575442920000,
        0.0201655,
        0.020165,
        0.0201675,
        0.0201645
      ],
      [
        1575442860000,
        0.02016425,
        0.0201655,
        0.02016825,
        0.02016325
      ],
      [
        1575442800000,
        0.0201635,
        0.02016425,
        0.0201655,
        0.02016125
      ],
      [
        1575442740000,
        0.0201645,
        0.0201635,
        0.02016525,
        0.020163
      ],
      [
        1575442680000,
        0.02016425,
        0.0201645,
        0.02016625,
        0.020164
      ],
      [
        1575442620000,
        0.020164,
        0.02016425,
        0.0201665,
        0.020162
      ],
      [
        1575442560000,
        0.020163,
        0.020164,
        0.0201665,
        0.020162
      ],
      [
        1575442500000,
        0.02016475,
        0.020163,
        0.02016575,
        0.020161
      ],
      [
        1575442440000,
        0.020164,
        0.02016475,
        0.020166,
        0.02016325
      ],
      [
        1575442380000,
        0.020168,
        0.020164,
        0.0201685,
        0.02016375
      ],
      [
        1575442320000,
        0.02017075,
        0.020168,
        0.020172,
        0.02016675
      ],
      [
        1575442260000,
        0.0201765,
        0.02017075,
        0.0201765,
        0.02017025
      ],
      [
        1575442200000,
        0.0201715,
        0.0201765,
        0.0201775,
        0.0201715
      ],
      [
        1575442140000,
        0.02017,
        0.0201715,
        0.020172,
        0.02016875
      ],
      [
        1575442080000,
        0.02016875,
        0.02017,
        0.0201715,
        0.02016675
      ],
      [
        1575442020000,
        0.02017125,
        0.02016875,
        0.0201735,
        0.02016725
      ],
      [
        1575441960000,
        0.02016775,
        0.02017125,
        0.0201715,
        0.020167
      ],
      [
        1575441900000,
        0.020169,
        0.02016775,
        0.02016975,
        0.0201645
      ],
      [
        1575441840000,
        0.020151,
        0.020169,
        0.02017325,
        0.0201495
      ],
      [
        1575441780000,
        0.020146,
        0.020151,
        0.02015125,
        0.02014575
      ],
      [
        1575441720000,
        0.02014475,
        0.020146,
        0.020147,
        0.020143
      ],
      [
        1575441660000,
        0.0201425,
        0.02014475,
        0.020145,
        0.020141
      ],
      [
        1575441600000,
        0.0201395,
        0.0201425,
        0.02014275,
        0.02013925
      ],
      [
        1575441540000,
        0.02013875,
        0.0201395,
        0.0201405,
        0.02013825
      ],
      [
        1575441480000,
        0.020138,
        0.02013875,
        0.0201395,
        0.0201375
      ],
      [
        1575441420000,
        0.02014025,
        0.020138,
        0.02014075,
        0.020137
      ],
      [
        1575441360000,
        0.02014025,
        0.02014025,
        0.0201405,
        0.020139
      ],
      [
        1575441300000,
        0.020141,
        0.02014025,
        0.02014125,
        0.020138
      ],
      [
        1575441240000,
        0.02014825,
        0.020141,
        0.020149,
        0.020141
      ],
      [
        1575441180000,
        0.0201495,
        0.02014825,
        0.02014975,
        0.02014775
      ],
      [
        1575441120000,
        0.02014525,
        0.0201495,
        0.0201505,
        0.02014525
      ],
      [
        1575441060000,
        0.02014525,
        0.02014525,
        0.02014725,
        0.020145
      ],
      [
        1575441000000,
        0.020149,
        0.02014525,
        0.0201495,
        0.02014525
      ],
      [
        1575440940000,
        0.020148,
        0.020149,
        0.0201495,
        0.02014725
      ],
      [
        1575440880000,
        0.02014675,
        0.020148,
        0.0201495,
        0.0201455
      ],
      [
        1575440820000,
        0.020147,
        0.02014675,
        0.02014775,
        0.02014625
      ],
      [
        1575440760000,
        0.02013925,
        0.020147,
        0.020147,
        0.020138
      ],
      [
        1575440700000,
        0.02013825,
        0.02013925,
        0.0201395,
        0.02013625
      ],
      [
        1575440640000,
        0.02013275,
        0.02013825,
        0.0201385,
        0.02013025
      ],
      [
        1575440580000,
        0.020133,
        0.02013275,
        0.0201365,
        0.02013275
      ],
      [
        1575440520000,
        0.02012925,
        0.020133,
        0.020133,
        0.020129
      ],
      [
        1575440460000,
        0.0201285,
        0.02012925,
        0.0201295,
        0.020127
      ],
      [
        1575440400000,
        0.0201255,
        0.0201285,
        0.02012925,
        0.0201255
      ],
      [
        1575440340000,
        0.02012675,
        0.0201255,
        0.02012775,
        0.02012475
      ],
      [
        1575440280000,
        0.02012975,
        0.02012675,
        0.02013025,
        0.02012675
      ],
      [
        1575440220000,
        0.0201275,
        0.02012975,
        0.02013,
        0.0201275
      ],
      [
        1575440160000,
        0.02013875,
        0.0201275,
        0.02013875,
        0.02012475
      ],
      [
        1575440100000,
        0.0201455,
        0.02013875,
        0.020149,
        0.0201375
      ],
      [
        1575440040000,
        0.0201435,
        0.0201455,
        0.020149,
        0.02014325
      ],
      [
        1575439980000,
        0.0201445,
        0.0201435,
        0.020147,
        0.0201425
      ],
      [
        1575439920000,
        0.0201445,
        0.0201445,
        0.0201455,
        0.02014225
      ],
      [
        1575439860000,
        0.020143,
        0.0201445,
        0.02014525,
        0.020143
      ],
      [
        1575439800000,
        0.02015175,
        0.020143,
        0.02015175,
        0.02014
      ],
      [
        1575439740000,
        0.020151,
        0.02015175,
        0.02015175,
        0.020146
      ],
      [
        1575439680000,
        0.02014775,
        0.020151,
        0.020151,
        0.020147
      ],
      [
        1575439620000,
        0.02014725,
        0.02014775,
        0.02014825,
        0.02014525
      ],
      [
        1575439560000,
        0.020145,
        0.02014725,
        0.020148,
        0.02014475
      ],
      [
        1575439500000,
        0.0201495,
        0.020145,
        0.0201475,
        0.02014425
      ],
      [
        1575439440000,
        0.02014375,
        0.0201495,
        0.0201505,
        0.02014325
      ],
      [
        1575439380000,
        0.02013725,
        0.02014375,
        0.02014375,
        0.02013725
      ],
      [
        1575439320000,
        0.0201315,
        0.02013725,
        0.02014,
        0.02013025
      ],
      [
        1575439260000,
        0.02012925,
        0.0201315,
        0.020134,
        0.02012825
      ],
      [
        1575439200000,
        0.020146,
        0.02012925,
        0.02014725,
        0.02012525
      ],
      [
        1575439140000,
        0.02014725,
        0.020146,
        0.0201475,
        0.020146
      ],
      [
        1575439080000,
        0.02014425,
        0.02014725,
        0.0201485,
        0.02014375
      ],
      [
        1575439020000,
        0.0201445,
        0.02014425,
        0.0201465,
        0.0201425
      ],
      [
        1575438960000,
        0.02014325,
        0.0201445,
        0.0201445,
        0.02014125
      ],
      [
        1575438900000,
        0.0201445,
        0.02014325,
        0.02014775,
        0.020141
      ],
      [
        1575438840000,
        0.02014975,
        0.0201445,
        0.02015,
        0.0201445
      ],
      [
        1575438780000,
        0.02014325,
        0.02014975,
        0.02015,
        0.02014325
      ],
      [
        1575438720000,
        0.02014575,
        0.02014325,
        0.020148,
        0.020143
      ],
      [
        1575438660000,
        0.02014575,
        0.02014575,
        0.020147,
        0.02014525
      ],
      [
        1575438600000,
        0.02015075,
        0.02014575,
        0.0201515,
        0.020145
      ],
      [
        1575438540000,
        0.0201565,
        0.02015075,
        0.0201575,
        0.02015025
      ],
      [
        1575438480000,
        0.0201575,
        0.0201565,
        0.02015725,
        0.020155
      ],
      [
        1575438420000,
        0.0201645,
        0.0201575,
        0.020162,
        0.02015675
      ],
      [
        1575438360000,
        0.0201665,
        0.0201645,
        0.0201675,
        0.020162
      ],
      [
        1575438300000,
        0.02015625,
        0.0201665,
        0.02016675,
        0.02015475
      ],
      [
        1575438240000,
        0.02016,
        0.02015625,
        0.0201625,
        0.0201555
      ],
      [
        1575438180000,
        0.02015575,
        0.02016,
        0.0201605,
        0.02015475
      ],
      [
        1575438120000,
        0.02016325,
        0.02015575,
        0.020163,
        0.0201555
      ],
      [
        1575438060000,
        0.0201625,
        0.02016325,
        0.02016325,
        0.02015675
      ],
      [
        1575438000000,
        0.02016325,
        0.0201625,
        0.020164,
        0.020161
      ],
      [
        1575437940000,
        0.02016675,
        0.02016325,
        0.020167,
        0.02016225
      ],
      [
        1575437880000,
        0.0201705,
        0.02016675,
        0.020171,
        0.02016675
      ],
      [
        1575437820000,
        0.0201675,
        0.0201705,
        0.02017125,
        0.02016725
      ],
      [
        1575437760000,
        0.02016725,
        0.0201675,
        0.02017225,
        0.020167
      ],
      [
        1575437700000,
        0.02016125,
        0.02016725,
        0.02016725,
        0.0201605
      ],
      [
        1575437640000,
        0.02016525,
        0.02016125,
        0.020168,
        0.02016
      ],
      [
        1575437580000,
        0.020172,
        0.02016525,
        0.0201725,
        0.02016525
      ],
      [
        1575437520000,
        0.02017575,
        0.020172,
        0.0201765,
        0.020169
      ],
      [
        1575437460000,
        0.0201755,
        0.02017575,
        0.02017575,
        0.02017225
      ],
      [
        1575437400000,
        0.02017875,
        0.0201755,
        0.02017575,
        0.02017325
      ],
      [
        1575437340000,
        0.02017525,
        0.02017875,
        0.02017975,
        0.02017575
      ],
      [
        1575437280000,
        0.02017425,
        0.02017525,
        0.02017525,
        0.02017075
      ],
      [
        1575437220000,
        0.0201755,
        0.02017425,
        0.0201765,
        0.02017
      ],
      [
        1575437160000,
        0.020175,
        0.0201755,
        0.02017825,
        0.02017375
      ],
      [
        1575437100000,
        0.0201745,
        0.020175,
        0.0201755,
        0.020173
      ],
      [
        1575437040000,
        0.020178,
        0.0201745,
        0.0201785,
        0.02017025
      ],
      [
        1575436980000,
        0.02017875,
        0.020178,
        0.020183,
        0.0201775
      ],
      [
        1575436920000,
        0.02017575,
        0.02017875,
        0.020181,
        0.02017075
      ],
      [
        1575436860000,
        0.02017625,
        0.02017575,
        0.02018025,
        0.0201745
      ],
      [
        1575436800000,
        0.0201755,
        0.02017625,
        0.02017825,
        0.020175
      ],
      [
        1575436740000,
        0.02017375,
        0.0201755,
        0.0201765,
        0.0201695
      ],
      [
        1575436680000,
        0.02018325,
        0.02017375,
        0.02018375,
        0.02017375
      ],
      [
        1575436620000,
        0.02018975,
        0.02018325,
        0.020192,
        0.02018325
      ],
      [
        1575436560000,
        0.0201915,
        0.02018975,
        0.020192,
        0.020189
      ],
      [
        1575436500000,
        0.02018325,
        0.0201915,
        0.02019175,
        0.0201815
      ],
      [
        1575436440000,
        0.02018075,
        0.02018325,
        0.02018325,
        0.0201795
      ],
      [
        1575436380000,
        0.0201835,
        0.02018075,
        0.02018375,
        0.020178
      ],
      [
        1575436320000,
        0.020183,
        0.0201835,
        0.0201855,
        0.020183
      ],
      [
        1575436260000,
        0.02018325,
        0.020183,
        0.020186,
        0.02018225
      ],
      [
        1575436200000,
        0.0201815,
        0.02018325,
        0.0201845,
        0.0201805
      ],
      [
        1575436140000,
        0.02018625,
        0.0201815,
        0.02018775,
        0.0201815
      ],
      [
        1575436080000,
        0.020185,
        0.02018625,
        0.020187,
        0.02018275
      ],
      [
        1575436020000,
        0.02017775,
        0.020185,
        0.020185,
        0.020177
      ],
      [
        1575435960000,
        0.02017475,
        0.02017775,
        0.02017775,
        0.02017425
      ],
      [
        1575435900000,
        0.020175,
        0.02017475,
        0.020176,
        0.020171
      ],
      [
        1575435840000,
        0.020177,
        0.020175,
        0.020177,
        0.02017475
      ],
      [
        1575435780000,
        0.02017525,
        0.020177,
        0.0201775,
        0.02017475
      ],
      [
        1575435720000,
        0.020176,
        0.02017525,
        0.020176,
        0.0201735
      ],
      [
        1575435660000,
        0.02017975,
        0.020176,
        0.020181,
        0.02017525
      ],
      [
        1575435600000,
        0.02018975,
        0.02017975,
        0.02019025,
        0.0201775
      ],
      [
        1575435540000,
        0.02019175,
        0.02018975,
        0.02019225,
        0.02018825
      ],
      [
        1575435480000,
        0.020191,
        0.02019175,
        0.0201935,
        0.020191
      ],
      [
        1575435420000,
        0.02019225,
        0.020191,
        0.02019375,
        0.0201905
      ],
      [
        1575435360000,
        0.02019625,
        0.02019225,
        0.02019625,
        0.02019225
      ],
      [
        1575435300000,
        0.0201945,
        0.02019625,
        0.020198,
        0.0201945
      ],
      [
        1575435240000,
        0.02019425,
        0.0201945,
        0.0201955,
        0.02019325
      ],
      [
        1575435180000,
        0.0201955,
        0.02019425,
        0.020197,
        0.020193
      ],
      [
        1575435120000,
        0.020194,
        0.0201955,
        0.020196,
        0.02019225
      ],
      [
        1575435060000,
        0.020193,
        0.020194,
        0.0201945,
        0.02019225
      ],
      [
        1575435000000,
        0.02019325,
        0.020193,
        0.02019375,
        0.020193
      ],
      [
        1575434940000,
        0.020193,
        0.02019325,
        0.0201935,
        0.020193
      ],
      [
        1575434880000,
        0.02019025,
        0.020193,
        0.02019325,
        0.02018975
      ],
      [
        1575434820000,
        0.02019175,
        0.02019025,
        0.020191,
        0.02018975
      ],
      [
        1575434760000,
        0.02018675,
        0.02019175,
        0.02019225,
        0.02018675
      ],
      [
        1575434700000,
        0.02017975,
        0.02018675,
        0.0201875,
        0.02017975
      ],
      [
        1575434640000,
        0.0201745,
        0.02017975,
        0.02018,
        0.0201745
      ],
      [
        1575434580000,
        0.0201765,
        0.0201745,
        0.02017725,
        0.0201745
      ],
      [
        1575434520000,
        0.020171,
        0.0201765,
        0.02017675,
        0.0201705
      ],
      [
        1575434460000,
        0.020174,
        0.020171,
        0.020174,
        0.020171
      ],
      [
        1575434400000,
        0.0201705,
        0.020174,
        0.02017425,
        0.02016975
      ],
      [
        1575434340000,
        0.02017125,
        0.0201705,
        0.02017225,
        0.02016975
      ],
      [
        1575434280000,
        0.02017025,
        0.02017125,
        0.020173,
        0.02017025
      ],
      [
        1575434220000,
        0.0201725,
        0.02017025,
        0.02017525,
        0.02017
      ],
      [
        1575434160000,
        0.02017475,
        0.0201725,
        0.02017475,
        0.0201725
      ],
      [
        1575434100000,
        0.0201765,
        0.02017475,
        0.02017725,
        0.02017375
      ],
      [
        1575434040000,
        0.02017475,
        0.0201765,
        0.02017725,
        0.02017475
      ],
      [
        1575433980000,
        0.0201745,
        0.02017475,
        0.02017525,
        0.020174
      ],
      [
        1575433920000,
        0.02017625,
        0.0201745,
        0.02017775,
        0.0201745
      ],
      [
        1575433860000,
        0.02017875,
        0.02017625,
        0.020179,
        0.0201735
      ],
      [
        1575433800000,
        0.0201805,
        0.02017875,
        0.0201805,
        0.02017825
      ],
      [
        1575433740000,
        0.02018,
        0.0201805,
        0.02018125,
        0.02018
      ],
      [
        1575433680000,
        0.02018275,
        0.02018,
        0.0201835,
        0.02017925
      ],
      [
        1575433620000,
        0.02018725,
        0.02018275,
        0.02018775,
        0.020182
      ],
      [
        1575433560000,
        0.020182,
        0.02018725,
        0.02018825,
        0.020181
      ],
      [
        1575433500000,
        0.02018325,
        0.020182,
        0.02018475,
        0.020182
      ],
      [
        1575433440000,
        0.02018425,
        0.02018325,
        0.02018875,
        0.02018175
      ],
      [
        1575433380000,
        0.02017525,
        0.02018425,
        0.02018725,
        0.02017525
      ],
      [
        1575433320000,
        0.02017475,
        0.02017525,
        0.02017725,
        0.02016925
      ],
      [
        1575433260000,
        0.02017725,
        0.02017475,
        0.0201765,
        0.02017175
      ],
      [
        1575433200000,
        0.020179,
        0.02017725,
        0.0201805,
        0.02017725
      ],
      [
        1575433140000,
        0.020178,
        0.020179,
        0.02017975,
        0.02017625
      ],
      [
        1575433080000,
        0.020181,
        0.020178,
        0.020182,
        0.02017625
      ],
      [
        1575433020000,
        0.02018425,
        0.020181,
        0.02018475,
        0.020181
      ],
      [
        1575432960000,
        0.02018525,
        0.02018425,
        0.0201855,
        0.02018125
      ],
      [
        1575432900000,
        0.020186,
        0.02018525,
        0.0201875,
        0.02018525
      ],
      [
        1575432840000,
        0.0201865,
        0.020186,
        0.020189,
        0.020186
      ],
      [
        1575432780000,
        0.02019,
        0.0201865,
        0.0201905,
        0.02018325
      ],
      [
        1575432720000,
        0.02018725,
        0.02019,
        0.020191,
        0.020187
      ],
      [
        1575432660000,
        0.02018975,
        0.02018725,
        0.02019175,
        0.02018725
      ],
      [
        1575432600000,
        0.02018575,
        0.02018975,
        0.02019075,
        0.020185
      ],
      [
        1575432540000,
        0.0201935,
        0.02018575,
        0.02019325,
        0.02018575
      ],
      [
        1575432480000,
        0.0201925,
        0.0201935,
        0.0201935,
        0.02018925
      ],
      [
        1575432420000,
        0.020193,
        0.0201925,
        0.0201965,
        0.020192
      ],
      [
        1575432360000,
        0.0201955,
        0.020193,
        0.02019725,
        0.0201925
      ],
      [
        1575432300000,
        0.020194,
        0.0201955,
        0.02019675,
        0.02019325
      ],
      [
        1575432240000,
        0.02020025,
        0.020194,
        0.0202005,
        0.02019225
      ],
      [
        1575432180000,
        0.0202015,
        0.02020025,
        0.02020325,
        0.02019875
      ],
      [
        1575432120000,
        0.0201955,
        0.0202015,
        0.0202015,
        0.0201955
      ],
      [
        1575432060000,
        0.020197,
        0.0201955,
        0.02020075,
        0.02019025
      ],
      [
        1575432000000,
        0.0201975,
        0.020197,
        0.0201985,
        0.02019475
      ],
      [
        1575431940000,
        0.0201995,
        0.0201975,
        0.0202005,
        0.020197
      ],
      [
        1575431880000,
        0.0202025,
        0.0201995,
        0.0202045,
        0.020198
      ],
      [
        1575431820000,
        0.02020125,
        0.0202025,
        0.02020475,
        0.02020025
      ],
      [
        1575431760000,
        0.0202,
        0.02020125,
        0.02020125,
        0.0201995
      ],
      [
        1575431700000,
        0.0202005,
        0.0202,
        0.020203,
        0.02019975
      ],
      [
        1575431640000,
        0.020204,
        0.0202005,
        0.020204,
        0.0201995
      ],
      [
        1575431580000,
        0.0202045,
        0.020204,
        0.02020525,
        0.02020225
      ],
      [
        1575431520000,
        0.02019825,
        0.0202045,
        0.0202045,
        0.020198
      ],
      [
        1575431460000,
        0.020201,
        0.02019825,
        0.02020175,
        0.0201975
      ],
      [
        1575431400000,
        0.0202005,
        0.020201,
        0.020202,
        0.02020025
      ],
      [
        1575431340000,
        0.020201,
        0.0202005,
        0.02020125,
        0.0201975
      ],
      [
        1575431280000,
        0.02020275,
        0.020201,
        0.020204,
        0.0202
      ],
      [
        1575431220000,
        0.02020325,
        0.02020275,
        0.020205,
        0.020202
      ],
      [
        1575431160000,
        0.0202,
        0.02020325,
        0.02020475,
        0.02019825
      ],
      [
        1575431100000,
        0.02019875,
        0.0202,
        0.02020075,
        0.02019725
      ],
      [
        1575431040000,
        0.02020125,
        0.02019875,
        0.0202015,
        0.0201975
      ],
      [
        1575430980000,
        0.020206,
        0.02020125,
        0.0202065,
        0.0202
      ],
      [
        1575430920000,
        0.0202045,
        0.020206,
        0.02020625,
        0.02020275
      ],
      [
        1575430860000,
        0.02020325,
        0.0202045,
        0.0202055,
        0.0202
      ],
      [
        1575430800000,
        0.02020375,
        0.02020325,
        0.020204,
        0.0202025
      ],
      [
        1575430740000,
        0.02019875,
        0.02020375,
        0.020204,
        0.02019675
      ],
      [
        1575430680000,
        0.020192,
        0.02019875,
        0.020199,
        0.02019175
      ],
      [
        1575430620000,
        0.0201965,
        0.020192,
        0.0201965,
        0.0201915
      ],
      [
        1575430560000,
        0.020194,
        0.0201965,
        0.0201965,
        0.02019325
      ],
      [
        1575430500000,
        0.0201995,
        0.020194,
        0.0202,
        0.0201935
      ],
      [
        1575430440000,
        0.020196,
        0.0201995,
        0.0201995,
        0.020196
      ],
      [
        1575430380000,
        0.0201975,
        0.020196,
        0.02019925,
        0.0201945
      ],
      [
        1575430320000,
        0.020196,
        0.0201975,
        0.0201975,
        0.0201965
      ],
      [
        1575430260000,
        0.0201945,
        0.020196,
        0.020196,
        0.020193
      ],
      [
        1575430200000,
        0.0201945,
        0.0201945,
        0.02019625,
        0.0201925
      ],
      [
        1575430140000,
        0.020194,
        0.0201945,
        0.0201965,
        0.020193
      ],
      [
        1575430080000,
        0.020196,
        0.020194,
        0.020196,
        0.020194
      ],
      [
        1575430020000,
        0.02019375,
        0.020196,
        0.0201965,
        0.02019275
      ],
      [
        1575429960000,
        0.020194,
        0.02019375,
        0.02019575,
        0.02019275
      ],
      [
        1575429900000,
        0.02019475,
        0.020194,
        0.02019525,
        0.020194
      ],
      [
        1575429840000,
        0.0201925,
        0.02019475,
        0.02019475,
        0.020191
      ],
      [
        1575429780000,
        0.0201895,
        0.0201925,
        0.0201935,
        0.020189
      ],
      [
        1575429720000,
        0.02019425,
        0.0201895,
        0.02019425,
        0.020188
      ],
      [
        1575429660000,
        0.02019475,
        0.02019425,
        0.02019575,
        0.020193
      ],
      [
        1575429600000,
        0.0201995,
        0.02019475,
        0.02019975,
        0.02019375
      ],
      [
        1575429540000,
        0.0201895,
        0.0201995,
        0.02019975,
        0.020189
      ],
      [
        1575429480000,
        0.02019475,
        0.0201895,
        0.0201965,
        0.02018875
      ],
      [
        1575429420000,
        0.02019575,
        0.02019475,
        0.02019625,
        0.0201935
      ],
      [
        1575429360000,
        0.020195,
        0.02019575,
        0.02019725,
        0.02019175
      ],
      [
        1575429300000,
        0.0201915,
        0.020195,
        0.020196,
        0.02019175
      ],
      [
        1575429240000,
        0.02019175,
        0.0201915,
        0.020194,
        0.02018825
      ],
      [
        1575429180000,
        0.02019325,
        0.02019175,
        0.02019375,
        0.02019075
      ],
      [
        1575429120000,
        0.02019625,
        0.02019325,
        0.02019625,
        0.02019225
      ],
      [
        1575429060000,
        0.02019675,
        0.02019625,
        0.020197,
        0.02019625
      ],
      [
        1575429000000,
        0.02019475,
        0.02019675,
        0.020197,
        0.02019425
      ],
      [
        1575428940000,
        0.02019725,
        0.02019475,
        0.02019825,
        0.02019475
      ],
      [
        1575428880000,
        0.020198,
        0.02019725,
        0.0201995,
        0.0201965
      ],
      [
        1575428820000,
        0.02019625,
        0.020198,
        0.02019825,
        0.02019425
      ],
      [
        1575428760000,
        0.02019075,
        0.02019625,
        0.020197,
        0.02019075
      ],
      [
        1575428700000,
        0.02019825,
        0.02019075,
        0.020198,
        0.0201905
      ],
      [
        1575428640000,
        0.02019825,
        0.02019825,
        0.02019825,
        0.02019575
      ],
      [
        1575428580000,
        0.0201965,
        0.02019825,
        0.02019925,
        0.02019625
      ],
      [
        1575428520000,
        0.02019575,
        0.0201965,
        0.02019875,
        0.020194
      ],
      [
        1575428460000,
        0.020193,
        0.02019575,
        0.02020525,
        0.020193
      ],
      [
        1575428400000,
        0.0201925,
        0.020193,
        0.0201945,
        0.02019175
      ],
      [
        1575428340000,
        0.02019225,
        0.0201925,
        0.020193,
        0.02019075
      ],
      [
        1575428280000,
        0.02018925,
        0.02019225,
        0.020193,
        0.02018925
      ],
      [
        1575428220000,
        0.02018475,
        0.02018925,
        0.02019275,
        0.0201845
      ],
      [
        1575428160000,
        0.02018525,
        0.02018475,
        0.02018625,
        0.0201845
      ],
      [
        1575428100000,
        0.02018725,
        0.02018525,
        0.02018825,
        0.0201845
      ],
      [
        1575428040000,
        0.020191,
        0.02018725,
        0.0201915,
        0.02018725
      ],
      [
        1575427980000,
        0.02019275,
        0.020191,
        0.0201945,
        0.02019075
      ],
      [
        1575427920000,
        0.0201935,
        0.02019275,
        0.020195,
        0.02019275
      ],
      [
        1575427860000,
        0.02019425,
        0.0201935,
        0.020197,
        0.0201935
      ],
      [
        1575427800000,
        0.02019675,
        0.02019425,
        0.02019725,
        0.020194
      ],
      [
        1575427740000,
        0.02019625,
        0.02019675,
        0.020198,
        0.0201955
      ],
      [
        1575427680000,
        0.0202,
        0.02019625,
        0.0202,
        0.02019575
      ],
      [
        1575427620000,
        0.020201,
        0.0202,
        0.02020175,
        0.02019925
      ],
      [
        1575427560000,
        0.02020725,
        0.020201,
        0.02020725,
        0.02019925
      ],
      [
        1575427500000,
        0.02020625,
        0.02020725,
        0.02020925,
        0.0202055
      ],
      [
        1575427440000,
        0.02020675,
        0.02020625,
        0.02020825,
        0.0202055
      ],
      [
        1575427380000,
        0.0202095,
        0.02020675,
        0.0202085,
        0.02020525
      ],
      [
        1575427320000,
        0.02020925,
        0.0202095,
        0.02020975,
        0.020206
      ],
      [
        1575427260000,
        0.020211,
        0.02020925,
        0.020211,
        0.0202085
      ],
      [
        1575427200000,
        0.02020725,
        0.020211,
        0.020211,
        0.020204
      ],
      [
        1575427140000,
        0.02020725,
        0.02020725,
        0.02020925,
        0.02020625
      ],
      [
        1575427080000,
        0.02020225,
        0.02020725,
        0.02020725,
        0.020201
      ],
      [
        1575427020000,
        0.02020675,
        0.02020225,
        0.02020675,
        0.02020075
      ],
      [
        1575426960000,
        0.02020625,
        0.02020675,
        0.02020875,
        0.02020525
      ],
      [
        1575426900000,
        0.02021025,
        0.02020625,
        0.020211,
        0.02020625
      ],
      [
        1575426840000,
        0.0202085,
        0.02021025,
        0.02021175,
        0.020207
      ],
      [
        1575426780000,
        0.02020775,
        0.0202085,
        0.0202085,
        0.020206
      ],
      [
        1575426720000,
        0.02021225,
        0.02020775,
        0.020214,
        0.020207
      ],
      [
        1575426660000,
        0.02021275,
        0.02021225,
        0.02021375,
        0.02021125
      ],
      [
        1575426600000,
        0.02021325,
        0.02021275,
        0.02021475,
        0.0202125
      ],
      [
        1575426540000,
        0.02021525,
        0.02021325,
        0.02021675,
        0.02021125
      ],
      [
        1575426480000,
        0.020219,
        0.02021525,
        0.02021975,
        0.02021275
      ],
      [
        1575426420000,
        0.02021825,
        0.020219,
        0.02022175,
        0.02021675
      ],
      [
        1575426360000,
        0.02021925,
        0.02021825,
        0.02022075,
        0.0202165
      ],
      [
        1575426300000,
        0.020202,
        0.02021925,
        0.02021925,
        0.02020325
      ],
      [
        1575426240000,
        0.02019025,
        0.020202,
        0.020202,
        0.02018825
      ],
      [
        1575426180000,
        0.0201945,
        0.02019025,
        0.02019475,
        0.02019025
      ],
      [
        1575426120000,
        0.02019225,
        0.0201945,
        0.02019575,
        0.02018975
      ],
      [
        1575426060000,
        0.020189,
        0.02019225,
        0.0201935,
        0.020187
      ],
      [
        1575426000000,
        0.02019525,
        0.020189,
        0.0201955,
        0.0201885
      ],
      [
        1575425940000,
        0.020196,
        0.02019525,
        0.0201965,
        0.02019075
      ],
      [
        1575425880000,
        0.02020075,
        0.020196,
        0.02020075,
        0.02019425
      ],
      [
        1575425820000,
        0.02020125,
        0.02020075,
        0.0202025,
        0.0201985
      ],
      [
        1575425760000,
        0.0202025,
        0.02020125,
        0.02020375,
        0.02020125
      ],
      [
        1575425700000,
        0.02020125,
        0.0202025,
        0.0202025,
        0.0202
      ],
      [
        1575425640000,
        0.0202015,
        0.02020125,
        0.020203,
        0.0202
      ],
      [
        1575425580000,
        0.020202,
        0.0202015,
        0.02020225,
        0.02020075
      ],
      [
        1575425520000,
        0.020207,
        0.020202,
        0.02020775,
        0.02020025
      ],
      [
        1575425460000,
        0.0202115,
        0.020207,
        0.0202135,
        0.02020675
      ],
      [
        1575425400000,
        0.02021275,
        0.0202115,
        0.02021325,
        0.02020975
      ],
      [
        1575425340000,
        0.0202035,
        0.02021275,
        0.02021325,
        0.0202035
      ],
      [
        1575425280000,
        0.020202,
        0.0202035,
        0.0202035,
        0.0201935
      ],
      [
        1575425220000,
        0.02019775,
        0.020202,
        0.02020275,
        0.0201975
      ],
      [
        1575425160000,
        0.0201945,
        0.02019775,
        0.02019875,
        0.02019325
      ],
      [
        1575425100000,
        0.02018675,
        0.0201945,
        0.0201945,
        0.02018725
      ],
      [
        1575425040000,
        0.0201885,
        0.02018675,
        0.0201905,
        0.02018425
      ],
      [
        1575424980000,
        0.02018775,
        0.0201885,
        0.02019,
        0.02018725
      ],
      [
        1575424920000,
        0.0201865,
        0.02018775,
        0.02019075,
        0.0201875
      ],
      [
        1575424860000,
        0.02019275,
        0.0201865,
        0.020196,
        0.0201865
      ],
      [
        1575424800000,
        0.020193,
        0.02019275,
        0.02019375,
        0.02019175
      ],
      [
        1575424740000,
        0.0202015,
        0.020193,
        0.0202015,
        0.020192
      ],
      [
        1575424680000,
        0.02019475,
        0.0202015,
        0.02020225,
        0.02019125
      ],
      [
        1575424620000,
        0.0202,
        0.02019475,
        0.02020075,
        0.02019475
      ],
      [
        1575424560000,
        0.02019125,
        0.0202,
        0.02020075,
        0.0201895
      ],
      [
        1575424500000,
        0.02019575,
        0.02019125,
        0.0201975,
        0.02019
      ],
      [
        1575424440000,
        0.020182,
        0.02019575,
        0.02019825,
        0.020182
      ],
      [
        1575424380000,
        0.020186,
        0.020182,
        0.02018625,
        0.020181
      ],
      [
        1575424320000,
        0.02018825,
        0.020186,
        0.02019075,
        0.020185
      ],
      [
        1575424260000,
        0.020189,
        0.02018825,
        0.02018925,
        0.02018525
      ],
      [
        1575424200000,
        0.02018675,
        0.020189,
        0.02019475,
        0.02018675
      ],
      [
        1575424140000,
        0.02017875,
        0.02018675,
        0.02018675,
        0.020178
      ],
      [
        1575424080000,
        0.02016875,
        0.02017875,
        0.02017875,
        0.020168
      ],
      [
        1575424020000,
        0.0201675,
        0.02016875,
        0.02016875,
        0.02016675
      ],
      [
        1575423960000,
        0.02016675,
        0.0201675,
        0.0201675,
        0.02016625
      ],
      [
        1575423900000,
        0.02016775,
        0.02016675,
        0.02016875,
        0.0201665
      ],
      [
        1575423840000,
        0.020168,
        0.02016775,
        0.0201705,
        0.0201665
      ],
      [
        1575423780000,
        0.020169,
        0.020168,
        0.0201695,
        0.02016775
      ],
      [
        1575423720000,
        0.02016975,
        0.020169,
        0.02017025,
        0.02016775
      ],
      [
        1575423660000,
        0.02016975,
        0.02016975,
        0.02017225,
        0.020169
      ],
      [
        1575423600000,
        0.02017175,
        0.02016975,
        0.020173,
        0.02016575
      ],
      [
        1575423540000,
        0.0201705,
        0.02017175,
        0.0201735,
        0.02017
      ],
      [
        1575423480000,
        0.02017225,
        0.0201705,
        0.0201745,
        0.0201705
      ],
      [
        1575423420000,
        0.02017175,
        0.02017225,
        0.020174,
        0.02016675
      ],
      [
        1575423360000,
        0.0201635,
        0.02017175,
        0.02017175,
        0.02016375
      ],
      [
        1575423300000,
        0.02015925,
        0.0201635,
        0.0201635,
        0.020159
      ],
      [
        1575423240000,
        0.02015875,
        0.02015925,
        0.02016,
        0.020158
      ],
      [
        1575423180000,
        0.02015925,
        0.02015875,
        0.020161,
        0.020157
      ],
      [
        1575423120000,
        0.02015825,
        0.02015925,
        0.02016075,
        0.02015775
      ],
      [
        1575423060000,
        0.02016875,
        0.02015825,
        0.02016675,
        0.020158
      ],
      [
        1575423000000,
        0.02016,
        0.02016875,
        0.020169,
        0.020158
      ],
      [
        1575422940000,
        0.0201625,
        0.02016,
        0.0201635,
        0.02015875
      ],
      [
        1575422880000,
        0.02016875,
        0.0201625,
        0.02016875,
        0.02016175
      ],
      [
        1575422820000,
        0.020166,
        0.02016875,
        0.0201725,
        0.0201645
      ],
      [
        1575422760000,
        0.02017325,
        0.020166,
        0.020175,
        0.02016475
      ],
      [
        1575422700000,
        0.0201705,
        0.02017325,
        0.02017525,
        0.02016925
      ],
      [
        1575422640000,
        0.0201645,
        0.0201705,
        0.0201705,
        0.02016425
      ],
      [
        1575422580000,
        0.02016675,
        0.0201645,
        0.0201685,
        0.0201645
      ],
      [
        1575422520000,
        0.0201605,
        0.02016675,
        0.02016675,
        0.0201585
      ],
      [
        1575422460000,
        0.0201625,
        0.0201605,
        0.02017375,
        0.0201605
      ],
      [
        1575422400000,
        0.020153,
        0.0201625,
        0.0201625,
        0.020151
      ],
      [
        1575422340000,
        0.020154,
        0.020153,
        0.02015525,
        0.0201475
      ],
      [
        1575422280000,
        0.0201595,
        0.020154,
        0.02016225,
        0.02015375
      ],
      [
        1575422220000,
        0.020167,
        0.0201595,
        0.02016975,
        0.020159
      ],
      [
        1575422160000,
        0.02016375,
        0.020167,
        0.02016925,
        0.0201635
      ],
      [
        1575422100000,
        0.02016825,
        0.02016375,
        0.02016825,
        0.02016275
      ],
      [
        1575422040000,
        0.02017375,
        0.02016825,
        0.02017375,
        0.020167
      ],
      [
        1575421980000,
        0.020158,
        0.02017375,
        0.02017675,
        0.020158
      ],
      [
        1575421920000,
        0.02016275,
        0.020158,
        0.020164,
        0.0201515
      ],
      [
        1575421860000,
        0.0201535,
        0.02016275,
        0.02016425,
        0.0201535
      ],
      [
        1575421800000,
        0.02015825,
        0.0201535,
        0.02015925,
        0.0201495
      ],
      [
        1575421740000,
        0.02015375,
        0.02015825,
        0.02015925,
        0.0201505
      ],
      [
        1575421680000,
        0.0201575,
        0.02015375,
        0.020161,
        0.02015275
      ],
      [
        1575421620000,
        0.0201645,
        0.0201575,
        0.02016525,
        0.0201535
      ],
      [
        1575421560000,
        0.0201675,
        0.0201645,
        0.0201755,
        0.020162
      ],
      [
        1575421500000,
        0.02016675,
        0.0201675,
        0.0201695,
        0.0201645
      ],
      [
        1575421440000,
        0.02016225,
        0.02016675,
        0.02016725,
        0.02015525
      ],
      [
        1575421380000,
        0.02017475,
        0.02016225,
        0.02017625,
        0.02016225
      ],
      [
        1575421320000,
        0.02014975,
        0.02017475,
        0.0201785,
        0.020144
      ],
      [
        1575421260000,
        0.02019425,
        0.02014975,
        0.02019425,
        0.02014325
      ],
      [
        1575421200000,
        0.0202065,
        0.02019425,
        0.020208,
        0.02019425
      ],
      [
        1575421140000,
        0.02020925,
        0.0202065,
        0.02020975,
        0.0202055
      ],
      [
        1575421080000,
        0.02020825,
        0.02020925,
        0.02021175,
        0.02020425
      ],
      [
        1575421020000,
        0.0201985,
        0.02020825,
        0.02020875,
        0.020198
      ],
      [
        1575420960000,
        0.02019875,
        0.0201985,
        0.02019875,
        0.02019675
      ],
      [
        1575420900000,
        0.02019825,
        0.02019875,
        0.02019925,
        0.02019125
      ],
      [
        1575420840000,
        0.02019875,
        0.02019825,
        0.02020275,
        0.02019775
      ],
      [
        1575420780000,
        0.0201995,
        0.02019875,
        0.02020025,
        0.020196
      ],
      [
        1575420720000,
        0.020195,
        0.0201995,
        0.0201995,
        0.0201915
      ],
      [
        1575420660000,
        0.02019375,
        0.020195,
        0.020199,
        0.02019325
      ],
      [
        1575420600000,
        0.02019325,
        0.02019375,
        0.02019875,
        0.02018875
      ],
      [
        1575420540000,
        0.020187,
        0.02019325,
        0.0201945,
        0.02018475
      ],
      [
        1575420480000,
        0.02018225,
        0.020187,
        0.0201905,
        0.02018275
      ],
      [
        1575420420000,
        0.02018125,
        0.02018225,
        0.02018325,
        0.0201795
      ],
      [
        1575420360000,
        0.02018225,
        0.02018125,
        0.02018225,
        0.020175
      ],
      [
        1575420300000,
        0.020177,
        0.02018225,
        0.02018375,
        0.0201715
      ],
      [
        1575420240000,
        0.02017325,
        0.020177,
        0.020177,
        0.02016725
      ],
      [
        1575420180000,
        0.0201705,
        0.02017325,
        0.0201745,
        0.02017075
      ],
      [
        1575420120000,
        0.02014775,
        0.0201705,
        0.020172,
        0.020149
      ],
      [
        1575420060000,
        0.02014475,
        0.02014775,
        0.02015175,
        0.0201405
      ],
      [
        1575420000000,
        0.0201535,
        0.02014475,
        0.0201575,
        0.0201435
      ],
      [
        1575419940000,
        0.02015025,
        0.0201535,
        0.0201615,
        0.02014425
      ],
      [
        1575419880000,
        0.0201495,
        0.02015025,
        0.02015025,
        0.0201395
      ],
      [
        1575419820000,
        0.02010515,
        0.0201495,
        0.020154,
        0.020099
      ],
      [
        1575419760000,
        0.02012435,
        0.02010515,
        0.0201301,
        0.0200921
      ],
      [
        1575419700000,
        0.0201411,
        0.02012435,
        0.02014235,
        0.0201216
      ],
      [
        1575419640000,
        0.02014385,
        0.0201411,
        0.0201456,
        0.0201371
      ],
      [
        1575419580000,
        0.02014485,
        0.02014385,
        0.02014735,
        0.02014135
      ],
      [
        1575419520000,
        0.02015535,
        0.02014485,
        0.02015535,
        0.02014435
      ],
      [
        1575419460000,
        0.02015485,
        0.02015535,
        0.02016435,
        0.0201531
      ],
      [
        1575419400000,
        0.02016085,
        0.02015485,
        0.0201621,
        0.0201496
      ],
      [
        1575419340000,
        0.0201576,
        0.02016085,
        0.0201671,
        0.0201451
      ],
      [
        1575419280000,
        0.0201361,
        0.0201576,
        0.02016285,
        0.02013385
      ],
      [
        1575419220000,
        0.02014485,
        0.0201361,
        0.02014585,
        0.0201326
      ],
      [
        1575419160000,
        0.02015485,
        0.02014485,
        0.0201566,
        0.0201446
      ],
      [
        1575419100000,
        0.02015885,
        0.02015485,
        0.0201601,
        0.02014985
      ],
      [
        1575419040000,
        0.02015735,
        0.02015885,
        0.0201621,
        0.0201586
      ],
      [
        1575418980000,
        0.0201636,
        0.02015735,
        0.0201636,
        0.0201561
      ],
      [
        1575418920000,
        0.02016635,
        0.0201636,
        0.0201676,
        0.02016135
      ],
      [
        1575418860000,
        0.0201681,
        0.02016635,
        0.0201681,
        0.0201636
      ],
      [
        1575418800000,
        0.0201681,
        0.0201681,
        0.0201691,
        0.0201661
      ],
      [
        1575418740000,
        0.02016635,
        0.0201681,
        0.0201686,
        0.02016585
      ],
      [
        1575418680000,
        0.0201521,
        0.02016635,
        0.0201666,
        0.0201521
      ],
      [
        1575418620000,
        0.02013935,
        0.0201521,
        0.0201526,
        0.02013935
      ],
      [
        1575418560000,
        0.02014135,
        0.02013935,
        0.0201461,
        0.0201386
      ],
      [
        1575418500000,
        0.0201496,
        0.02014135,
        0.0201501,
        0.0201411
      ],
      [
        1575418440000,
        0.02014385,
        0.0201496,
        0.02014985,
        0.02014485
      ],
      [
        1575418380000,
        0.02014635,
        0.02014385,
        0.02014635,
        0.02014335
      ],
      [
        1575418320000,
        0.02014635,
        0.02014635,
        0.0201471,
        0.0201431
      ],
      [
        1575418260000,
        0.02013935,
        0.02014635,
        0.02014785,
        0.0201396
      ],
      [
        1575418200000,
        0.0201486,
        0.02013935,
        0.02015235,
        0.0201351
      ],
      [
        1575418140000,
        0.02015285,
        0.0201486,
        0.02015285,
        0.0201486
      ],
      [
        1575418080000,
        0.02015885,
        0.02015285,
        0.02015985,
        0.0201521
      ],
      [
        1575418020000,
        0.02016635,
        0.02015885,
        0.02017485,
        0.0201586
      ],
      [
        1575417960000,
        0.0201786,
        0.02016635,
        0.02017935,
        0.0201551
      ],
      [
        1575417900000,
        0.0201796,
        0.0201786,
        0.0201831,
        0.02017735
      ],
      [
        1575417840000,
        0.0201706,
        0.0201796,
        0.0201806,
        0.02016935
      ],
      [
        1575417780000,
        0.02017385,
        0.0201706,
        0.0201741,
        0.0201706
      ],
      [
        1575417720000,
        0.02017335,
        0.02017385,
        0.02017435,
        0.02017135
      ],
      [
        1575417660000,
        0.02016935,
        0.02017335,
        0.0201751,
        0.0201686
      ],
      [
        1575417600000,
        0.02017435,
        0.02016935,
        0.02017285,
        0.0201671
      ],
      [
        1575417540000,
        0.02017585,
        0.02017435,
        0.0201771,
        0.0201711
      ],
      [
        1575417480000,
        0.0201786,
        0.02017585,
        0.0201781,
        0.02017585
      ],
      [
        1575417420000,
        0.02018035,
        0.0201786,
        0.02018035,
        0.02017635
      ],
      [
        1575417360000,
        0.0201856,
        0.02018035,
        0.02018685,
        0.0201791
      ],
      [
        1575417300000,
        0.0201846,
        0.0201856,
        0.02018785,
        0.0201846
      ],
      [
        1575417240000,
        0.0201831,
        0.0201846,
        0.0201861,
        0.0201826
      ],
      [
        1575417180000,
        0.02018485,
        0.0201831,
        0.02018835,
        0.02018285
      ],
      [
        1575417120000,
        0.02018885,
        0.02018485,
        0.0201906,
        0.02018485
      ],
      [
        1575417060000,
        0.0201791,
        0.02018885,
        0.02018885,
        0.0201791
      ],
      [
        1575417000000,
        0.02017835,
        0.0201791,
        0.0201806,
        0.02017835
      ],
      [
        1575416940000,
        0.0201746,
        0.02017835,
        0.0201796,
        0.0201741
      ],
      [
        1575416880000,
        0.02017385,
        0.0201746,
        0.0201751,
        0.02017385
      ],
      [
        1575416820000,
        0.02017035,
        0.02017385,
        0.0201751,
        0.0201701
      ],
      [
        1575416760000,
        0.0201706,
        0.02017035,
        0.02017235,
        0.0201696
      ],
      [
        1575416700000,
        0.02017335,
        0.0201706,
        0.0201736,
        0.0201706
      ],
      [
        1575416640000,
        0.02017185,
        0.02017335,
        0.0201741,
        0.02017185
      ],
      [
        1575416580000,
        0.0201651,
        0.02017185,
        0.02017185,
        0.02016435
      ],
      [
        1575416520000,
        0.0201656,
        0.0201651,
        0.0201671,
        0.02016435
      ],
      [
        1575416460000,
        0.02016585,
        0.0201656,
        0.02016835,
        0.0201631
      ],
      [
        1575416400000,
        0.0201636,
        0.02016585,
        0.02016585,
        0.0201631
      ],
      [
        1575416340000,
        0.0201596,
        0.0201636,
        0.0201636,
        0.0201581
      ],
      [
        1575416280000,
        0.0201576,
        0.0201596,
        0.02016135,
        0.0201576
      ],
      [
        1575416220000,
        0.02015885,
        0.0201576,
        0.02015935,
        0.02015585
      ],
      [
        1575416160000,
        0.0201591,
        0.02015885,
        0.0201631,
        0.02015885
      ],
      [
        1575416100000,
        0.02015935,
        0.0201591,
        0.02016335,
        0.0201591
      ],
      [
        1575416040000,
        0.0201641,
        0.02015935,
        0.0201641,
        0.02015885
      ],
      [
        1575415980000,
        0.0201631,
        0.0201641,
        0.0201641,
        0.0201626
      ],
      [
        1575415920000,
        0.02015935,
        0.0201631,
        0.0201641,
        0.02016035
      ],
      [
        1575415860000,
        0.0201616,
        0.02015935,
        0.0201601,
        0.0201581
      ],
      [
        1575415800000,
        0.0201631,
        0.0201616,
        0.02016335,
        0.02015785
      ],
      [
        1575415740000,
        0.0201601,
        0.0201631,
        0.02016385,
        0.0201596
      ],
      [
        1575415680000,
        0.02016085,
        0.0201601,
        0.02016185,
        0.02015785
      ],
      [
        1575415620000,
        0.0201606,
        0.02016085,
        0.02016285,
        0.02015935
      ],
      [
        1575415560000,
        0.02016035,
        0.0201606,
        0.02016285,
        0.0201596
      ],
      [
        1575415500000,
        0.0201601,
        0.02016035,
        0.02016185,
        0.0201586
      ],
      [
        1575415440000,
        0.0201626,
        0.0201601,
        0.02016135,
        0.02015785
      ],
      [
        1575415380000,
        0.02015985,
        0.0201626,
        0.0201626,
        0.0201591
      ],
      [
        1575415320000,
        0.02015935,
        0.02015985,
        0.0201606,
        0.0201581
      ],
      [
        1575415260000,
        0.0201646,
        0.02015935,
        0.02016485,
        0.0201586
      ],
      [
        1575415200000,
        0.0201631,
        0.0201646,
        0.0201646,
        0.02016235
      ],
      [
        1575415140000,
        0.02016435,
        0.0201631,
        0.02016435,
        0.02016185
      ],
      [
        1575415080000,
        0.02016685,
        0.02016435,
        0.02016835,
        0.0201631
      ],
      [
        1575415020000,
        0.02016835,
        0.02016685,
        0.02016835,
        0.02016285
      ],
      [
        1575414960000,
        0.02017135,
        0.02016835,
        0.0201721,
        0.0201641
      ],
      [
        1575414900000,
        0.02017535,
        0.02017135,
        0.02017535,
        0.02017085
      ],
      [
        1575414840000,
        0.02017485,
        0.02017535,
        0.02017685,
        0.02017435
      ],
      [
        1575414780000,
        0.02017435,
        0.02017485,
        0.02017635,
        0.02017385
      ],
      [
        1575414720000,
        0.0201776,
        0.02017435,
        0.02017785,
        0.0201741
      ],
      [
        1575414660000,
        0.0201766,
        0.0201776,
        0.02017835,
        0.02017385
      ],
      [
        1575414600000,
        0.0201741,
        0.0201766,
        0.0201766,
        0.0201741
      ],
      [
        1575414540000,
        0.0201736,
        0.0201741,
        0.0201771,
        0.02017385
      ],
      [
        1575414480000,
        0.02017285,
        0.0201736,
        0.0201741,
        0.02017185
      ],
      [
        1575414420000,
        0.0201716,
        0.02017285,
        0.02017335,
        0.02017085
      ],
      [
        1575414360000,
        0.0201741,
        0.0201716,
        0.02017485,
        0.02016985
      ],
      [
        1575414300000,
        0.0201741,
        0.0201741,
        0.02017685,
        0.02017385
      ],
      [
        1575414240000,
        0.0201751,
        0.0201741,
        0.0201766,
        0.02017385
      ],
      [
        1575414180000,
        0.0201801,
        0.0201751,
        0.0201801,
        0.0201751
      ],
      [
        1575414120000,
        0.0201741,
        0.0201801,
        0.0201801,
        0.0201726
      ],
      [
        1575414060000,
        0.02017285,
        0.0201741,
        0.0201741,
        0.0201726
      ],
      [
        1575414000000,
        0.0201721,
        0.02017285,
        0.0201741,
        0.02016985
      ],
      [
        1575413940000,
        0.02016985,
        0.0201721,
        0.02017235,
        0.0201691
      ],
      [
        1575413880000,
        0.02017035,
        0.02016985,
        0.02017085,
        0.02016835
      ],
      [
        1575413820000,
        0.0201721,
        0.02017035,
        0.0201721,
        0.02016935
      ],
      [
        1575413760000,
        0.02017035,
        0.0201721,
        0.0201721,
        0.02016885
      ],
      [
        1575413700000,
        0.0201681,
        0.02017035,
        0.02017035,
        0.02016685
      ],
      [
        1575413640000,
        0.02016635,
        0.0201681,
        0.0201681,
        0.0201601
      ],
      [
        1575413580000,
        0.0201641,
        0.02016635,
        0.02016635,
        0.02016185
      ],
      [
        1575413520000,
        0.02016535,
        0.0201641,
        0.0201661,
        0.0201621
      ],
      [
        1575413460000,
        0.02016535,
        0.02016535,
        0.02016585,
        0.02016185
      ],
      [
        1575413400000,
        0.02016985,
        0.02016535,
        0.02016985,
        0.02016535
      ],
      [
        1575413340000,
        0.0201686,
        0.02016985,
        0.02016985,
        0.02016435
      ],
      [
        1575413280000,
        0.0201751,
        0.0201686,
        0.0201751,
        0.0201681
      ],
      [
        1575413220000,
        0.0201716,
        0.0201751,
        0.0201751,
        0.0201696
      ],
      [
        1575413160000,
        0.0201626,
        0.0201716,
        0.02017235,
        0.0201666
      ],
      [
        1575413100000,
        0.0201621,
        0.0201626,
        0.0201626,
        0.02015785
      ],
      [
        1575413040000,
        0.02015735,
        0.0201621,
        0.0201621,
        0.0201571
      ],
      [
        1575412980000,
        0.0201641,
        0.02015735,
        0.0201651,
        0.02015685
      ],
      [
        1575412920000,
        0.02016385,
        0.0201641,
        0.02016685,
        0.02016235
      ],
      [
        1575412860000,
        0.0201661,
        0.02016385,
        0.02016785,
        0.02016385
      ],
      [
        1575412800000,
        0.0201661,
        0.0201661,
        0.0201696,
        0.0201641
      ],
      [
        1575412740000,
        0.0201681,
        0.0201661,
        0.0201691,
        0.02016585
      ],
      [
        1575412680000,
        0.0201646,
        0.0201681,
        0.0201681,
        0.0201646
      ],
      [
        1575412620000,
        0.0201641,
        0.0201646,
        0.0201651,
        0.02016285
      ],
      [
        1575412560000,
        0.02015935,
        0.0201641,
        0.02016435,
        0.02015785
      ],
      [
        1575412500000,
        0.0201536,
        0.02015935,
        0.02015985,
        0.0201526
      ],
      [
        1575412440000,
        0.0201526,
        0.0201536,
        0.02015385,
        0.02014835
      ],
      [
        1575412380000,
        0.02015185,
        0.0201526,
        0.0201536,
        0.02014985
      ],
      [
        1575412320000,
        0.0201501,
        0.02015185,
        0.0201531,
        0.0201501
      ],
      [
        1575412260000,
        0.0201626,
        0.0201501,
        0.0201626,
        0.0201501
      ],
      [
        1575412200000,
        0.02016735,
        0.0201626,
        0.02016885,
        0.0201626
      ],
      [
        1575412140000,
        0.0201671,
        0.02016735,
        0.0201711,
        0.02016335
      ],
      [
        1575412080000,
        0.0201626,
        0.0201671,
        0.0201676,
        0.0201646
      ],
      [
        1575412020000,
        0.0201556,
        0.0201626,
        0.0201641,
        0.0201556
      ],
      [
        1575411960000,
        0.02014935,
        0.0201556,
        0.02015885,
        0.02014735
      ],
      [
        1575411900000,
        0.02014785,
        0.02014935,
        0.0201501,
        0.0201466
      ],
      [
        1575411840000,
        0.02015035,
        0.02014785,
        0.02015035,
        0.02014535
      ],
      [
        1575411780000,
        0.02013285,
        0.02015035,
        0.02015035,
        0.02013635
      ],
      [
        1575411720000,
        0.02013685,
        0.02013285,
        0.0201371,
        0.02013285
      ],
      [
        1575411660000,
        0.02013735,
        0.02013685,
        0.0201391,
        0.02013685
      ],
      [
        1575411600000,
        0.0201371,
        0.02013735,
        0.02013885,
        0.02013335
      ],
      [
        1575411540000,
        0.02013185,
        0.0201371,
        0.0201376,
        0.02013235
      ],
      [
        1575411480000,
        0.0201276,
        0.02013185,
        0.02013385,
        0.0201276
      ],
      [
        1575411420000,
        0.0201281,
        0.0201276,
        0.02013235,
        0.0201266
      ],
      [
        1575411360000,
        0.0201291,
        0.0201281,
        0.0201321,
        0.0201261
      ],
      [
        1575411300000,
        0.0201301,
        0.0201291,
        0.0201336,
        0.0201271
      ],
      [
        1575411240000,
        0.0201396,
        0.0201301,
        0.0201416,
        0.0201286
      ],
      [
        1575411180000,
        0.0201626,
        0.0201396,
        0.02016485,
        0.0201396
      ],
      [
        1575411120000,
        0.0201621,
        0.0201626,
        0.02016985,
        0.0201621
      ],
      [
        1575411060000,
        0.0201636,
        0.0201621,
        0.0201656,
        0.02016185
      ],
      [
        1575411000000,
        0.02016335,
        0.0201636,
        0.02016685,
        0.02016185
      ],
      [
        1575410940000,
        0.02016685,
        0.02016335,
        0.0201661,
        0.02015935
      ],
      [
        1575410880000,
        0.0201751,
        0.02016685,
        0.02017685,
        0.0201661
      ],
      [
        1575410820000,
        0.0201756,
        0.0201751,
        0.02017685,
        0.0201726
      ],
      [
        1575410760000,
        0.0201751,
        0.0201756,
        0.02017735,
        0.02017185
      ],
      [
        1575410700000,
        0.02017085,
        0.0201751,
        0.02017735,
        0.0201711
      ],
      [
        1575410640000,
        0.02017235,
        0.02017085,
        0.02017335,
        0.0201706
      ],
      [
        1575410580000,
        0.02017035,
        0.02017235,
        0.02017285,
        0.02017035
      ],
      [
        1575410520000,
        0.02016335,
        0.02017035,
        0.0201721,
        0.02016335
      ],
      [
        1575410460000,
        0.02016435,
        0.02016335,
        0.0201656,
        0.0201631
      ],
      [
        1575410400000,
        0.0201661,
        0.02016435,
        0.0201686,
        0.0201631
      ],
      [
        1575410340000,
        0.02016685,
        0.0201661,
        0.02016735,
        0.0201631
      ],
      [
        1575410280000,
        0.02017135,
        0.02016685,
        0.02017135,
        0.0201651
      ],
      [
        1575410220000,
        0.0201666,
        0.02017135,
        0.02017185,
        0.0201651
      ],
      [
        1575410160000,
        0.02016935,
        0.0201666,
        0.02017135,
        0.02016635
      ],
      [
        1575410100000,
        0.02016935,
        0.02016935,
        0.0201741,
        0.02016935
      ],
      [
        1575410040000,
        0.0201776,
        0.02016935,
        0.0201801,
        0.02016935
      ],
      [
        1575409980000,
        0.02018085,
        0.0201776,
        0.02018085,
        0.02017735
      ],
      [
        1575409920000,
        0.02018085,
        0.02018085,
        0.0201821,
        0.02017835
      ],
      [
        1575409860000,
        0.0201851,
        0.02018085,
        0.02018535,
        0.02017735
      ],
      [
        1575409800000,
        0.02018335,
        0.0201851,
        0.02018585,
        0.02018035
      ],
      [
        1575409740000,
        0.02018335,
        0.02018335,
        0.0201856,
        0.0201751
      ],
      [
        1575409680000,
        0.0201851,
        0.02018335,
        0.0201881,
        0.02018185
      ],
      [
        1575409620000,
        0.0201826,
        0.0201851,
        0.02018585,
        0.02017935
      ],
      [
        1575409560000,
        0.02018335,
        0.0201826,
        0.02018385,
        0.02018135
      ],
      [
        1575409500000,
        0.0201851,
        0.02018335,
        0.0201851,
        0.0201816
      ],
      [
        1575409440000,
        0.0201731,
        0.0201851,
        0.0201851,
        0.0201731
      ],
      [
        1575409380000,
        0.0201726,
        0.0201731,
        0.0201746,
        0.0201726
      ],
      [
        1575409320000,
        0.0201746,
        0.0201726,
        0.0201756,
        0.0201726
      ],
      [
        1575409260000,
        0.0201741,
        0.0201746,
        0.0201761,
        0.0201736
      ],
      [
        1575409200000,
        0.0201721,
        0.0201741,
        0.0201751,
        0.0201716
      ],
      [
        1575409140000,
        0.0201756,
        0.0201721,
        0.0201756,
        0.0201716
      ],
      [
        1575409080000,
        0.0201796,
        0.0201756,
        0.02018035,
        0.0201736
      ],
      [
        1575409020000,
        0.02018135,
        0.0201796,
        0.0201826,
        0.02017885
      ],
      [
        1575408960000,
        0.0201756,
        0.02018135,
        0.02018285,
        0.0201741
      ],
      [
        1575408900000,
        0.0201741,
        0.0201756,
        0.02017635,
        0.02016985
      ],
      [
        1575408840000,
        0.0201776,
        0.0201741,
        0.0201776,
        0.02017385
      ],
      [
        1575408780000,
        0.0201776,
        0.0201776,
        0.0201776,
        0.0201766
      ],
      [
        1575408720000,
        0.02017985,
        0.0201776,
        0.0201801,
        0.0201766
      ],
      [
        1575408660000,
        0.02018385,
        0.02017985,
        0.02018385,
        0.02017985
      ],
      [
        1575408600000,
        0.02018885,
        0.02018385,
        0.02018835,
        0.02018135
      ],
      [
        1575408540000,
        0.02018585,
        0.02018885,
        0.0201896,
        0.02018585
      ],
      [
        1575408480000,
        0.0201841,
        0.02018585,
        0.02018735,
        0.0201841
      ],
      [
        1575408420000,
        0.02018185,
        0.0201841,
        0.0201851,
        0.02017885
      ],
      [
        1575408360000,
        0.0201846,
        0.02018185,
        0.02018485,
        0.02018085
      ],
      [
        1575408300000,
        0.02018035,
        0.0201846,
        0.02018535,
        0.02017835
      ],
      [
        1575408240000,
        0.02018235,
        0.02018035,
        0.0201841,
        0.02017985
      ],
      [
        1575408180000,
        0.0201781,
        0.02018235,
        0.0201831,
        0.0201781
      ],
      [
        1575408120000,
        0.02017785,
        0.0201781,
        0.02017985,
        0.0201776
      ],
      [
        1575408060000,
        0.0201766,
        0.02017785,
        0.02018035,
        0.0201746
      ],
      [
        1575408000000,
        0.0201766,
        0.0201766,
        0.0201771,
        0.0201746
      ],
      [
        1575407940000,
        0.0201716,
        0.0201766,
        0.0201801,
        0.0201711
      ],
      [
        1575407880000,
        0.0201656,
        0.0201716,
        0.02017185,
        0.0201656
      ],
      [
        1575407820000,
        0.02016935,
        0.0201656,
        0.02016885,
        0.02016485
      ],
      [
        1575407760000,
        0.0201686,
        0.02016935,
        0.0201706,
        0.02016835
      ],
      [
        1575407700000,
        0.02016985,
        0.0201686,
        0.0201726,
        0.0201681
      ],
      [
        1575407640000,
        0.0201711,
        0.02016985,
        0.0201716,
        0.0201686
      ],
      [
        1575407580000,
        0.0201616,
        0.0201711,
        0.0201726,
        0.0201626
      ],
      [
        1575407520000,
        0.0201616,
        0.0201616,
        0.02016385,
        0.02016135
      ],
      [
        1575407460000,
        0.02016235,
        0.0201616,
        0.0201631,
        0.02016085
      ],
      [
        1575407400000,
        0.02016135,
        0.02016235,
        0.02016235,
        0.0201596
      ],
      [
        1575407340000,
        0.0201606,
        0.02016135,
        0.02016335,
        0.0201606
      ],
      [
        1575407280000,
        0.0201626,
        0.0201606,
        0.0201641,
        0.0201606
      ],
      [
        1575407220000,
        0.0201711,
        0.0201626,
        0.0201736,
        0.0201606
      ],
      [
        1575407160000,
        0.0201751,
        0.0201711,
        0.02017535,
        0.02016935
      ],
      [
        1575407100000,
        0.0201721,
        0.0201751,
        0.0201771,
        0.0201686
      ],
      [
        1575407040000,
        0.02017435,
        0.0201721,
        0.0201791,
        0.0201721
      ],
      [
        1575406980000,
        0.0201771,
        0.02017435,
        0.0201781,
        0.02017385
      ],
      [
        1575406920000,
        0.02017485,
        0.0201771,
        0.0201786,
        0.02017485
      ],
      [
        1575406860000,
        0.02017535,
        0.02017485,
        0.02017685,
        0.02017485
      ],
      [
        1575406800000,
        0.02016635,
        0.02017535,
        0.02017635,
        0.0201661
      ],
      [
        1575406740000,
        0.02016435,
        0.02016635,
        0.02016785,
        0.0201626
      ],
      [
        1575406680000,
        0.02015985,
        0.02016435,
        0.02016485,
        0.02015735
      ],
      [
        1575406620000,
        0.02015835,
        0.02015985,
        0.02015985,
        0.02015435
      ],
      [
        1575406560000,
        0.0201596,
        0.02015835,
        0.02015985,
        0.0201551
      ],
      [
        1575406500000,
        0.02016235,
        0.0201596,
        0.02016385,
        0.02015885
      ],
      [
        1575406440000,
        0.02016435,
        0.02016235,
        0.0201651,
        0.02016085
      ],
      [
        1575406380000,
        0.0201646,
        0.02016435,
        0.02016535,
        0.02016335
      ],
      [
        1575406320000,
        0.0201716,
        0.0201646,
        0.02017185,
        0.0201636
      ],
      [
        1575406260000,
        0.02017235,
        0.0201716,
        0.0201741,
        0.0201716
      ],
      [
        1575406200000,
        0.02016885,
        0.02017235,
        0.02017385,
        0.0201686
      ],
      [
        1575406140000,
        0.02016985,
        0.02016885,
        0.02017085,
        0.02016885
      ],
      [
        1575406080000,
        0.02017235,
        0.02016985,
        0.0201741,
        0.02016985
      ],
      [
        1575406020000,
        0.0201736,
        0.02017235,
        0.0201736,
        0.02017185
      ],
      [
        1575405960000,
        0.02017185,
        0.0201736,
        0.02017385,
        0.02017135
      ],
      [
        1575405900000,
        0.0201681,
        0.02017185,
        0.0201726,
        0.02016735
      ],
      [
        1575405840000,
        0.02017085,
        0.0201681,
        0.02017085,
        0.02016735
      ],
      [
        1575405780000,
        0.0201686,
        0.02017085,
        0.0201711,
        0.02016785
      ],
      [
        1575405720000,
        0.02016935,
        0.0201686,
        0.02016985,
        0.0201676
      ],
      [
        1575405660000,
        0.02016585,
        0.02016935,
        0.0201696,
        0.0201651
      ],
      [
        1575405600000,
        0.02016685,
        0.02016585,
        0.02016735,
        0.0201646
      ]
    ]
  }
}
```

This endpoint retrieves index chart OHLC of a specific index.

### HTTP Request

`GET https://bff.goesoteric.com/public/indices-detailed-breakdown/<index>/<todo>`

### URL Parameters

Parameter | Description
--------- | -----------
index | The index 
todo | todo

### Request Parameters

Parameter | Required | Description
--------- | ----------- | -----------
limit | false | Limit for data size per page
ts | false | From timestamp in milliseconds

## Get Order Book

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/order-book/XBTUSD/200'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": {
      "ts": 15816876568905832,
      "bids": {
        "10235": 1.30376,
        "10236": 0.081586,
        "10237": 0.127691,
        "10238": 0.366522,
        "10240": 24.3739479999,
        "10241": 0.090064,
        "10242": 0.0020769999,
        "10243": 0.0012099999,
        "10244": 9.400743,
        "10249.39": 0.196964,
        "10249.35": 5.977335,
        "10249.34": 3.5499999999,
        "10249.28": 2,
        "10249.08": 2,
        "10248.89": 0.070299,
        "10248.57": 0.01,
        "10248.24": 0.01,
        "10248.18": 0.2,
        "10248.12": 0.019512,
        "10246.58": 5.6399999999,
        "10246.56": 0.841608,
        "10246.55": 0.091852,
        "10246.2": 0.1154329999,
        "10246.19": 0.103809,
        "10245.9": 0.2,
        "10245.88": 0.2928009999,
        "10245.77": 1.25,
        "10245.56": 1.606115,
        "10245.55": 0.195051,
        "10245.22": 0.2439649999,
        "10244.88": 0.0044879999,
        "10244.87": 0.0011199999,
        "10244.56": 1.606287,
        "10244.33": 0.175426,
        "10244.31": 0.0869999999,
        "10244.11": 0.7335979999,
        "10244.03": 0.5839999999,
        "10243.91": 0.130304,
        "10243.9": 1.6063689999,
        "10243.63": 0.002,
        "10243.49": 0.0168239999,
        "10243.31": 0.2999999999,
        "10243.3": 1.606478,
        "10243.19": 0.2,
        "10243.18": 0.4,
        "10243.16": 0.244039,
        "10243.15": 0.0336489999,
        "10243.13": 4.4,
        "10243.09": 0.01682,
        "10243.05": 0.016108,
        "10242.18": 0.225828,
        "10241.74": 0.0336289999,
        "10241.67": 0.2214359999,
        "10241.11": 0.160975,
        "10241.1": 0.244061,
        "10240.99": 0.0488009999,
        "10240.92": 0.195294,
        "10240.5": 0.183678,
        "10240.2": 0.3952379999,
        "10240.1": 0.240073,
        "10240.03": 0.152429,
        "10239.72": 0.317338,
        "10239.6": 0.14649,
        "10239.25": 1,
        "10239.19": 0.100927,
        "10239.04": 0.244115,
        "10238.95": 0.2,
        "10238.93": 0.2441659999,
        "10238.92": 0.388952,
        "10238.88": 0.030394,
        "10238.86": 0.095956,
        "10238.23": 0.0285669999,
        "10238.22": 0.244183,
        "10238.19": 0.0034169999,
        "10237.8": 0.226379,
        "10237.79": 0.01,
        "10237.5": 0.001678,
        "10237.37": 0.0010269999,
        "10237.17": 0.251039,
        "10236.98": 0.244185,
        "10236.84": 0.02,
        "10236.74": 0.3048589999,
        "10236.61": 0.012503,
        "10236.5": 0.100338,
        "10236.21": 1.4269689999,
        "10236.19": 0.002089,
        "10236.16": 0.0376649999,
        "10236.12": 0.0120059999,
        "10235.85": 0.065753,
        "10235.56": 3.173,
        "10235.53": 0.0010499999,
        "10235.36": 0.01,
        "10235.09": 0.036537,
        "10234.93": 0.244197,
        "10234.89": 0.2802879999,
        "10234.88": 0.001309,
        "10234.78": 0.0010499999,
        "10234.69": 0.01,
        "10234.68": 0.0035049999,
        "10234.51": 0.0053699999
      },
      "asks": {
        "10260": 0.1248129999,
        "10263": 0.4245209999,
        "10264": 0.143539,
        "10265": 0.127448,
        "10266": 0.047008,
        "10267": 1.015334,
        "10268": 0.1268529999,
        "10269": 0.317711,
        "10270": 5.047899,
        "10271": 0.1467,
        "10272": 0.271602,
        "10251.77": 0.4975919999,
        "10251.78": 0.068425,
        "10251.81": 2,
        "10251.85": 2,
        "10251.86": 2,
        "10251.88": 0.2999999999,
        "10251.98": 0.437466,
        "10251.99": 0.0299999999,
        "10252.87": 0.010943,
        "10252.9": 0.243921,
        "10252.93": 0.402316,
        "10253.63": 0.425283,
        "10253.7": 0.329095,
        "10253.99": 0.1,
        "10254.49": 0.2,
        "10255.17": 0.002926,
        "10255.31": 0.3999619999,
        "10255.32": 0.3911029999,
        "10255.33": 0.149428,
        "10255.34": 0.144064,
        "10255.35": 0.0488009999,
        "10255.59": 0.1306509999,
        "10256.4": 0.131441,
        "10256.41": 0.1993689999,
        "10256.49": 0.191283,
        "10256.5": 1.44665,
        "10256.63": 0.04,
        "10256.92": 0.2399999999,
        "10257.48": 0.3157929999,
        "10257.54": 0.05,
        "10258.74": 0.0025339999,
        "10259.05": 0.023192,
        "10259.08": 0.00936,
        "10259.36": 0.4258259999,
        "10259.54": 4.4,
        "10259.63": 0.243685,
        "10259.85": 0.036614,
        "10260.19": 3.9089999999,
        "10260.31": 0.11271,
        "10260.49": 0.1542179999,
        "10260.5": 0.003504,
        "10260.69": 0.1605179999,
        "10261.34": 0.195053,
        "10261.37": 0.04761,
        "10261.67": 0.0016999999,
        "10261.69": 0.243685,
        "10262.02": 0.162524,
        "10262.03": 0.0245389999,
        "10262.61": 0.194882,
        "10262.64": 0.252,
        "10263.74": 0.185564,
        "10263.75": 0.2436099999,
        "10264.42": 4.248,
        "10264.9": 0.044524,
        "10265.07": 0.0971899999,
        "10265.81": 0.2435269999,
        "10266.36": 0.016806,
        "10266.66": 0.0016,
        "10266.81": 0.0336199999,
        "10267.53": 0.117072,
        "10267.87": 0.243479,
        "10267.92": 0.2921719999,
        "10267.93": 0.0336199999,
        "10268.32": 0.174468,
        "10268.52": 0.1,
        "10268.53": 0.016784,
        "10268.65": 4.024,
        "10269.23": 0.001021,
        "10269.25": 0.5,
        "10269.84": 0.012259,
        "10269.92": 0.243546,
        "10269.97": 0.6872129999,
        "10269.99": 0.078392,
        "10270.04": 0.0019469999,
        "10270.23": 0.017288,
        "10270.51": 0.028791,
        "10270.56": 8.8,
        "10270.8": 0.0020939999,
        "10270.83": 0.001064,
        "10271.17": 0.0013209999,
        "10271.41": 0.0025799999,
        "10271.69": 6.232033,
        "10271.98": 0.243546,
        "10272.09": 0.1947019999,
        "10272.1": 0.048675,
        "10272.23": 0.051511,
        "10272.56": 0.1008339999,
        "10272.61": 0.3135999999,
        "10272.7": 0.001946
      }
    }
  }
}
```

This endpoint retrieves a specific order book.

### HTTP Request

`GET https://bff.goesoteric.com/public/order-book/<contractsymbol>/<ordernumber>`

### URL Parameters

Parameter | Description
--------- | -----------
contractsymbol | The symbol of the contract
ordernumber | The specific ordernumber

## Get Cache Delete

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/all-cache/all' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
    "success": {
        "code": 100,
        "message": "Success",
        "data": "Successfully deleted."
    }
}
```

This endpoint delete cache.

### HTTP Request

`GET https://bff.goesoteric.com/public/order-book/cache-delete/all`

## Get Cache 

```shell
curl --location --request GET 'https://bff.goesoteric.com/public/all-cache/all' \
--header 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
    "success": {
        "code": 100,
        "message": "Success",
        "data": "Successfully deleted."
    }
}
```

This endpoint get cache.

### HTTP Request

`GET https://bff.goesoteric.com/public/order-book/cache-delete/all`

# Orders/Wallet Endpoints

## HMAC Signature Calculation

```
// Example for calculating signature message for a POST Request to {{base_url}}/api/open-orders
{
    timestamp:1587820973,
    recvWindow:10000,
    orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'
}

signature_message = "POST" + "\n" + "/api/open-orders" + "\n" + "1587820973" + "{timestamp:1587820973,recvWindow:10000,orderID:'3ec4facb-c2bf-4bdf-8adf-b11e2851d235'}"
signature = HMAC(signature_message)

// computed signature should be Hexadecimal equivalent of the HMAC signature. 
```

Message authentication signature. The request message is hashed with the API secret key using SHA256 algorithm. The structure of the message:

* Request method. (e.g. "GET or "POST")
* Request URI including the query parameters for GET.
* The unix timestamp value
* The payload in JSON format only for POST.
* To ensure the signature is successfully validated, please be aware of the following:
    * Each piece of information in the signature message should be separated by a new line. (see the example)
    * The payload should not contain any whitespace between the names and values
    * The Request URI should not contain the host name. e.g. `/api/orders` instead of `https://myexchange.com/api/orders`

Python Snippet: https://repl.it/@AnkitSinghal1/modulus-derivatives-hmac-signature-python

## POST New Order

```shell
curl --location --request POST 'https://bff.goesoteric.com/api/new-order' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: FBDF9E1CC798C5897D6E32A2ED336B762C3E3565ABE16A482DC0E30A2F775227B18F0D93E77F38BB6397C73FA814E165D237B85AE01CA6510E9DE528ADA29DB2' \
--data-raw '{
    "symbol": "XBTUSD",
    "side": "SELL",
    "orderQty": 1,
    "price": 100,
    "stopPrice": 0,
    "orderType": "LIMIT",
    "timeinForce": "DO"
}'
```

> The above command returns JSON structured like this:

```json
{
  "error": {
    "code": 3037,
    "message": "Payload_Instant_Liquidation",
    "description": {
      "natsPayload": {
        "symbol": "XBTUSD",
        "size": 1,
        "side": 2,
        "type": 2,
        "timeInForce": 2,
        "limitPrice": 100,
        "stopPrice": 0,
        "trailingAmount": 0,
        "orderID": "8b9fe45a-17a1-4df5-b074-eb78ce10824e",
        "userID": "332424",
        "balance": 10,
        "orderMargin": 0.01040456,
        "liquidationPrice": 104.26539296,
        "takerFee": 0.075,
        "makerFee": -0.025,
        "filledPrice": 0,
        "orderValue": 0.01
      },
      "mtCalc": {
        "liquidationPrice": 104.26539296,
        "maintainanceMarginPerc": 5,
        "initialMarginPerc": 9.0909,
        "leverage": 11,
        "initialCollateral": 0.00090909,
        "takerfeePerc": 0.075,
        "fundingRate": 0.91,
        "markPrice": 9054.91,
        "orderSize": 0.01,
        "transactionFee": -0.0000075,
        "twoWayFee": 0.000015,
        "maintainanceMargin": 0.0005,
        "costNormal": 0.00092409,
        "costAbnormal": 0.01040456,
        "cost": 0.01040456,
        "pLatMarkPrice": -0.00988956
      }
    }
  }
}
```

This endpoint create a new order

### HTTP Request

`POST https://bff.goesoteric.com/api/new-order`

Note: place order using api-key and HMAC authentication.

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
symbol | Yes | XBTUSD
side| Yes | BUY,SELL
orderQty | Yes | Integer and Greater than Zero
price | Yes | Decimal and Greater than Zero
stopPrice | Yes |	Decimal and Greater than Zero
orderType	| Yes	| LIMIT
timeinForce	| NO |	GTC
triggerType	| NO | 	MarkPrice
isReduceOnly | NO | True/False
IsCloseOnTrigger | NO | True/False
IsPostOnly | NO | True/False

## POST Cancel Order

```shell
curl --location --request POST '{{api_url}}/api/cancel-order' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: EF950375703CE12226EE653B78B5154B3563ECFA0C458C0476025C4246B0CCBB52E2987CF2E95BDEB6D5A8E01BF87302DF0C8EE601DC4716B918979F27451C89' \
--data-raw '{
	"timestamp":"1587820973",
	"recvWindow":10000,
	"orderID":"3ec4facb-c2bf-4bdf-8adf-b11e2851d235"
}'
```

This endpoint cancel a new order

### HTTP Request

`POST https://bff.goesoteric.com/api/cancel-order`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
orderID | Yes | string

## POST All Orders

```shell
curl --location --request POST 'https://bff.goesoteric.com/api/new-order' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: FBDF9E1CC798C5897D6E32A2ED336B762C3E3565ABE16A482DC0E30A2F775227B18F0D93E77F38BB6397C73FA814E165D237B85AE01CA6510E9DE528ADA29DB2' \
--data-raw '{
    "symbol": "XBTUSD",
    "side": "SELL",
    "orderQty": 1,
    "price": 100,
    "stopPrice": 0,
    "orderType": "LIMIT",
    "timeinForce": "DO"
}'
```

This endpoint post all order // todo

### HTTP Request

`POST https://bff.goesoteric.com/api/all-orders`

Note: place order using api-key and HMAC authentication.

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
DateTo | NO | string 'yyyy/mm/dd'
DateFrom | NO | string 'yyyy/mm/dd'
Contract | NO | XBTUSD
OrderStatus | NO | true or false
Limit | NO | MAX:1000
timestamp | YES | Current UTC TS
recvWindow | YES | Default: 30sec ,any integar value

### Response

FieldName |	Short Description
--------- | -----------
sym | Symbol or ContractName
o | Orderid
sp | Stop price
p | Price
r |	Remaining
s | Order Side "S": Sell, "B": Buy
ts | Accepted Timestamp
u | UserID
q | Quantity or Size
st | Order Status
tif | Time in force
t | Order Type
v | Order Value
fp | Filled Price
odst | Order detailed Status

## POST My Trade History

```shell
curl --location --request POST '{{api_url}}/LP/my-trade-history' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: 14F846BFC247D40B56A71547888C0E51D226E835683A530BE55A27ED93C3B6F1681C4F8EFED8BAD949B9C8A12D8E323A931FD33FD54B703D23367E272E662ECB' \
--data-raw '{
	"side":"sell",
	"symbol":"",
	"orderid":""
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      {
        "sym": "XBTUSD",
        "ts": 1583394834,
        "o": "d3e87c02-d02d-4078-aef9-b4e2e29fcf51",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8800,
        "ep": 8800,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583403228,
        "o": "d145b742-716e-470a-bcaf-2052ea918be6",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583404613,
        "o": "01bf5823-b4be-41b3-83bd-98bb767ab15f",
        "q": 20,
        "eq": 20,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583404622,
        "o": "6efbd950-2bd0-4d84-88a8-0871184cbbb2",
        "q": 20,
        "eq": 20,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583404742,
        "o": "bc2aab73-ad09-4a76-a7be-f54a5e4a8711",
        "q": 10,
        "eq": 10,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583408427,
        "o": "1a1052d7-5511-496b-addd-b54cc4c2a3a8",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583408427,
        "o": "fc5c5144-e448-4fc4-9593-80c8f9e0dcbf",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583408427,
        "o": "a38426e2-1d45-4baa-8341-d4f0a9ed9bea",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583408427,
        "o": "16d6d58b-856c-46aa-824f-e69e86191805",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583408427,
        "o": "8fefe614-ed72-4d4b-9aab-685503d59e1f",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583408427,
        "o": "981f7364-6c2d-46f3-9e0a-8db37dd030ee",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583408897,
        "o": "b16769b3-29d4-4ae2-877a-2d88b998703c",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583408897,
        "o": "b042b4bb-1e9a-4249-bbd4-26086f1f9dce",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583408897,
        "o": "8772caa0-b528-471a-8aaa-5822cbd47705",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583409787,
        "o": "d1cd5a23-3091-47b7-81f1-3cfb71bac328",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583409787,
        "o": "7b48270e-3cab-4df7-93eb-5241ccf5250c",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583409787,
        "o": "67918f29-1206-443b-916d-914c9030c4b3",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583409787,
        "o": "c421bf21-dab0-491c-b188-ea510d5541b9",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583410932,
        "o": "2fb6469a-3740-4cc7-9839-e8c30a26e748",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583410932,
        "o": "49e0819f-dc8f-4386-bcba-50a5455402dd",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583410933,
        "o": "baeea5e3-8d44-4e99-a09d-67c30a4b72f8",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583410942,
        "o": "6883df1e-1885-4d3c-a1fe-510e4f1901f6",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583410944,
        "o": "9401bee2-5850-48d8-828e-a8120263c8c8",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8900,
        "ep": 8900,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411669,
        "o": "c3f6ac51-ccb6-4fda-b5dd-c833d12ec051",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411673,
        "o": "40397084-98ed-49dd-ac5c-80fd53029e7f",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411678,
        "o": "1a861ad7-6445-4c8c-bee2-ef392482fc22",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411680,
        "o": "7f2b5e0f-4435-4d10-aabd-6138a86e18ca",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411680,
        "o": "f07eebf8-9fcb-448b-bc6b-5341aac2db22",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411680,
        "o": "0a637876-361b-4731-9fae-abe818f3c68c",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411680,
        "o": "609ed9b8-6cb1-4a8d-b32e-e34dc84effe2",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411682,
        "o": "a8fc873d-a04d-4d23-93eb-55dee412ed22",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411682,
        "o": "a30f71e0-37b4-4268-9818-4498ee5c9c5c",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411689,
        "o": "2bfe50a4-6305-4af5-bbcd-25a6292e93b2",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411689,
        "o": "1136d988-13a5-401b-946b-132cb9e100e3",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411689,
        "o": "b365808d-67dc-4f7c-a668-5ec76ddd4f77",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411689,
        "o": "0a15a7ee-dbf8-4a4c-b3a5-8585e8925a17",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411690,
        "o": "a0b24a16-89a3-4892-b0d0-53810a377456",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411703,
        "o": "7d01ba99-bfae-48c4-bf8d-31f6deb84888",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411705,
        "o": "19e27c85-b369-4760-88cb-7b7cbab59f12",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411706,
        "o": "569ab73e-e1cb-4cb8-8d57-4c887dedd4af",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896.5,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411757,
        "o": "427054a0-2b12-4afa-b7fc-3bf71e476bbc",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411759,
        "o": "070f683f-9d4c-47cd-a277-66e4f6442aae",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      },
      {
        "sym": "XBTUSD",
        "ts": 1583411761,
        "o": "d3355d81-d75a-4841-968f-5f3972a20544",
        "q": 1,
        "eq": 1,
        "v": 0,
        "t": "Limit",
        "sp": 0,
        "p": 8896,
        "ep": 8896.5,
        "r": 0,
        "s": "S",
        "tif": "GTC"
      }
    ]
  }
}      
```


This endpoint post my trade history  //todo

### HTTP Request

`POST https://bff.goesoteric.com/api/my-trade-history`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
DateTo | NO | string 'yyyy/mm/dd'
DateFrom | NO | string 'yyyy/mm/dd'
Contract | NO | XBTUSD

### Response

FieldName |	Short Description
--------- | -----------
sym | Symbol or ContractName
ts | Timestamp
o | Orderid
q	| Quantity or Size
eq | Entry Quantity
v	| Order Value
t	| Order Type
sp | Stop price
p	| Price
ep | Entry Price
r	| Remaining
s	| Order Side "S": Sell, "B": Buy
tif	| Time in force

## POST My Trade History

```shell
curl --location --request POST '{{api_url}}/api/open-orders' \
--header 'apiKey: cee3d621-86b6-4db2-85a8-f69db6b4cc99' \
--header 'Content-Type: application/json' \
--header 'HMAC: eedcfe4022dce12898e9171327de3daa3e1339dd5f788a778effdc85d02456b5' \
--data-raw '{
	"timestamp":"1590230834",
	"recvWindow":10000,
	"Contract":"XBTUSD"
}'
```

This endpoint post open orders  //todo

### HTTP Request

`POST https://bff.goesoteric.com/api/open-orders`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
Contract | NO | XBTUSD

## POST Wallet Balance

```shell
curl --location --request POST '{{api_url}}/api/wallet-balance' \
--header 'apiKey: 5693851c-7030-4383-b814-dc47336ac137' \
--header 'Content-Type: application/json' \
--header 'HMAC: 56E8B6C4AE66DBFFF1C11E79C03F9938E9C8A0E1B4005DFEE7769700B861A9B411C9FDF7ACB048F643E793A9890B01410F1A82B69C87C5920BDB54E33DA3FDF8' \
--data-raw '{
	"timestamp":"1587820973",
	"recvWindow":10000,
	"currency":"BTC"
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": {
    "code": 100,
    "message": "Success",
    "data": [
      {
        "currency": "BTC",
        "balance": 25.90798327
      }
    ]
  }
}
```

This endpoint get wallet balance

### HTTP Request

`POST https://bff.goesoteric.com/api/wallet-balance`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
Contract | NO | XBTUSD

## POST Cancel Muliti Orders

```shell
curl --location --request POST '{{api_url}}/api/cancel-multi-orders' \
--header 'Content-Type: application/json' \
--header 'apiKey: cee3d621-86b6-4db2-85a8-f69db6b4cc99' \
--header 'HMAC: 213f60555b3eda2c79c8fc36e01363407041e03af351b5f73518133377937110' \
--data-raw '{
	 "timestamp":"1590230475",
	"recvWindow":1000,
	"Oid": [
		{
			"Orderid":"07114653-9fa0-4c5d-a797-14936cfc33a3"
		},
		{
			"Orderid":"39e9cfc8-2cfe-48a7-ad0a-927490818ca8"
		}
		]
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": [
    {
      "success": {
        "code": 100,
        "message": "Success",
        "data": {
          "userID": "332424",
          "orderID": "39e9cfc8-2cfe-48a7-ad0a-927490818ca8"
        }
      }
    }
  ],
  "error": [
    {
      "error": {
        "code": 3036,
        "message": "Payload_Invalid_OrderID",
        "description": " Invalid orderid "
      }
    }
  ]
}
```

This endpoint cancel multi orders.

### HTTP Request

`POST https://bff.goesoteric.com/api/cancel-multi-orders`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
Contract | NO | XBTUSD

## POST Cancel All Orders

```shell
curl --location --request POST '{{api_url}}/api/cancel-all-orders' \
--header 'Content-Type: application/json' \
--header 'apiKey: cee3d621-86b6-4db2-85a8-f69db6b4cc99' \
--header 'HMAC: 90e665bf0ab0f2867bc9472a8762ff336a984d4361ec819e0beac328238852bf' \
--data-raw '{
	"timestamp":"1590230603",
	"recvWindow":1000
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": [
    {
      "success": {
        "code": 100,
        "message": "Success",
        "data": {
          "userID": "332424",
          "orderID": "d45e47a8-24f1-4718-b350-77798a91f67a"
        }
      }
    }
  ],
  "error": []
}
```

This endpoint cancel all orders.

### HTTP Request

`POST https://bff.goesoteric.com/api/cancel-all-orders`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
timestamp | YES | Current TS in seconds
recvWindow | NO	| Default is 10 seconds
Contract | NO | XBTUSD

## POST Place All Orders

```shell
curl --location --request POST '{{api_url}}/api/place-multi-orders' \
--header 'apiKey: cee3d621-86b6-4db2-85a8-f69db6b4cc99' \
--header 'Content-Type: application/json' \
--header 'HMAC: 773a9a4fcdd64473c0453846c3b0a91e6848a9d93a79a6fab1be731b88d1445d' \
--data-raw '{
     "timestamp":"1590229685",
	"recvWindow":1000,
	"Orderpayload": [
		{
		  "symbol": "XBTUSD",
		  "side": "BUY",
		  "orderQty": 2,
		  "price": 30,
		  "stopPrice": 0,
		  "orderType": "LIMIT",
		  "timeinForce": "GTC",
		  "triggerType": "LastPrice",
		  "isReduceOnly": false,
		  "IsCloseOnTrigger": false,
		  "IsHiddenOrder": false,
		  "IsPostOnly": false
		},
		{
		  "symbol": "XBTUSD",
		  "side": "SELL",
		  "orderQty": 1,
		  "price": 7030,
		  "stopPrice": 0,
		  "orderType": "LIMIT",
		  "timeinForce": "GTC",
		  "triggerType": "LastPrice",
		  "isReduceOnly": false,
		  "IsCloseOnTrigger": false,
		  "IsHiddenOrder": false,
		  "IsPostOnly": false
		}
	]
}
'
```

> The above command returns JSON structured like this:

```json
{
  "success": [
    {
      "success": {
        "code": 100,
        "message": "Success",
        "data": {
          "natsPayload": {
            "symbol": "XBTUSD",
            "size": 2,
            "side": 1,
            "type": 2,
            "timeInForce": 1,
            "limitPrice": 30,
            "stopPrice": 0,
            "trailingAmount": 0,
            "orderID": "39e9cfc8-2cfe-48a7-ad0a-927490818ca8",
            "userID": "332424",
            "balance": 100000,
            "orderMargin": 0.00068132,
            "liquidationPrice": 0.00001999,
            "takerFee": 0.011,
            "makerFee": -0.025,
            "filledPrice": 0,
            "orderValue": 0.06666666,
            "isReduceOnly": false,
            "isCloseOnTrigger": false,
            "isHiddenOrder": false,
            "isPostOnly": false,
            "triggerType": 0
          },
          "mtCalc": {
            "liquidationPrice": 0.00001999,
            "maintainanceMarginPerc": 0.5,
            "initialMarginPerc": 1,
            "leverage": 0,
            "initialCollateral": 0.00066666,
            "takerfeePerc": 0.011,
            "fundingRate": 0,
            "markPrice": 8748.51,
            "orderSize": 0.06666666,
            "transactionFee": -0.00000733,
            "twoWayFee": 0.00001466,
            "maintainanceMargin": 0.00033333,
            "costNormal": 0.00068132,
            "costAbnormal": -0.06609006,
            "cost": 0.00068132,
            "pLatMarkPrice": 0.06643805,
            "costOfPlacingNewOrder": 0.0006813333
          }
        }
      }
    },
    {
      "success": {
        "code": 100,
        "message": "Success",
        "data": {
          "natsPayload": {
            "symbol": "XBTUSD",
            "size": 1,
            "side": 2,
            "type": 2,
            "timeInForce": 1,
            "limitPrice": 7030,
            "stopPrice": 0,
            "trailingAmount": 0,
            "orderID": "340a1eb4-f502-47f7-8518-15a1b36feaf2",
            "userID": "332424",
            "balance": 100000,
            "orderMargin": 0.00002867,
            "liquidationPrice": 1000000,
            "takerFee": 0.011,
            "makerFee": -0.025,
            "filledPrice": 0,
  
```

This endpoint place multi orders.

### HTTP Request

`POST https://bff.goesoteric.com/api/place-all-orders`

### Request Payload

FieldName | Mandatory | Valid Values
--------- | ----------- | -----------
symbol | Yes | XBTUSD
side | Yes | BUY,SELL
orderQty | Yes | Integer and Greater than Zero
price | Yes | Decimal and Greater than Zero
stopPrice | Yes | Decimal and Greater than Zero
orderType | Yes| LIMIT,MARKET,STOPMARKET,STOPLIMIT,TAKEPROFITLIMIT,TAKEPROFITMARKET
timeinForce	| NO | GTC,DO,IOC,FOK
triggerType | NO	| MarkPrice,IndexPrice,LastPrice
isReduceOnly | NO | True/False
IsCloseOnTrigger | NO | True/False
IsPostOnly | NO | True/False
