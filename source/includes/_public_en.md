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
      "rate": "-0.00500000",// Funding rate
      "contractId": "1",// Contract ID
      "nextFundingTime":1753459200000,
      "ts": 1687250525704 // Timestamp
    }
  ]
}
```

**HTTP Request**

`GET https://api.coincall.com/open/public/fundingRate/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD,ETHUSD | false | Contract name (if not passed, all will be taken. Multiple can be taken separated by commas)

## Set Countdown(SIGNED)

Set countdown time, only opened for MM.

> Response:

```json
{
  "code": 0,
  "msg": "success",
  "i18nArgs": null,
  "data": true
}
```

**HTTP Request**

`POST https://api.coincall.com/open/futures/countdown/cancel/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | Contract name
type | integer | 1 | true | Type of trade, 1:options, 2:futures, 3:spot
countdownTime | integer | 120000 | true | countdown time(ms)

## Get Countdown Settings

Get Countdown Settings, only opened for MM.

> Response:

```json
{
  "code": 0,
  "msg": "success",
  "i18nArgs": null,
  "data": [
		{
			//"status": 1,      // Status: 0:Disconnected, 1:effect. Only return status=1 
			"type": 1,                      
		  "symbol": "BTCUSD",
		  "countdownTime": 120000  
		},
		{
			//"status": 0,          
			"type": 2,                      
		  "symbol": "BTCUSD",
		  "countdownTime": 100000  
		},
		{
			//"status": 0, 
			"type": 3,                      
		  "symbol": "TRXUSDT",
		  "countdownTime": 30000  
		},
	]
}
```

**HTTP Request**

`GET https://api.coincall.com/open/futures/countdown/cancel/get/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
type | integer | 1 | true | Type of trade, 1:options, 2:futures, 3:spot

## Reset Countdown Settings

Reset Countdown Settings, only opened for MM.

> Response:

```json
{
  "code": 0,
  "msg": "success",
  "i18nArgs": null,
  "data": ["BTCUSD","ETHUSD"]     // Symbol which was set successfully
}
```

**HTTP Request**

`POST https://api.coincall.com/open/futures/countdown/cancel/heartbeat/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD,ETHUSD | true | Contract name
type | integer | 1 | true | Type of trade, 1:options, 2:futures, 3:spot
