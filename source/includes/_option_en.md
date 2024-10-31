# Options Endpoint

## Get Option Instruments(SIGNED)

Get all option instruments information.

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": [{
		"baseCurrency": "BTC",
		"expirationTimestamp": 1694678400000,
		"strike": 22500.0,
		"symbolName": "BTCUSD-14SEP23-22500-C",
		"isActive": true,
		"minQty": 0.01,
		"tickSize": 0.1
	}, {
		"baseCurrency": "BTC",
		"expirationTimestamp": 1694678400000,
		"strike": 22500.0,
		"symbolName": "BTCUSD-14SEP23-22500-P",
		"isActive": true,
		"minQty": 0.01,
		"tickSize": 0.1
	}, {
		"baseCurrency": "BTC",
		"expirationTimestamp": 1694678400000,
		"strike": 23000.0,
		"symbolName": "BTCUSD-14SEP23-23000-C",
		"isActive": true,
		"minQty": 0.01,
		"tickSize": 0.1
	}, {
		"baseCurrency": "BTC",
		"expirationTimestamp": 1694678400000,
		"strike": 23000.0,
		"symbolName": "BTCUSD-14SEP23-23000-P",
		"isActive": true,
		"minQty": 0.01,
		"tickSize": 0.1
	}]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/getInstruments/{}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
baseCurrency | string | BTC | true | option base currency

## Get Option Chain(SIGNED)

Get option chain

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": [{
		"strike": 22000.00000000,// Strike price
		"callOption": {
			"optionId": 1584505132356345856,// Option ID
			"index": "BTCUSD",// Underlying symbol
			"symbol": "BTCUSD-26OCT22-22000-C",// Option symbol name
			"baseToken":"BTC",// Base token
			"displayName":"BTC-31MAY23-30000-C",// display name
			"endTime": 1666771200000,// Time of expiration
			"strike": 22000.00000000,// Strike price
			"lastPrice": 0,// Last price
			"markPrice": 0.0,// Mark price
			"volume": 0,// Trade volume
			"openInterest": 0,// Open interest
			"ask": 0,// Best ask price
			"askIv": 0.0,// Best ask IV
			"askSize": 0,// Best ask size
			"bid": 0,// Best bid price
			"bidIv": 0.0,// Best bid IV
			"bidSize": 0,// Best bid size
			"markIv": 0.0,// Mark price IV
			"type": 1,// Option type
			"lastPriceIv": 1.7976931348623157E308,// Last price IV
			"underlyingPrice": 20278.25,// Price of the underlying
			"breakeven": 30000,// Break-even Point
			"changeRate": -1.0000,// Price change in percentage
			"changePrice": -6.10000000,// Price change in value
			"userPosition":0,// User Holdings in position
			"delta": 0.0,// greeks delta
			"gamma": 0.0,// greeks gamma
			"vega": 0.0,// greeks vega
			"theta": 0.0,// greeks theta
			"rho":0 // greeks rho
		},
		"putOption": {
                "optionId": 1668166500983382054,
                "underlying": "BTCUSD",
                "symbol": "BTCUSD-15JUN23-26000-P",
                "baseToken": "BTC",
                "displayName": "BTC-15JUN23-26000-P",
                "endTime": 1686816000000,
                "strike": 26000.00000000,
                "lastPrice": 989.9,
                "markPrice": 1138.22770000,
                "volume": 8.95000000,
                "openInterest": 7.38000000,
                "ask": 0,
                "askIv": 0.01,
                "askSize": 0,
                "bid": 658.6,
                "bidIv": 0.01,
                "bidSize": 10.35,
                "markIv": 0.6292,
                "type": 2,
                "lastPriceIv": 1.0E-4,
                "underlyingPrice": 24861.7723,
                "breakeven": 24861.77230000,
                "changeRate": 0.2271,
                "changePrice": 199.53688859,
                "userPosition": 0,
                "delta": -1.0,
                "gamma": 0.0,
                "vega": 0.0,
                "theta": 0.0,
                "rho": -0.02421
            }
	}]
}
```

**HTTP Request**

`GET https://api.coincall.com/open/option/get/v1/{index}?endTime={endTime}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
endTime | long | 1666771200000 | true | Expiration time(timestamp)
index | string | BTCUSD | true | Underlying symbol

## Get Option Details(SIGNED)

