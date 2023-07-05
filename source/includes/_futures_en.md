# Futures Endpoints

## Get Symbol Information

Get futures symbol

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": [{
		"contractId": 1,// Contract ID
		"symbol": "BTCUSD",// Symbol
		"symbolName":"BTC/USD",// Symbol name
		"displayName":"BTC-PERP",// Symbol display name
		"baseToken":"BTC",// Base Token
		"quoteToken":"USD",// Quote Token
		"price": 25614.7,// Price
		"changeRate": -0.003,// Price change in percentage
		"changePrice":-78.2,// Price change in value
		"markPrice": 25661.25861712,// Mark price
		"indexPrice": 25754.025,// Index Price
		"price24hHigh": 27065.7,// Highest price in 24hrs
		"price24hLow": 18000,// Lowest price in 24hrs
		"volumeUsd24h": 3846213875.0958,// USD volume in 24hrs
		"volume24h": 147370.135,// Volume in 24hrs
		"ts": 20201116024818,// Timestamp
		"price24hOpen":25692.9,// Open price on UTC 00:00:00
		"hasOption":true,// Whether there are options
		"sortIdx":null // Sort Field
	}]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/market/symbol/v1`


**Parameter**

Null

## Get OrderBook 

 Get futures order book for 100 depth

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": {
		"symbol": "BTCUSD",// Symbol
		"bids": [{
			"size": "0.001",// Size
			"price": "18801"// Price
		}],
		"asks": [{
			"size": "0.992",// Size
			"price": "18898"// Price
		}]
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/order/orderbook/v1/{}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | Symbol name

## Get Last Trade

Get futures last trade

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": [{
		"symbol": "BTCUSD",// Symbol
		"price": "18898",// Price
		"qty": "0.001",// Quantity
		"time": 1666754916559,// Time of the transaction
		"tradeSide": 1 // Trade side
	}]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/trade/lasttrade/v1/{}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | Symbol name

## Get leverage

Get current futrues leverage

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",
  "i18nArgs": null,
  "data": {
    "userId": 123,// User ID
    "symbol": "BTCUSD",// Symbol
    "currentLeverage": 5 // Current leverage
  }
}
```

**HTTP Request**

`GET https://api.coincall.com/open/futures/leverage/current/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | Symbol name

## Set Leverage

 Set futures leverage

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": null
}
```

**HTTP Request**

`POST https://api.coincall.com/open/futures/leverage/set/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | Symbol name
leverage | number | 10 | true | leverage for this symbol


## Get Positions(SIGNED)

Get futures positions

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": [
    {
      "id": 1584467417583730700,// ID
      "positionId": 1584467417583730700,// Position ID
      "updateTime": 1666602220413,// Update time
      "userId": 1536933707941347300,// User ID
      "value": 176.7825,// Value of Position
      "qty": 0.009,// Quantity
      "initMargin": 35.3565,// Initial margin
      "maintMargin": 1.767825,// Maintnance margin
      "avgPrice": 19642.5,// Average price
      "markPrice": 18900.38311437,// Mark price
      "elp": null,// Estimated liquidation price
      "roi": -0.03778118,// ROI
      "upnl": -6.67905197067,// Unrealized Pnl
      "symbol": "BTCUSD",//symbol
	  "displayName": "BTC-PERP",// Display name
      "tradeSide": 1,// Trade side
      "leverage": 5,// Leverage
      "delta": 0.009,// Position delta
	  "baseToken": "BTC", // Base token
      "quoteToken": "USD" // Quote token
    }]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/position/get/v1`

**Parameter**

Null

## Place Order(SIGNED)

 Place a futures order

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": 1673571411341475840 // Order id
}
```


**HTTP Request**

`POST https://api.coincall.com/open/futures/order/create/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
clientOrderId | number | 123123123 | false | client order id
symbol | string | BTCUSD | true | Futures Symbol 
price | number | 19000.01 | false | Price, required for limit orders
qty | number | 0.5 | true | Quantity 
tradeSide | number | 1 | true | Trade Side, 1 BUY 2 SELL
tradeType | number | 1 | true | Trade Type, 1 LIMIT 2 MARKET 3 POST_ONLY

<!-- reduceOnly | number | 1 | false | Reduce the position quantity only, 1 reduce only true, 0 reduce only false -->

## Cancel Order(SIGNED)

Cancel a futures order

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": null
}
```


**HTTP Request**

`POST https://api.coincall.com/open/futures/order/cancel/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
orderId | number | 111 | true | query string
clientOrderId | number | 123123123 | false | client order id

**Notice**:

