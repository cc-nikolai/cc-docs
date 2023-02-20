# Futures Endpoints

## Get Futures Symbol

```shell
curl "http://api.coincall.com/open/futures/market/symbol/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getFuturesSymbol()
```


```python
import coincall

api = coincall.authorize('key','secret')
api.futures.getSymbol()
```


```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let positions = api.futures.getSymbol();
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": [{
		"contractId": 1,// Contract ID
		"symbol": "BTCUSD",// Symbol
		"symbolName": "BTC-PERP",// Symbol name
		"price": 20260.31,// Price
		"changeRate": 0,// Change in percentage
		"changeVolume": 0,// Change in value
		"markPrice": 18898.4293759300000000,// Mark price
		"indexPrice": 20260.31,// Index Price
		"price24hHigh": 0,// Highest price in 24hrs
		"price24hLow": 0,// Lowest price in 24hrs
		"volumeUsd24h": 0,// USD volume in 24hrs
		"volume24h": 0,// Volume in 24hrs
		"ts": null,// Timestamp
		"price24hOpen": 18234.279// Open price on UTC 00:00:00
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/market/symbol/v1`

<aside class="notice">
   Get futures symbol
</aside>

**header**

name  | value  | Required | Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

Null


## Get Futures Position 

```shell
curl "http://api.coincall.com/open/futures/position/get/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getFuturesPosition()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.futures.getPosition(123)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let positions = api.futures.getPosition(123);
``` -->

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
      "value": 176.7825,// Value
      "volume": 0.009,// Volume
      "initMargin": 35.3565,// Initial margin
      "maintMargin": 1.767825,// Maintnance margin
      "avgPrice": 19642.5,// Average price
      "markPrice": 18900.38311437,// Mark price
      "elp": null,// Estimated liquidation price
      "pnl": 0,// Realized PnL
      "roi": -0.03778118,// ROI
      "rspl": 0,//
      "unpl": -6.67905197067,// Unrealized Pnl
      "symbol": "BTCUSD",//symbol
      "tradeSide": 1,// Trade side 1 BUY  2 SELL
      "tradeType": null,// Trade type 1 LIMIT 2 MARKET  
      "lockVolume": 0,// Lock volume
      "leverage": 5,// Leverage
      "delta": 0.009// Position delta
    }
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/position/get/v1`

<aside class="notice">
   Get futures positions (SIGNED)----Signature required
</aside>

**header**

name  | value  | Required | Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

Null

## Place Futures Order

```shell
curl "http://api.coincall.com/open/futures/order/create/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -D {}
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.placeFuturesOrder(param)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.futures.placeOrder(10)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.futures.placeOrder();
``` -->

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": null
}
```


### HTTP Request

`POST http://api.coincall.com/open/futures/order/create/v1`

<aside class="notice">
    Place futures orders(SIGNED)----Signature required
</aside>

**header**

name  | value  | Required  | Note
-------------- | -------------- | -------------- | ----
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true |
sign | xxx | true | Endpoint Signature

**Parameter**

name  | value  | Required | Note
-------------- | -------------- | -------------- | -------
symbol | BTCUSD | true | Futures Symbol 
price | 19000 | false | Price required for limit orders
volume| 0.5 | true | Quantity of the order 
tradeSide | 1 | true | Trader side：1 buy, 2 sell
tradeType | 1 | true | Trade type：1 limit, 2 market
isClose | 1 | true | Clarify if the order is a close order 




## Cancel Futures Order

