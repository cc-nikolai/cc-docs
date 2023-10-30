# Spot Endpoint

## Get Instruments(SIGNED)

Query for the instrument specification of online trading pairs.

> Response:

```json
{
	"code": 0,
	"msg": "success",
	"i18nArgs": null,
	"data": {
		"symbol": "TRXUSDT", // Symbol name
		"baseCoin": "TRX", // Base coin
		"quoteCoin": "USDT", // Quote coin
		"enableTrading": 1, // Enable trade, 1 TRUE 0 FALSE
		"lotSizeFilter": {
			"basePrecision": "0", // The precision of base coin
			"quotePrecision": "2", // The precision of quote coin
			"maxOrderSize": 10, // Maximum order size
			"minQty": "1", // Minimum order quantity
			"maxQty": "10000000", // Maximum order quantity
			"maxMarketQty": "5000000" // Maximum market order quantity
		},
		"priceFilter": {
			"tickSize": "0.00001" // The step to increase/reduce order price
		}
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/market/instruments`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | false | Symbol name
limit | integer | 1 | false | Limit for data size per page. [1, 1000]. Default: 500

## Kline(SIGNED)

Query for historical klines (also known as candles/candlesticks)

> Response:

```json
{
	"code": 0,
	"msg": "success",
	"i18nArgs": null,
	"data": [{
		"endTime": 1697087280000, // Close Time
		"open": 0.4684, // Open price
		"close": 0.0, // Close price
		"low": 0.4684, // Lowest price
		"high": 0.4684, // Highest price
		"volume": 0.0, // Trade volume
		"volumeUsd": 0.0 // Trade volume in USD
	}]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/market/klines`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | true | Symbol name
interval | string | 1min | true | Kline interval.
start | integer | 1698202825192 | false | The start timestamp (ms)
end | integer | 1698202825192 | false | The end timestamp (ms)
limit | integer | 1 | false | Limit for data size per page. [1, 1000]. Default: 200

## Get Orderbook(SIGNED)

Query for orderbook depth data.

> Response:

```json
{
	"code": 0,
	"msg": "success",
	"i18nArgs": null,
	"data": {
		"s": "XRPUSDT", // Symbol name
		"b": [ // Bid, buyer. Sort by price desc
			[0.5459, 22.0] // price, size
		],
		"a": [ // Ask, seller. Order by price asc
			[0.5479, 132.0]
		],
		"ts": 1698202825192, // The timestamp (ms) that the system generates the data
		"u": 7144136 // Update ID, is always in sequence
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/market/orderbook`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | true | Symbol name
depth | integer | 1 | false | Limit size for each bid and ask, [ 1, 10, 20, 50, 100,200] Default: 1.

## Get Public Trading History(SIGNED)

Query recent public trading data.

> Response:

```json
{
	"code": 0,
	"msg": "success",
	"i18nArgs": null,
	"data": [{
		"tradeId": "714412239621107665563948", // trade ID
		"symbol": "XRPUSDT", // Symbol name
		"price": 0.5479, // Trade price
		"qty": 1.0, // Trade quantity
		"side": 1, // Side of taker `Buy` 1, `Sell` 2
		"ts": 1698148006763 // Trade time (ms)
	}]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/market/histories`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | true | Symbol name
limit | integer | 1 | false | Limit for data size per page.spot: [ 1, 100], default: 1

## Get Tickers 24hr(SIGNED)

Query for the latest price snapshot, best bid/ask price, and trading volume in the last 24 hours.

> Response:

```json
{
	"code": 0,
	"msg": "success",
	"i18nArgs": null,
	"data": {
		"s": "XRPUSDT", // Symbol name
		"base": "XRP", // Base coin
		"quote": "USDT", // Quote coin
		"o": 0.53, // Open price
		"h": 0.5605, // The highest price in the last 24 hours
		"l": 0.53, // The lowest price in the last 24 hours
		"c": 0.5479, // Close price
		"a": 82023.0, // Amount
		"v": 44828.4405, // Volume for 24h
		"i": 0.55363524, // indexprice
		"cp": 0.017900000000000027, // Price change in value
		"r": 0.033773584905660424, // Price change in percentage
		"hasOption": false // Whether there are options
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/market/overviewV2`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | false | Symbol name

## Place Order(SIGNED)

Create a new order.

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": 42953967928017000 // Order ID
}
```


**HTTP Request**

`POST https://api.coincall.com/open/spot/trade/order/v1`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | true | Symbol name
clientOrderId | string | abc123 | false | Client order id
tradeSide | string | 1 |  true | `1` BUY `2` SELL
tradeType | string | 1 | true | `1` LIMIT,`2` MARKET,`3` POST_ONLY
qty | string | 1 | false | Order quantity. 
price | string | 0.53 | false | Order price.


Type | Additional mandatory parameters
LIMIT, POST_ONLY | qty, price
MARKET | qty

## Cancel Order(SIGNED)

