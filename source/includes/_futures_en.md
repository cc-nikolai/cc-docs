# Futures Endpoint

## Get instruments

Get futures instruments

> Response:

```json
{
    "code":0,
    "msg":"Success",
    "i18nArgs":null,
    "data":[
        {
            "ticker_id":"BTC-USD", // symbol id
            "base_currency":"BTC",
            "quote_currency":"USD",
            "last_price":"42782.00000000",
            "base_volume":"2485.862", // 24 hour trading volume in BASE currency
            "usd_volume":"106351139.55450000", // 24 hour trading volume in USD
            "quote_volume":"106351139.55450000", // 24 hour trading volume in QUOTE currency
            "bid":"42777.9", // Current highest bid price
            "ask":"42779.6", // Current lowest ask price
            "high":"43849.6", // Rolling 24-hour highest transaction price
            "low":"42549.2", // Rolling 24-hour lowest transaction price
            "product_type":"Perpetual",
            "open_interest":"9.35800000",
            "open_interest_usd":"400346.61622638",
            "index_price":"42751.48738636", // Last calculated index price for underlying of contract
            "funding_rate":"0.00016736", // Current funding rate
            "next_funding_rate":"0.00016736", // Upcoming predicted funding rate
            "next_funding_rate_timestamp":1703606400000, // Timestamp of the next funding rate change
            "contract_type":"Vanilla",
            "contract_price":"42782.00000000",
            "contract_price_currency":"USD"
        },
		{...}]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/market/instruments/v1`


**Parameter**

Null

## Get OrderBook

 Get futures order book
 
> Request:

```json

curl -X GET 
-H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU=" 
-H "sign: DDD580BDF67B2CE93FACA962C96716D425FE878652A22A92CDDBFF39971584D1" 
-H "ts: 1745918318045" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " "https://beta.seizeyouralpha.com/open/futures/market/orderbook?symbol=BTC-USD"

```

> Response:

```json
{
    "code":0,
    "msg":"Success",
    "i18nArgs":null,
    "data":{
        "symbol":"BTC-USD", // symbol id
        "bids":[ // // Bid, buyer. Sort by price desc
            [
                "42759.1", // price
                "0.568" // size
            ] 
        ],
        "asks":[ // Ask, seller. Order by price asc
            [
                "42761.2",
                "2.94"
            ]
        ],
        "timestamp":1703579842559 // // The timestamp (ms) that the system generates the data
    }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/market/orderbook`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTC-USD | true | Symbol name
depth | Integer | 1 | false | Limit size for each bid and ask, [ 1, 10, 20, 50, 100] Default: 1.

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

## Get Fixed Depth OrderBook 

 Get futures order book for 150 depth

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

`GET https://api.coincall.com/open/futures/order/orderbook/v1/{symbol}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | Symbol name

## Kline

Query for historical klines (also known as candles/candlesticks)

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": [{
			"open": 27437.30000000, // Open price
			"close": 27435.10000000, // Close price
			"low": 27435.10000000, // Lowest price
			"high": 27437.30000000, // Highest price
			"volume": 14.24300000, // Trade volume
			"time": 1693526400000, // Start time of this line (ms)
			"period": "D1" // period
		},
		{
			"open": 27435.10000000,
			"close": 27434.90000000,
			"low": 27434.90000000,
			"high": 27435.10000000,
			"volume": 0.00300000,
			"time": 1693612800000,
			"period": "D1"
		}
	]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/market/kline/history/v2/{symbol}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | Symbol name
period | string | D1 | true | granularity of K-line
start | integer | 1697760509000 | true | Start time(ms)
end | integer | 1697771549000 | true | End time(ms)
limit | integer | 1 | true | Please make sure limit=1.

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

## Get leverage(SIGNED)

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

## Set Leverage(SIGNED)

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

**Rate Limit: 60/s**

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
clientOrderId | long | 123123123 | false | client order id
symbol | string | BTCUSD | true | Futures Symbol 
price | number | 19000.01 | false | Price, required for limit orders
qty | number | 0.5 | true | Quantity 
tradeSide | number | 1 | true | Trade Side, 1 BUY 2 SELL
tradeType | number | 1 | true | Trade Type, 1 LIMIT 2 MARKET 3 POST_ONLY 4 STOP_LIMIT 5 STOP_MARKET
timeInForce | string | GTC | false | IOC, FOK. default: GTC
stp | integer | 1 | false | Value: [0,1,2,3], Default is 0 (No stp strategy is used).
reduceOnly | number | 1 | false | Reduce the position quantity only, 1 reduce only true, 0 reduce only false
triggerPrice | number | 18000.01 | false | The trigger price when tradeType is 4 (STOP_LIMIT) or 5 (STOP_MARKET)
*Time in force (timeInForce):*

Name | Note
---- | ----
GTC  | Good Till Cancel
IOC  | Immediate or Cancel
FOK  | Fill or Kill

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

**Rate Limit: 60/s**

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

`GET https://api.coincall.com/open/futures/order/cancelOpenOrders/{version}/{symbol}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
version | string | v1 | true | version, only v1 for now
symbol | string | BTCUSD | true | Futures symbol name