orderId and clientOrderId, one of the two parameters must be entered.

## Cancel Orders(SIGNED)

Cancel futures orders by symbol

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": null
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/order/cancelOpenOrders`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
version | string | v1 | true | version, only v1 for now
symbol | string | BTCUSD | true | Futures symbol name


## Get Open Orders(SIGNED)

Get open orders 

> Response:

```json
{
	"code": 0, // Status code
	"msg": "success", //Message
	"i18nArgs": null,
	"data":{
		"list":[
			{
				"id": 1663004711982333952,// ID
                "clientOrderId":1000200000, // Client order id
           		"orderId": 1663004711982333952, // Order id
                "symbol": "BTCUSD",// Futures symbol name
                "displayName": "BTC-PERP", // Futures display name
                "qty": 1.00000000, // Order Quantity
                "remainQty": 1.00000000, // Unfilled Quantity
                "fillQty": 0E-8, // Filled Quantity
                "price": 500.00000000, // Price
                "avgPrice": 0E-8, // Avrage price
                "initMargin": 166.66666667,  // Initial Margin
                "tradeSide": 1,  // Trade side
                "tradeType": 1,  // Trade type
                "createTime": 1685326195118,// Time of the order created
                "reduceOnly": 0,  //Reduce only
                "leverage": 3,  //  Leverage
                "expression": null,  // Conditional Expression (GE -- Greater than or equal to, LE -- Less than or equal to)
                "triggerPrice": null  // Trigger Price
			}
		],
		"pageTotal":1,// Total Page Count
		"total":1 // Total Data Count
	}
}
```

**HTTP Request**

`GET https://api.coincall.com/open/futures/order/pending/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
page | number | 1 | false | Page number, default is 1
pageSize | number | 20 | false | Number of items per page, default is 20
symbol | string | BTCUSD | false | Filter data for a specific symbol

## Get Order Details(SIGNED)

Get futures order history

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": {
		"list": [{
			"clientOrderId":1000200000, // Client order id
			"orderId": 1665650442392174592,  // Order id
			"symbol": "XRPUSD",// Futures symbol name
			"displayName": "XRP-PERP",// Futures display name
			"qty": 1.00000000,  // Order Quantity
			"fillQty": 1.00000000, // Filled Quantity
			"price": 0.49110000,   // Price
			"avgPrice": 0.49110000, // Avrage price
			"fee": 0.00039288,  // Order transaction fee
			"rpnl": 0E-8, // Realized Pnl
			"tradeSide": 2, // Trade side
			"tradeType": 1, // Trade type
			"createTime": 1685956986404,// Time of the order created
			"state": 1, //Order Status
			"reduceOnly": 0, // Reduce only
			"leverage": 3, //Lleverage
			"expression": null,  // Conditional Expression (GE -- Greater than or equal to, LE -- Less than or equal to)
			"triggerPrice": null  // Trigger Price
		}],
		"hasNext": false, // Whether there is a next page
        "hasPre": false  // Whether there is a previous page
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/order/history/v1/{}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
pageSize | number | 10 | true | Number of items per page
fromId | number | 123123123 | false | Minimum orderId, can be obtained from the result field of the previous page when paging
startTime | number| 1686308840388 | false |  Start time of the history
endTime | number | 1686308840388 | false | End time of the history

## Get Transaction details(SIGNED)

Get futrues transaction history

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": {
		"list": [{
			"id": 1574775822713806849,// ID
			"contractId": null,// Contract ID
			"symbol": "ETHUSD",// Symbol
			"displayName": "ETH-PERP",// Display name
			"tradeSide": 1,// Trade side
			"tradeType": 1,// Trade type
			"price": 1389.00000000,// Price
			"qty": 1.00000000,// Quantity
			"markPrice": null,// Mark price
			"indexPrice": 1389.26000000,// Index Price
			"orderId": 1574775820017352705,// Order ID
			"tradeId": 1574775820805869568,// Trade ID
			"fee": 0.13890000,// Fees
			"time": 1664290788701,// Time of the transaction
			"leverage": 5, // Leverage
			"isTaker": 1 // Filled by taker side, 1 Taker 0 FALSE
		}],
		"hasNext": true, // Whether there is a next page
        "hasPre": false  // Whether there is a previous page
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/trade/history/v1/{}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
pageSize | number | 10 | false | Quantity per page
fromId | number | 123123123 | false | Minimum orderId, can be obtained from the result field of the previous page when paging
startTime | number| 1686308840388 | false |  Start time of the history
endTime | number | 1686308840388 | false | End time of the history