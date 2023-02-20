# Options Endpoint

## Get Option Chain

```shell
curl "http://api.coincall.com/open/optioin/get/v1?endTime=123" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getTOption(123)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.tOption(123)
```


```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.option.get(123);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": [{
		"strike": 22000.00000000,// Strike price
		"callOption": {
			"optionId": 1584505132356345856,// Option ID
			"underSymbol": "BTCUSD",// Underlying symbol
			"optionName": "BTCUSD-26OCT22-22000-C",// Option name
			"endTime": 1666771200000,// Time of expiration
			"strike": 22000.00000000,// Strike price
			"lastPrice": 0,// Last price
			"markPrice": 0.0,// Mark price
			"tradeVolume": 0,// Trade volume
			"openInterest": 0,// Open interest
			"ask": 0,// Best ask price
			"askIv": 0.0,// Best ask IV
			"askVolume": 0,// Best ask volume
			"bid": 0,// Best bid price
			"bidIv": 0.0,// Best bid IV
			"bidVolume": 0,// Bid volume
			"markIv": 0.0,// Mark IV
			"type": 1,// Option type 1 CALL 2 PUT
			"lastPriceIv": 1.7976931348623157E308,// Last priceIV
			"underlyingPrice": 20278.25,// Price of the underlying
			"delta": 0.0,//greeks delta
			"gamma": 0.0,//greeks gamma
			"vega": 0.0,//greeks vega
			"theta": 0.0//greeks theta
		},
		"putOption": {
			"optionId": 1584505132356345856,// Option ID
			"underSymbol": "BTCUSD",// Underlying symbol
			"optionName": "BTCUSD-26OCT22-22000-C",// Option name
			"endTime": 1666771200000,// Time of expiration
			"strike": 22000.00000000,// Strike price
			"lastPrice": 0,// Last price
			"markPrice": 0.0,// Mark price
			"tradeVolume": 0,// Trade volume
			"openInterest": 0,// Open interest
			"ask": 0,// Best ask price
			"askIv": 0.0,// Best ask IV
			"askVolume": 0,// Best ask volume
			"bid": 0,// Best bid price
			"bidIv": 0.0,// Best bid IV
			"bidVolume": 0,// Bid volume
			"markIv": 0.0,// Mark IV
			"type": 2,// Option type 1 CALL 2 PUT
			"lastPriceIv": 1.7976931348623157E308,// Last priceIV
			"underlyingPrice": 20278.25,// Price of the underlying
			"delta": 0.0,//greeks delta
			"gamma": 0.0,//greeks gamma
			"vega": 0.0,//greeks vega
			"theta": 0.0//greeks theta
		}
	}
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/get/v1?endTime=123`

<aside class="notice">
   Get option chain
</aside>

**header**

name  | value  |  Required 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true
X-REQ-TS-DIFF | 100 | true

**Parameter**

name  | value  |  Required  |  Note
-------------- | -------------- | -------------- | --------
endTime | 1233 | true | Expiration time


## Get Option Details

```shell
curl "http://api.coincall.com/open/optioin/detail/v1/{optionName}" \
  -H "X-CC-APIKEY: TEST"
\  -H "X-REQ-TS-DIFF:1222"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getOptionDetail(BTCUSD-XXX)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.detail(BTCUSD-XXX)
```


```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.option.detail(BTCUSD-XX);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",
	"i18nArgs": null,
	"data": {
		"optionId": 1584505132293431296,// Option ID
		"optionName": "BTCUSD-26OCT22-20000-P",// Option name
		"endTime": 1666771200000,// Time of expiration
		"remainTime": 13565073,// Time remain until expiration
		"strike": 20000.00000000,// Strike price
		"markPrice": 10.231632230252217,// Mark price
		"tradeVolume": 1.00000000,// Trade volume
		"tradeValue": 1.00000000,// Trade value
		"openInterest": 0,// Open interest
		"lastPrice": 10.231632230252217,// Last price
		"premium": 0,// Premium
		"changeRate": 2.87,// Price change in percentage
		"changeVolume": 473.78165573,// Price change in value
		"iv": 0.58,// Implied volatility
		"type": 2,// Option type 1 CALL 2 PUT
		"indexPrice": 20239.96000000,// Index price
		"price24hHigh": 0,// Highest price in 24hrs
		"price24hLow": 0,// Lowest price in 24hrs
		"volumeUsd24h": 0,// USD volume in 24hrs
		"price24hOpen": 18215.964000000,// Open price on UTC 00:00:00
		"volume24h": 0,// 24h Trade volume
		"delta": -0.10808987585883545,//greeks delta
		"gamma": 0.0009475995953294489,//greeks gamma
		"vega": 0.7794498985827641,//greeks vega
		"theta": 0.0,//greeks theta
		"rho": -0.009454405809863273,//greeks rho
		"maxDelta": null//max delta
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/detail/v1/{optionName}`