Get option details

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",
	"i18nArgs": null,
	"data": {
		"optionId": 1584505132293431296,// Option ID
		"symbol": "BTCUSD-26OCT22-20000-P",// Option name
		"index":"BTCUSD",// Underlying Asset Name
        "displayName":"BTC-31MAY23-24000-C",// display name
		"endTime": 1666771200000,// Time of expiration
		"remainTime": 13565073,// Time remain until expiration
		"strike": 20000.00000000,// Strike price
		"markPrice": 10.231632230252217,// Mark price
		"underlyingPrice":27181.6936,// Underlying price
		"volume": 1.00000000,// Trade volume
		"volumeUsd": 1.00000000,// Trade value
		"openInterest": 0,// Open interest
		"lastPrice": 10.231632230252217,// Last price
		"premium": 0,// Premium
		"changeRate": 2.87,// Price change in percentage
		"changePrice":null,// Price change in value
		"iv": 0.58,// Implied volatility
		"multiplier":0.01,// Contract Multiplier
		"type": 2,// Option type
		"indexPrice": 20239.96000000,// Index price
		"price24hHigh": 0,// Highest price in 24hrs
		"price24hLow": 0,// Lowest price in 24hrs
		"volumeUsd24h": 0,// USD volume in 24hrs
		"price24hOpen": 18215.964000000,// Open price on UTC 00:00:00
		"volume24h": 0,// Trade volume in 24hrs
		"breakeven":27171.65,// Break-even Point
		"delta": -0.10808987585883545,// greeks delta
		"gamma": 0.0009475995953294489,// greeks gamma
		"vega": 0.7794498985827641,// greeks vega
		"theta": 0.0,// greeks theta
		"rho": -0.009454405809863273// greeks rho
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/detail/v1/{}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD-24MAY22-48000-P | true | option symbol name

## Get OrderBook(SIGNED)

Get option order book for 100 depth

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": {
		"optionName": "BTCUSD-26OCT22-15000-C",// Option name
		"displayName": null,
		"strike": 15000,// Strike price
		"bids": [{
			"size": "0.5",// Size
			"price": "5251"// Price
		}],
		"asks": [{
			"size": "1",// Size
			"price": "8888"// Price
		}]
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/order/orderbook/v1/{}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD-26OCT22-15000-C | true | Option Name 

## Get Last Trade(SIGNED)

Get option last trade

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": [
		{
			"symbol": "BTCUSD-26OCT22-20000-P",// Option symbol name
			"displayName":"BTC-26OCT22-20000-P",// Option display name
			"price": "10.3",// Trade price
			"qty": "1",// Trade Quantity
			"time": 1666757622819,// Trade time
			"tradeSide": 2// Trade side
		}
	]
}
```

**HTTP Request**

`GET https://api.coincall.com/open/option/trade/lasttrade/v1/{}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD-6JUN23-24000-C | true | Option Name 


## Get Positions(SIGNED)

Get All option positions

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": [{
		"id": 1584736851047620608,// ID
		"positionId": 1584736851047620609,// Position ID
		"updateTime": 1666665682934,// Update time
		"orderId": 1584736036348895232,// Order ID
		"userId": 1536933707941347382,// User ID
		"value": 11294.2000000000000000,// Position Value
		"qty": 1.00000000,// Position Quantity
		"initMargin": 0,// Initial Margin
		"maintMargin": 0,// Maintnance Margin
		"avgPrice": 11294.20000000,// Average Price
		"markPrice": 12260.310000000001,// Mark price
		"upnl": 966.11000000000100000000,// unRealized PnL
		"roi": 8.55403659,// Return on investment
		"rspl": 0E-8, // Realized PnL
		"symbol": "BTCUSD-25NOV22-8000-C",// Option symbol name
		"displayName": "BTC-25NOV22-8000-C",// Display name
		"tradeSide": 1,// Trade Side 1 BUY 2 SELL
		"lockQty": 0,// Lock Quantity
		"indexPrice": 12.22, // Index price
		"delta": 1.0,// greeks delta
		"gamma": 0.0,// greeks gamma
		"vega": 0.0,// greeks vega
		"theta": 0.0,// greeks theta
		"rho": 6.610892947742262,// greeks rho
		"baseToken": "BTC",// Base token
        "quoteToken": "USD" // Quote token
	}]
}
```

**HTTP Request**

`GET https://api.coincall.com/open/option/position/get/v1`