```shell
curl "http://api.coincall.com/open/option/order/cancel/v1/{orderId}" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.cancelFuturesOrder(orderId)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.futures.cancelOrder(123)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.futures.cancelOrder(123);
``` -->

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": null
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/order/cancel/v1/{orderId}`

<aside class="notice">
   Cancel futures order(SIGNED)----Signature required
</aside>

**header**

name  | value  | Required | Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

name | value | true否必填 | 说明
-------------- | -------------- | -------------- | --------------
orderId | 111 | true | query string


## Get Futures Open Orders

```shell
curl "http://api.coincall.com/open/futures/order/pending/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getFuturesPendingOrder()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.futures.getPendingOrder()
```

```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.futures.getPendingOrder();
``` -->

> Response:

```json
{
	"code": 0, // Status code
	"msg": "success", //Message
	"i18nArgs": null,
	"data": [
		{
			"id": 1584848662192898000,// ID
			"orderId": 1584848661807022000,// Order ID
			"symbol": "BTCUSD",// Symbol
			"volume": 0.001,// Volume
			"remainVolume": 0.001,// Unfilled volume
			"fillVolume": 0,// Filled volume
			"price": 19000,// Price
			"avgPrice": 0,// Average price
			"initMargin": 6.333333,// Initial margin
			"tradeSide": 1,// Trade side  1 BUY 2 SELL
			"tradeType": 1,// Trade type 1 LIMIT 2 MARKET
			"createTime": 1666692340695,// Time of the order created
			"closeType": 1,//
			"leverage": 3 // Leverage
		}
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/order/pending/v1`

<aside class="notice">
   Get open orders (SIGNED)----Signature required
</aside>

**header**

name  | value  | Required | Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

Null

## Get Futures Order History

```shell
curl "http://api.coincall.com/open/futures/order/history/v1?pageSize=10&page=1&startTime=111&endTime=333" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getFuturesOrderHistory()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.futures.getOrderHistory()
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let orders = api.futures.getOrderHistory(123);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": {
		"list": [{
			"orderId": 1584837328353017856,// Order ID
			"symbol": "BTCUSD",// Symbol
			"volume": 0.0010000000000000,// Volume
			"fillVolume": 0E-16,// Filled volume
			"price": 18999.0000000000000000,// Price
			"avgPrice": 0E-8,// Average price
			"fee": 0E-16,// Fees
			"pnl": 0E-16,// Realized PnL
			"tradeSide": 2,// Trade side 1 BUY 2 SELL
			"tradeType": 1,// Trade type 1 LIMIT 2 MARKET
			"createTime": 1666689638588,// Time of the order created
			"state": 3,// Order state
			"closeType": 1,//
			"leverage": 3 // Leverage
		}],
		"pageTotal": 2 // Number of pages
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/order/history/v1?pageSize=10&page=1&startTime=111&endTime=333`

<aside class="notice">
   Get futures order history(SIGNED)----Signature required
</aside>

**header**

name  | value  | Required | Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

name  | value  | Required | Note
-------------- | -------------- | -------------- | --------
pageSize | 10 | true | Quantity per page
page | 1 | true | Numbe of pages
startTime | 1000000 | true |  Start time of the history
endTime | 200000 | true | End time of the history

## Get Futures Order Book 

```shell
curl "http://api.coincall.com/open/futures/order/orderbook/v1/{symbol}" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getFuturesOrderBook(symbol)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.futures.getOrderBook(symbol)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let orderbook = api.futures.getOrderBook(symbol);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": {
		"symbol": "BTCUSD",//symbol
		"bids": [{
			"volume": 0.001,// Volume
			"price": "18801"// Volume
		}],
		"asks": [{
			"volume": 0.992,// Volume
			"price": "18898"// Volume
		}]
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/order/orderbook/v1/{symbol}`

<aside class="notice">
   Get futures order book
</aside>

**header**

name  | value  | Required | Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

Null


## Get Futures Transaction History

```shell
curl "http://api.coincall.com/open/futures/trade/history/v1?pageSize=10&page=1&startTime=111&endTime=333" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getFuturesTradeHistory()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.futures.getTradeHistory(123)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let trades = api.futures.getTradeHistory(123);
``` -->

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
			"symbol": "ETHUSD",//symbol
			"tradeSide": 1,//Trade side 1 BUY 2 SELL
			"tradeType": 1,//Trade type 1 LIMIT 2 MARKET
			"price": 1389.00000000,// Price
			"volume": 1.00000000,// Volume
			"markPrice": null,// Mark price
			"indexPrice": 1389.26000000,// Index Price
			"orderId": 1574775820017352705,// Order ID
			"tradeId": 1574775820805869568,// Trade ID
			"fee": 0.13890000,// Fees
			"time": 1664290788701,// Time of the transaction
			"closeType": null,
			"leverage": 5 // Leverage
		}],
		"pageTotal": 1 // Number of pages
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/trade/history/v1?pageSize=10&page=1&startTime=111&endTime=333`

<aside class="notice">
   Get futrues transaction history (SIGNED)----Signature required
</aside>

**header**

name  | value  | Required | Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

name  | value  | Required | 说明
-------------- | -------------- | -------------- | --------
pageSize | 10 | true | Quantity per page
page | 1 | true | Numbe of pages
startTime | 1000000 | true |  Start time of the history
endTime | 200000 | true | End time of the history

## Get Futures Last Trade

```shell
curl "http://api.coincall.com/open/futures/trade/lasttrade/v1/{symbol}" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getFuturesLastTrade(symbol)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.futures.getLastTrade(symbol)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.futures.getLastTrade(symbol);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": [{
		"symbol": "BTCUSD",//symbol
		"price": 18898,// Price
		"volume": 0.001,// Volume
		"time": 1666754916559,// Time of the transaction
		"tradeSide": 1 // Trade side 1 BUY 2 SELL
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/trade/lasttrade/v1/{symbol}`

<aside class="notice">
   Get futures last trade
</aside>

**header**

name  | value  | Required | Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

Null

## Set Futures Leverage

```shell
curl "http://api.coincall.com/open/futures/leverage/set/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -D {}
```

<!-- ```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.setLeverage(10)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.leverage.set(10)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.leverage.set();
``` -->

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": null
}
```


### HTTP Request

`POST http://api.coincall.com/open/futures/leverage/set/v1`
<aside class="notice">
    Set futures leverage
</aside>


**header**

name  | value  | Required 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true
X-REQ-TS-DIFF | 100 | true

**Parameter**

name  | value  | Required 
-------------- | -------------- | --------------
symbol | BTCUSD | true
leverage | 10 | true



## Get futures leverage

```shell
curl "http://api.coincall.com/open/futures/leverage/current/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
```

<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.currentLeverage()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.leverage.current()
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let currLeverage = api.leverage.current();
``` -->

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


### HTTP Request

`GET http://api.coincall.com/open/futures/leverage/current/v1`

<aside class="notice">
    Get current futrues leverage
</aside>

**header**

name  | value  | Required 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true
X-REQ-TS-DIFF | 100 | true

**Parameter**

Null