## Batch Cancel Order(SIGNED)

Cancel batch Orders by ids

> Request:

```sh
curl -X POST 
-H "sign:3260D3D58F2982B9E3982D2BD51B0CF18E153B6F35686DE30ACA1A267925C832" 
-H "X-REQ-TS-DIFF:12" 
-H "x-cc-apikey:mtQ/qQcbFnccSV061nGvWC1Ni9lXf4sBw36NAaDsKMs=" 
-H "ts:1730337237761" 
-H "Content-Type:application/json; charset=utf-8" 
-H "Content-Length:79" 
-H "Host:api.coincall.com" 
-H "Connection:Keep-Alive" 
-d '{"clientOrderIdList":[2215534552962207610],"orderIdList":[2215534552962207611]}' "https://api.coincall.com/open/futures/order/batchCancel/v1"
```

> Response:

```json
{
        "code": 0,
        "msg": "Success",
        "i18nArgs": null,
        "data": [{
                "clOrdId": 2215534552962207610, // client order id
                "ordId": 2215534552962207611, // order id
                "ts": 1730337238487, 
                "scode": 0, // 0 success, 1 failed
                "smsg": null
        }]
}
```


**HTTP Request**

`POST https://api.coincall.com/open/futures/order/batchCancel/v1`

**Parameter**

Name | Type | Required | Note
---- | ---- | -------- | ----
orderIdList | list | false | orderId list
clientOrderIdList | list | false | clientOrderId list

**Notice**:

* Either `orderIdList` or `clientOrderIdList` is required. If both are provided, priority will be given to the `orderIdList`.
* You can cancel unfilled or partially filled orders.
* The ack of cancel order request indicates that the request is successfully accepted. Please use websocket order stream to confirm the order status


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
                "avgPrice": 0E-8, // Average price
                "initMargin": 166.66666667,  // Initial Margin
                "tradeSide": 1,  // Trade side
                "tradeType": 1,  // Trade type
                "createTime": 1685326195118,// Time of the order created
                "reduceOnly": 0,  //Reduce only
                "leverage": 3,  //  Leverage
                "expression": null,  // Conditional Expression (GE -- Greater than or equal to, LE -- Less than or equal to)
                "triggerPrice": null,  // Trigger Price
				"timeInForce": "IOC"
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
			"clientOrderId":1000200000, // Client order id
			"orderId": 1663004711982333952, // Order id
			"symbol": "BTCUSD",// Futures symbol name
			"displayName": "BTC-PERP", // Futures display name
			"qty": 1.00000000, // Order Quantity
			"remainQty": 1.00000000, // Unfilled Quantity
			"fillQty": 0E-8, // Filled Quantity
			"price": 500.00000000, // Price
			"avgPrice": 0E-8, // Average price
			"tradeSide": 1,  // Trade side
			"tradeType": 1,  // Trade type
			"createTime": 1685326195118,// Time of the order created
			"reduceOnly": 0,  //Reduce only
			"leverage": 3,  //  Leverage
			"fee": 0, // transaction fee(accumulated)
			"updateTime": 1685326195118,
			"state": 0, // order status
			"timeInForce": "IOC"
		}
	}
}
```

**HTTP Request**

`GET https://api.coincall.com/open/futures/order/singleQuery/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
orderId | number | 111 | false | query string
clientOrderId | number | 123123123 | false | client order id

**Notice**:

orderId and clientOrderId, one of the two parameters must be entered.

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
			"avgPrice": 0.49110000, // Average price
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

`GET https://api.coincall.com/open/futures/order/history/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
pageSize | number | 10 | true | Number of items per page
fromId | number | 123123123 | false | Minimum orderId, can be obtained from the result field of the previous page when paging
startTime | number| 1686308840388 | false |  Start time of the history, default is the current time pushed forward by 24 hours
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

`GET https://api.coincall.com/open/futures/trade/history/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
pageSize | number | 10 | false | Quantity per page
fromId | number | 123123123 | false | Minimum orderId, can be obtained from the result field of the previous page when paging
startTime | number| 1686308840388 | false |  Start time of the history
endTime | number | 1686308840388 | false | End time of the history