**Parameter**

Null

## Place Order(SIGNED)

Place an option order

> Response:

```json
{
    "code":0,
    "msg":"Success",
    "i18nArgs":null,
    "data":1663820914095300608 // Order id
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/order/create/v1`

**Rate Limit: 60/s**

**Parameter**


Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
clientOrderId | long | 123123123 | false | client order id
tradeSide | number | 1 | true | Trade Side, 1 BUY 2 SELL
tradeType | number | 1 | true | Trade Type, 1 LIMIT 3 POST_ONLY
symbol | string | BTCUSD-26OCT22-15000-C | true |  Option name
qty | number | 0.5 | true | Quantity 
price | number | 19000.01 | false | Price, required for limit orders
stp | integer | 1 | false | Value: [1,2,3]

<!-- reduceOnly | number | 1 | false | Reduce the position quantity only, 1 reduce only true, 0 reduce only false -->

Value | Name | Note |
--- | -------- | ---- |
1 | CM | Cancel Maker
2 | CT | Cancel Taker
3 | CB | Cancel Both


## Amend Order(SIGNED)

Modify unfilled or partially filled orders

> Response:

```json
{
    "code":0,
    "msg":"Success",
    "i18nArgs":null,
    "data":1663820914095300608 // Order id
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/order/modify/v1`

**Rate Limit: 60/s**

**Parameter**


Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
clientOrderId | long | 123123123 | false | client order id. Either orderId or clientOrderId is required
orderId | number | 1663820914095300000 | false | order id. Either orderId or clientOrderId is required
symbol | string | BTCUSD-26OCT22-15000-C | true |  Option symbol
qty | number | 0.5 | false | Order quantity after modification. Do not pass it if not modify the qty 
price | number | 19000.01 | false | Order price after modification. Do not pass it if not modify the price

**Notice**:

* The ack of amend order request indicates that the request is successfully accepted. Please use websocket order stream to confirm the order status

* You can only modify unfilled or partially filled orders.

* Do not support modify the `clientOrderId`.

* When the `qty` or `price` of a new order does not match order validation requirements, the modification will be rejected, and the original order will remain unchanged.

* If the original order is partially filled and the new order quantity is less than or equal to the executed quantity, the original order will be fully filled.

## Cancel Order(SIGNED)

Cancel an option order

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data":"success"
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/order/cancel/v1`

**Rate Limit: 60/s**

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
orderId | number | 1663820914095300608 | false | order id
clientOrderId | number | 123123123 | false | client order id

**Notice**:

orderId and clientOrderId, one of the two parameters must be entered.

## Cancel Orders(SIGNED)

Cancel option orders by index

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

`GET https://api.coincall.com/open/option/order/cancelOpenOrders/{version}/{index}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
version | string | v1 | true | version, only v1 for now
index | string | BTCUSD | true | coin index symbol name

## Cancel Orders by symbol(SIGNED)

Cancel option orders by symbol

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