<aside class="notice">
   Get option details
</aside>

**header**

name  | value  |  Required 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true
X-REQ-TS-DIFF | 100 | true

**Parameter**

Null


## Get Option Positions

```shell
curl "http://api.coincall.com/open/option/position/get/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getOptionPosition()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.getPosition(123)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.option.getPosition(123);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": [{
		"id": 1584736851047620608,// ID
		"positionId": 1584736851047620609,// Position ID
		"updateTime": 1666665682934,// Opdate time
		"orderId": 1584736036348895232,// Order ID
		"userId": 1536933707941347382,// User ID
		"value": 11294.2000000000000000,// Value
		"volume": 1.00000000,// Volume
		"closeVolume": 0E-8,// Close volume
		"initMargin": 0,// Initial Margin
		"maintMargin": 0,// Maintnance Margin
		"avgPrice": 11294.20000000,// Average Price
		"markPrice": 12260.310000000001,// Mark price
		"elp": null,// Estimated liquidation Price
		"pnl": 966.11000000000100000000,// Realized PnL
		"roi": 8.55403659,// Return on investment
		"unpl": 966.11000000000100000000,// Unrealized PnL
		"optionName": "BTCUSD-25NOV22-8000-C",// Option name
		"tradeSide": 1,// Trade Side 1 BUY 2 SELL
		"tradeType": 1,// Trade Type 1 LIMIT 2 MARKET
		"lockVolume": 0,// Lock volume
		"delta": 1.0,// greeks delta
		"gamma": 0.0,// greeks gamma
		"vega": 0.0,// greeks vega
		"theta": 0.0,// greeks theta
		"rho": 6.610892947742262// greeks rho
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/position/get/v1`

<aside class="notice">
   Get option positions(SIGNED)----Signature required
</aside>

**header**

name  | value  |  Required |  Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

Null

## Place Orders

```shell
curl "http://api.coincall.com/open/option/order/create/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -D {}
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.placeOptionOrder(param)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.placeOrder(10)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.optioin.placeOrder();
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data":null
}
```


### HTTP Request

`POST http://api.coincall.com/open/option/order/create/v1`

<aside class="notice">
    Place option orders(SIGNED)----Signature required
</aside>

**header**

name  | value  |  Required  |  Note
-------------- | -------------- | -------------- | ----
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true |
sign | xxx | true | Endpoint Signature

**Parameter**

name  | value  |  Required |  Note
-------------- | -------------- | --------------
optionName | BTCUSD-26OCT22-15000-C | true |  Option name
price | 19000 | false | Price required for limit orders
volume| 0.5 | true | Quantity 
tradeSide | 1 | true | Trade Side 1 BUY 2 SELL
tradeType | 1 | true | Trade Type 1 LIMIT 2 MARKET