## Get Funding Rate Details(SIGNED)

Get Funding Rate History

> Response:

```json
{
    "code": 0,
    "msg": "success",
    "i18nArgs": null,
    "data": {
        "list": [
            {
                "id": 379372,
                "symbol": "TONUSD",
                "displayName": "TONUSDT Perp",
                "tradeSide": 1,
                "qty": 2.00000000,
                "fundFee": -0.00114441,
                "fundRate": 0.00010000,
                "ctime": 1730160005432
            },
            {
                "id": 379361,
                "symbol": "TRXUSD",
                "displayName": "TRXUSDT Perp",
                "tradeSide": 2,
                "qty": 2.00000000,
                "fundFee": 0.00002432,
                "fundRate": 0.00010000,
                "ctime": 1730160004652
            },
            {
                "id": 379270,
                "symbol": "TONUSD",
                "displayName": "TONUSDT Perp",
                "tradeSide": 1,
                "qty": 2.00000000,
                "fundFee": -0.00114441,
                "fundRate": 0.00010000,
                "ctime": 1730131205546
            },
            {
                "id": 379259,
                "symbol": "TRXUSD",
                "displayName": "TRXUSDT Perp",
                "tradeSide": 2,
                "qty": 2.00000000,
                "fundFee": 0.00002432,
                "fundRate": 0.00010000,
                "ctime": 1730131204634
            }
        ],
        "pageTotal": 1,
        "total": 4
    }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/settle/future/record/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | futures symbol name
startTime | number| 1686308840388 | false | Start time of the history
endTime | number | 1686308840388 | false | End time of the history
pageSize | number | 20 | false | Number of items per page, default is 20, maximum value is 50
page | number | 1 | false | default is 1




## Get Funding Rate latest Details(SIGNED)

Get the latest funding rate settlement records. 

> Request:

```json

curl -X GET 
-H "X-CC-APIKEY: elYSEjC7KJw+CFJU9TqTpdh0m5/wTgJAVB6YnMy4b20=" 
-H "sign: 311CB0E4C91BE42448CE61F4E558341EDAFF8BD9917B85AE3FE9C1E6BB1983D9" 
-H "ts: 1753786530992" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " "https://beta.seizeyouralpha.com/open/settle/future/latestRecord/v1?symbol=BTCUSD&startTime=1663490353000"