`GET https://api.coincall.com/open/option/order/batchCancelByOption/v1/{symbol}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | KASUSD-31MAY24-0.1250-C | true | Options symbol name


## Get Open Orders(SIGNED)

Get option open orders

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": {
		"list":[
			{
				"id": 1665910350698258432,// ID
				"orderId": 1665910350698258432,// Order ID
				"clientOrderId": 123123123,// Client order id
				"symbol": "BTCUSD-6JUN23-24000-C",// Option symbol name
				"displayName":"BTC-6JUN23-24000-C",// Option display name
				"qty": 0.5,// Order Quantity
				"remainQty":0.5,// Unfilled Quantity
				"fillQty": 0,// Filled Quantity
				"price": 2095.6,// Price
				"avgPrice": null,// Average price
				"initMargin": 1047.8,// Initial Margin
				"tradeSide": 1,// Trade side
				"tradeType": 1,// Trade type
				"createTime": 1666667584739,// Time of the order created
				"reduceOnly": 0, // Reduce only
				"indexPrice": 25782.815 // Index Price
			}
		],
		"pageTotal":1,// Total Page Count
		"total":1 // Total Data Count
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/order/pending/v1/{}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
page | number | 1 | false | Page number, default is 1
pageSize | number | 20 | false | Number of items per page, default is 20, maximum value is 500
currency | string | BTC | false | Filter data for a specific currency

## Get Order Info(SIGNED)

Get an order information by orderId or clientOrderId

> Response:

```json
{
	"code": 0, // Status code
	"msg": "success", //Message
	"i18nArgs": null,
	"data":{
		{
			"orderId": 1665910350698258432,// Order ID
			"clientOrderId": 123123123,// Client order id
			"symbol": "BTCUSD-6JUN23-24000-C",// Option symbol name
			"displayName":"BTC-6JUN23-24000-C",// Option display name
			"qty": 0.5,// Order Quantity
			"remainQty":0.5,// Unfilled Quantity
			"fillQty": 0,// Filled Quantity
			"price": 2095.6,// Price
			"avgPrice": null,// Average price
			"tradeSide": 1,// Trade side
			"tradeType": 1,// Trade type
			"createTime": 1666667584739,// Time of the order created
			"reduceOnly": 0, // Reduce only
			"fee": 0, // transaction fee(accumulated)
			"updateTime": 1685326195118,
			"state": 0 // order status
		}
	}
}
```

**HTTP Request**

`GET https://api.coincall.com/open/option/order/singleQuery/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
orderId | number | 111 | false | query string
clientOrderId | number | 123123123 | false | client order id

**Notice**:

orderId and clientOrderId, one of the two parameters must be entered.

## Get Order Details(SIGNED)

Get Option Order History

> Response:

```json
{
    "code": 0,// Status code
	"msg": "Success",// Message
    "i18nArgs":null,
    "data":{
        "list":[
            {
                "orderId": 1665650442392174592, // Order ID
				"clientOrderId": 1665650442392174592,// Client order id
                "symbol": "BTCUSD-25NOV22-8000-C", // Option symbol name
                "displayName": "BTC-25NOV22-8000-C", // Display name
                "qty": 1.00000000, // Order Quantity
                "fillQty": 1.00000000, // Filled Quantity
                "price": 0.49110000, // Order Price
                "avgPrice": 0.49110000, // Average price
                "fee":0.22, // fee
                "rpnl":0.22, // Realized PnL 
                "tradeSide": 1, // Trade side
                "tradeType": 1, // Trade type
                "createTime": 1666667584739,// Time of the order created
                "state": 1, // Order status
                "reduceOnly": 0 // Reduce only
            }
        ],
        "hasNext": false, // Whether there is a next page
        "hasPre": false  // Whether there is a previous page
    }
}
```



**HTTP Request**

`GET https://api.coincall.com/open/option/order/history/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
pageSize | number | 20 | true | Number of items per page, default is 20, maximum value is 500
fromId | number | 123123123 | false | Minimum orderId, can be obtained from the result field of the previous page when paging
startTime | number| 1686308840388 | false |  Start time of the history, default is the current time pushed forward by 24 hours
endTime | number | 1686308840388 | false | End time of the history


## Get Transaction Details(SIGNED)

Get option transaction history

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": {
		"list": [
			{
				"id": 1584745240079241216,// ID
				"optionId": null,// Option ID
				"symbol":"BTCUSD-2JUN23-18000-C",// Option symbol name
				"displayName":"BTC-2JUN23-18000-C",// Option display name
				"tradeSide": 1,// Trade side
				"tradeType": 1,// Trade type
				"price": 951.00000000,// Price
				"qty": 2.00000000,// Quantity
				"iv": 0.5606,// Implied Volatility
				"markPrice": 1419.5139928388217,// Mark price
				"indexPrice": 20247.0,// Index price
				"orderId": 1584744827800133632,// Order ID
				"tradeId": 1584745239911469056,// Trade ID
				"fee": 0.00190200,// Fees
				"time": 1666667683034,// Transaction time
				"reduceOnly":0, // Reduce only
				"isTaker":0 // Filled by taker side
			}
		],
		"hasNext": true, // Whether there is a next page
        "hasPre": false  // Whether there is a previous page
	}
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/trade/history/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
pageSize | number | 20 | false | Number of items per page, default is 20, maximum value is 500
fromId | number | 123123123 | false | Minimum tradeId, can be obtained from the result field of the previous page when paging
startTime | number| 1686308840388 | false |  Start time of the history
endTime | number | 1686308840388 | false | End time of the history