Cancel an open order.

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": true
}
```


**HTTP Request**

`POST https://api.coincall.com/open/spot/market/cancel/v1`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
orderId | string | 1321003749386327552 | false | Order ID. Either orderId or clientOrderId is required
clientOrderId | string | abc123 | false | User customized order ID. Either orderId or clientOrderId is required

## Cancel Orders(SIGNED)

Cancels all active orders on one symbol.

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": true
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/trade/cancelAll/v1`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | true | Symbol name

## Query Order(SIGNED)

Check an order's status.

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": {
		"id": 320295,
		"clientOrderId": "42953967928017000", // User customised order ID
		"orderId": 42953967928017000, // Order ID
		"userId": 8098448373, // User ID
		"symbol": "XRPUSDT", // Symbol name
		"displaySymbol": "XRP/USDT", // Symbol Display name
		"price": "0.566", // Order price
		"avgPrice": "0.5479", // Average trade price
		"qty": "1", // Order quantity
		"fillQty": "1", // Trade quantity
		"remainQty": "0", // Remain quantity
		"status": 1, // Order status
		"tradeSide": 1, // Trade side
		"tradeType": 2, // Trade Type 
		"fee": "0.0001", // Transaction fee(accumulated)
		"feeCurrency": "XRP", // Fee charged in
		"ts": 1698208992286, // Order created timestamp (ms)
		"updateTime": 1698208992345 // Order updated timestamp (ms)
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/trade/order/v1`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
orderId | string | 1321003749386327552 | false | Order ID. Either orderId or clientOrderId is required
clientOrderId | string | abc123 | false | User customized order ID. Either orderId or clientOrderId is required

## Query Open Orders(SIGNED)

Get all open orders.

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": [{
		"id": 320307,
		"clientOrderId": "42953967928017012", // User customised order ID
		"orderId": 42953967928017012, // Order ID
		"userId": 8098448373, // User ID
		"symbol": "XRPUSDT", // Symbol name
		"displaySymbol": "XRP/USDT", // Symbol display name
		"price": "0.5446", // Trade price
		"avgPrice": "0", // Average trade price
		"qty": "1", // Order quantity
		"fillQty": "0", // Trade quantity
		"remainQty": "1", // Remain quantity
		"status": 0, // Order status
		"tradeSide": 1, // Trade side
		"tradeType": 1, // Trade Type
		"fee": "0", // Transaction fee(accumulated)
		"feeCurrency": null, // Fee charged in
		"ts": 1698215274894, // Order created timestamp (ms)
		"updateTime": 1698215274950 // Order updated timestamp (ms)
	}]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/trade/orders/v1`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | false | Symbol name

## Query All Orders(SIGNED)

Get all orders; active, canceled, or filled.

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": [{
		"id": 320307,
		"clientOrderId": "42953967928017012", // User customised order ID
		"orderId": 42953967928017012, // Order ID
		"userId": 8098448373, // User ID
		"symbol": "XRPUSDT", // Symbol name
		"displaySymbol": "XRP/USDT", // Symbol display name
		"price": "0.5446", // Trade price
		"avgPrice": "0", // Average trade price
		"qty": "1", // Order quantity
		"fillQty": "0", // Trade quantity
		"remainQty": "1", // Remain quantity
		"status": 0, // Order status
		"tradeSide": 1, // Trade side
		"tradeType": 1, // Trade Type
		"fee": "0", // Transaction fee(accumulated)
		"feeCurrency": null, // Fee charged in
		"ts": 1698215274894, // Order created timestamp (ms)
		"updateTime": 1698215274950 // Order updated timestamp (ms)
	}]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/trade/allorders/v1`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | false | Symbol name
limit | integer | false | Limit for data size per page. [1, 1000]. Default: 500
startTime | integer | 1698202825192 | false | The start timestamp (ms)
endTime | integer | 1698202825192 | false | The end timestamp (ms)

## Query Fill List(SIGNED)

Get fills trade list.

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": [{
		"id": 20598,
		"clientOrderId": "42953967928017002", // User customised order ID
		"orderId": 42953967928017002, // Order ID
		"tradeId": "714414039621107665563948", // Trade ID
		"userId": 8098448373, // User ID
		"symbol": "XRPUSDT", // Symbol name
		"displaySymbol": "XRP/USDT", // Symbol display name
		"tradeSide": 1, // Trade side
		"price": "0.5479", // Order price
		"qty": "1", // Order quantity
		"isTaker": 1, // Filled by taker side, `1` Taker `0` FALSE
		"fee": "0.0001", // Transaction fee(accumulated)
		"feeCurrency": "XRP", // Fee charged in
		"ts": 1698209660112, // Order created timestamp (ms)
		"updateTime": 1698209660112 // Order updated timestamp (ms)
	}]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/spot/trade/fills/v1`


**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | TRXUSDT | false | Symbol name
orderId | number | 42953967928017012 | false | Order ID
limit | integer | false | Limit for data size per page. [1, 1000]. Default: 500
startTime | integer | 1698202825192 | false | The start timestamp (ms)
endTime | integer | 1698202825192 | false | The end timestamp (ms)