```

> Response:

```json
{
  "code": 0,
  "msg": null,
  "i18nArgs": null,
  "data": {
    "list": [
      {
        "id": 543666,
        "symbol": "BTCUSD",
        "displayName": "BTCUSDT Perp",
        "tradeSide": 2,
        "qty": 1,
        "fundFee": -0.05101865,
        "fundRate": -5.4e-7,
        "ctime": 1746604800015
      },
      {
        "id": 543468,
        "symbol": "BTCUSD",
        "displayName": "BTCUSDT Perp",
        "tradeSide": 2,
        "qty": 1,
        "fundFee": 1.08174426,
        "fundRate": 0.00001145,
        "ctime": 1746576000018
      },
      {
        "id": 543217,
        "symbol": "BTCUSD",
        "displayName": "BTCUSDT Perp",
        "tradeSide": 2,
        "qty": 1,
        "fundFee": 0.69439478,
        "fundRate": 0.00000735,
        "ctime": 1746547200022
      },
      {
        "id": 542966,
        "symbol": "BTCUSD",
        "displayName": "BTCUSDT Perp",
        "tradeSide": 2,
        "qty": 1,
        "fundFee": 4.21927528,
        "fundRate": 0.00004466,
        "ctime": 1746518400032
      },
      {
        "id": 542715,
        "symbol": "BTCUSD",
        "displayName": "BTCUSDT Perp",
        "tradeSide": 2,
        "qty": 1,
        "fundFee": 1.67909,
        "fundRate": 0.00002023,
        "ctime": 1746489600029
      },
      {
        "id": 542412,
        "symbol": "BTCUSD",
        "displayName": "BTCUSDT Perp",
        "tradeSide": 2,
        "qty": 1,
        "fundFee": -1.86501,
        "fundRate": -0.00002247,
        "ctime": 1746460800012
      }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/settle/future/latestRecord/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | false | futures symbol name
startTime | number| 1663490353000 | false | Start time of the records

**Parameter Description**  

*  If the symbol is empty, query the records for all symbols.    
*  If startTime is empty, the query will use the time point 8 hours ago as the startTime (startTime = currentTimeMillis - 8 * 60 * 60 * 1000).
*  The maximum query range is 24 hours (startTime must be greater than currentTimeMillis - 24 * 60 * 60 * 1000)
 

## Get Settlement Record (SIGNED)

Query delivery future Settlement history 


> Rquest: 

```json
curl -X GET 
-H "X-CC-APIKEY: rKhWnvo/KR3yXtCmaNNf6NxORXBAyOC24TnQzx0P7yY=" 
-H "sign: F8F430FAA1E01A64FFC5A5AE4A37CDCFCD1A14CBBBD8305644405F76C7DCF478" 
-H "ts: 1750326740785" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " "https://beta.seizeyouralpha.com/open/futures/delivery/settlement/history/v1?startTime=1663490353000&endTime=1663500353000&page=1&pageSize=20&symbol=BTCUSD"

```


> Response:

```json
{
    "code": 0,
    "msg": "Success",
    "i18nArgs": null,
    "data": {
        "list": [
            {
                "symbol": "BTCUSD",    //futures name
                "time": 1726248852785, //create time
                "qty": 2.00000000,     //Position  quantity
                "tradeSide": 2,        // Trade Side, 1 BUY 2 SELL
                "entryPrice": 12200.00000000,  //entry price 
                "settlementPrice": 12409.38569142,  //settlement price 
                "settlementPnL": -418.77138284,   //Profit and Loss
                "fees": 0.72317826     //Trading Fee
            }
        ],
        "pageTotal": 1,
        "total": 1
    }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/delivery/settlement/history/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | false | future symbol name
startTime | number| 1686308840388 | false | Start time of the history
endTime | number | 1686308850388 | false | End time of the history
page | number | 1 | false | default is 1
pageSize | number | 20 | false | Number of items per page, default is 20, maximum value is 50



## Get Premium Index history Records (SIGNED)

 Query premium index history records


> Rquest: 

```json 

curl -X GET 
-H "X-CC-APIKEY: Ipl6mkcZxxE3ESvPMYUJYJ9JY81myuefEpKDelht77k=" 
-H "sign: 4E3EDCF9A7E0EE0F26A2ED93FBCEEEE8393BB5B10F5EE04E9442242BDFDBA4E9" 
-H "ts: 1761881198823" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " "https://beta.seizeyouralpha.com/open/futures/market/premiumIndexHistory/v1?symbol=BTCUSD&pageSize=5"

```


> Response:

```json
{
  "code": 0,
  "msg": "success",
  "data": {
    "records": [
      {
        "symbol": "BTCUSD",
        "premiumIndex": "0.0042492700000000",
        "fundingRate": "0.0030000000000000",
        "minute": "2025-10-31 03:26"
      },
      {
        "symbol": "BTCUSD",
        "premiumIndex": "0.0042492700000000",
        "fundingRate": "0.0030000000000000",
        "minute": "2025-10-31 03:25"
      },
      {
        "symbol": "BTCUSD",
        "premiumIndex": "0.0042492700000000",
        "fundingRate": "0.0030000000000000",
        "minute": "2025-10-31 03:24"
      },
      {
        "symbol": "BTCUSD",
        "premiumIndex": "0.0042492700000000",
        "fundingRate": "0.0030000000000000",
        "minute": "2025-10-31 03:23"
      },
      {
        "symbol": "BTCUSD",
        "premiumIndex": "0.0042492700000000",
        "fundingRate": "0.0030000000000000",
        "minute": "2025-10-31 03:22"
      }
    ],
    "total": 1438,
    "size": 5,
    "current": 1,
    "pages": 288,
    "hasNext": true,
    "hasPrevious": false
  }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/futures/market/premiumIndexHistory/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | future symbol name
startTime | number| 1686308840388 | false | Start time of the history records
endTime | number | 1686308840388 | false | End time of the history records
page | number | 1 | false | default is 1
pageSize | number | 60 | false | Number of items per page, default is 60, miniumm value is 1, maximum value is 200

**Parameter Description**  

*  If startTime is empty, the query will use the time point 24 hours ago as the startTime (startTime = currentTimeMillis - 24 * 60 * 60 * 1000).
*  If endTime is empty, the query will use the current time point  as the endTime
*  The maximum query range is 24 hours (endTime - startTime must be greater than 24 * 60 * 60 * 1000)