## Cancel Option Orders

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
api.cancelOptionOrder(orderId)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.cancelOrder(123)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.option.cancelOrder(123);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data":null
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/order/cancel/v1/{orderId}`

<aside class="notice">
   Cancel option orders(SIGNED)----Signature required
</aside>

**header**

name  | value  |  Required |  Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

name | value | Required | Note
-------------- | -------------- | -------------- | --------------
orderId | 111 | true | query string


## Get option open orders

```shell
curl "http://api.coincall.com/open/option/order/pending/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getOptionPendingOrder()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.getPendingOrder()
```

```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.option.getPendingOrder();
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": [{
		"id": 1584744827800133633,// ID
		"orderId": 1584744827800133632,// Order ID
		"optionName": "BTCUSD-25NOV22-20000-C",// Option name
		"volume": 5.00000000,// Volume
		"remainVolume": 2.00000000,// Unfilled volume
		"fillVolume": 3.00000000,// Filled volume
		"price": 951.00000000,// Price
		"avgPrice": 951.00000000,// Avrage price
		"initMargin": 1902.0000000000000000,// Initial Margin
		"tradeSide": 1,// Trade side 1 BUT 2 SELL
		"tradeType": 1,// Trade type 1 LIMIT 2 MARKET
		"createTime": 1666667584739,// Time of the order created
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/order/pending/v1`

<aside class="notice">
   Get option open orders(SIGNED)----Signature required
</aside>

**header**

name  | value  |  Required |  Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

Null

## Get Option Order History 

```shell
curl "http://api.coincall.com/open/option/order/history/v1?pageSize=10&page=1&startTime=111&endTime=333" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getOptionOrderHistory()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.getOrderHistory()
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.option.getOrderHistory(123);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": {
		"list": [{
			"orderId": 1584784227935854592,// Order ID
			"optionName": "BTCUSD-25NOV22-14000-C",// Option name
			"volume": 5.00000000,// Volume
			"fillVolume": 0E-8,// Filled volume
			"price": 0.50000000,// Order price
			"avgPrice": null,// Average Price
			"fee": 0,// Fees
			"pnl": 0,// Realized PnL
			"tradeSide": 1,// Trade side 1 BUY 2 SELL
			"tradeType": 2,// Trade type 1 LIMIT 2 MARKET
			"createTime": 1666676978465,// Time of the order created
			"state": 3,// Order status
		}],
		"pageTotal": 1// Number of pages
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/order/history/v1?pageSize=10&page=1&startTime=111&endTime=333`

<aside class="notice">
   Get Option Order History (SIGNED)----Signature required
</aside>

**header**

name  | value  |  Required |  Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

name  | value  |  Required | Note
-------------- | -------------- | -------------- | --------
pageSize | 10 | true | Quantity per page 
page | 1 | true | Numbe of pages
startTime | 1000000 | true |  Start time of the history
endTime | 200000 | true | End time of the history

## Get Option Order Book

```shell
curl "http://api.coincall.com/open/option/order/orderbook/v1/{optionName}" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getOptionOrderBook(optionName)
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.getOrderBook(optionName)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.option.getOrderBook(optionName);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": {
		"optionName": "BTCUSD-26OCT22-15000-C",// Option name
		"strike": 15000,// Strike price
		"bids": [{
			"volume": 0.5,// Volume
			"price": "5251"// Price
		}],
		"asks": [{
			"volume": 1,// Volume
			"price": "8888"// Price
		}]
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/order/orderbook/v1/{optionName}`

<aside class="notice">
   Get option order book
</aside>

**header**

name  | value  |  Required |  Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

Null


## Get Option Transaction History

```shell
curl "http://api.coincall.com/open/option/trade/history/v1?pageSize=10&page=1&startTime=111&endTime=333" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getOptionTradeHistory()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.getTradeHistory(123)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.option.getTradeHistory(123);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": {
		"list": [{
			"id": 1584745240079241216,// ID
			"optionId": null,// Option ID
			"optionName": "BTCUSD-25NOV22-20000-C",// Option name
			"tradeSide": 1,// Trade side 1 BUY 2 SELL
			"tradeType": 1,// Trade type 1 LIMIT 2 MARKET
			"price": 951.00000000,// Price
			"volume": 2.00000000,// Trade volume
			"iv": 0.5606,// Implied Volatility
			"markPrice": 1419.5139928388217,// Mark price
			"indexPrice": 20247.0,// Index price
			"orderId": 1584744827800133632,// Order ID
			"tradeId": 1584745239911469056,// Trade ID
			"fee": 0.00190200,// Fees
			"time": 1666667683034// Transaction time
		}],
		"pageTotal": 1 // Number of pages
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/trade/history/v1?pageSize=10&page=1&startTime=111&endTime=333`

<aside class="notice">
   Get option transaction history(SIGNED)----Signature required
</aside>

**header**

name  | value  |  Required |  Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

name  | value  |  Required | Note
-------------- | -------------- | -------------- | --------
pageSize | 10 | true | Quantity per page
page | 1 | true | Numbe of pages
startTime | 1000000 | true |  Start time of the history
endTime | 200000 | true | End time of the history

## Get Option Last Trade

```shell
curl "http://api.coincall.com/open/option/trade/lasttrade/v1/{optionName}" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
  -H "sign:xxx"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.getOptionLastTrade()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.option.getLastTrade(optionName)
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.option.getLastTrade(optionName);
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": [{
		"optionName": "BTCUSD-26OCT22-20000-P",// Option name
		"price": 10.3,// Trade price
		"volume": 1,// Trade volume
		"time": 1666757622819,// Trade time
		"tradeSide": 2// Trade side 1 BUY 2 SELL
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/trade/lasttrade/v1/{optionName}`

<aside class="notice">
   Get option last trade
</aside>

**header**

name  | value  |  Required |  Note
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true |
X-REQ-TS-DIFF | 100 | true | 
sign | xxx | true | Endpoint Signature

**Parameter**

Null