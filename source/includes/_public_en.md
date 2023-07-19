# Public Endpoints

## Check Server Time

Test connectivity to the Rest API and get the current server time.

> Response:

```json

{
    "code":0,
    "msg":null,
    "i18nArgs":null,
    "data":{
        "serverTime":1687250525704 // Server time
    }
}
```

**HTTP Request**

`GET https://api.coincall.com/time`

**Parameter**

Null

## Get Public Configurations

Get trading-related configuration

> Response:

```json
{
    "code":0,
    "msg":"Success",
    "i18nArgs":null,
    "data":{
        // Options configuration
        "optionConfig":{
            "BTCUSD":{
                "symbol":"BTCUSD", // Symbol
                "takerFee":0.0004, // Taker fee
                "maxOrderNumber":200, // Maximum number of open orders
                "multiplier":0.01, // Multiplier
                "settle":"USD", // Settlement currency
                "priceDecimal":2, // Decimal of price
                "limitMaxQty":1000, // Maximum value of quantity for limit order
                "tickDecimal":1, // Decimal of tick
                "tickSize":0.1, // Tick size
                "greeksDecimal":5, // Decimal of greeks
                "makerFee":0.0003, // Maker fee
                "marketMaxQty":100, // Maximum value of quantity for market order
                "qtyDecimal":2, // Decimal of quantity
                "maxPositionQty":1000, // Maximum quantity of position
                "base":"BTC" // Base token
            }
        },
        "futuresConfig":{
            "BTCUSD":{
                "symbol":"BTCUSD", // Symbol
                "positionQty":100000000, // Maximum quantity of position
                "takerFee":0.0006, // Taker fee
                "maxOrderNumber":200, // Maximum number of open orders
                "settle":"USD", // Settlement currency
                "priceDecimal":1, // price of Decimal
                "limitMaxQty":1000, // Maximum value of quantity for limit order
                "tickDecimal":1, // Decimal of tick
                "tickSize":0.1, // Tick size
                "makerFee":0.0002, // Maker fee
                "triggerLimit":20, 
                "marketMaxQty":120,// Maximum value of quantity for market order
                "qtyDecimal":3, // Decimal of quantity
                "base":"BTC", // Base token
                "minQty":0.001 // Minimum value of quantity
            }
        }
    }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/public/config/v1`

**Parameter**

Null

## Get Funding Rate

Get real-time funding rate

> Response:

```json
{
  "code": 0,// Status code
  "msg": "Success",// Message
  "i18nArgs": null,
  "data": [
    {
      "symbol": "BTCUSD",// Symbol
      "rate": "-0.00500000",// Margin rate
      "contractId": "1"// Contract ID
    }
  ]
}
```

**HTTP Request**

`GET https://api.coincall.com/open/public/fundingRate/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSDT,ETHUSDT | false | Contract name (if not passed, all will be taken. Multiple can be taken separated by commas)