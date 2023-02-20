# 期货接口

## 查询期货交易对

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": [{
		"contractId": 1,//合约id
		"symbol": "BTCUSD",//合约名
		"symbolName": "BTC-PERP",//合约别名
		"price": 20260.31,//最新价
		"changeRate": 0,//合约涨跌幅
		"changeVolume": 0,//合约涨跌额
		"markPrice": 18898.4293759300000000,//标记价格
		"indexPrice": 20260.31,//指数价格
		"price24hHigh": 0,//24小时最高价
		"price24hLow": 0,//24小时最低价
		"volumeUsd24h": 0,//24小时成交U
		"volume24h": 0,//24小时成交额
		"ts": null,//时间
		"price24hOpen": 18234.279//UTC 0点开盘价
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/market/symbol/v1`

<aside class="notice">
   获取期货交易对
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

无


## 查询期货仓位信息

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

> 接口返回值:

```json
{
  "code": 0,//状态码
  "msg": "success",//提示信息
  "i18nArgs": null,
  "data": [
    {
      "id": 1584467417583730700,//仓位主键
      "positionId": 1584467417583730700,//仓位编码
      "updateTime": 1666602220413,//更新时间
      "userId": 1536933707941347300,//用户编码
      "value": 176.7825,//仓位价值
      "volume": 0.009,//仓位面额
      "initMargin": 35.3565,//仓位初始保证金
      "maintMargin": 1.767825,//仓位维持保证金
      "avgPrice": 19642.5,//持仓均价
      "markPrice": 18900.38311437,//标记价格
      "elp": null,//预估强平价
      "pnl": 0,//已实现盈亏
      "roi": -0.03778118,//回报率
      "rspl": 0,//
      "unpl": -6.67905197067,//未实现盈亏
      "symbol": "BTCUSD",//symbol
      "tradeSide": 1,//交易方向 1 BUY  2 SELL
      "tradeType": null,//交易类型  1 LIMIT 2 MARKET 
      "lockVolume": 0,//锁定面额
      "leverage": 5,//杠杆
      "delta": 0.009//仓位delta
    }
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/position/get/v1`

<aside class="notice">
   获取期货当前持仓(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

无

## 期货下单

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

> 接口返回值:

```json
{
  "code": 0,//状态码
  "msg": "success",//提示信息
  "i18nArgs": null,
  "data": null
}
```


### HTTP Request

`POST http://api.coincall.com/open/futures/order/create/v1`

<aside class="notice">
    期货下单(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传  | 备注
-------------- | -------------- | -------------- | ----
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 |
sign | xxx | 是 | 接口签名

**参数**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | -------
symbol | BTCUSD | 是 | 合约标识
price | 19000 | 否 | 价格：限价单必传
volume| 0.5 | 是 | 数量 
tradeSide | 1 | 是 | 交易方向：1 buy 2 sell
tradeType | 1 | 是 | 交易类型：1 limit 2 market
isClose | true | 是否是平仓单 




## 取消期货委托单

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

> 接口返回值:

```json
{
  "code": 0,//状态码
  "msg": "success",//提示信息
  "i18nArgs": null,
  "data": null
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/order/cancel/v1/{orderId}`

<aside class="notice">
   撤销期货委托单(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

name | value | 是否必填 | 说明
-------------- | -------------- | -------------- | --------------
orderId | 111 | 是 | query string


## 查询期货委托单

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

> 接口返回值:

```json
{
	"code": 0, //状态码
	"msg": "success", //提示信息
	"i18nArgs": null,
	"data": [
		{
			"id": 1584848662192898000,//订单主键
			"orderId": 1584848661807022000,//订单编码
			"symbol": "BTCUSD",//symbol
			"volume": 0.001,//订单面额
			"remainVolume": 0.001,//订单未成交面额
			"fillVolume": 0,//订单已成交面额
			"price": 19000,//挂单价格
			"avgPrice": 0,//均价
			"initMargin": 6.333333,//IM(初始保证金)
			"tradeSide": 1,//交易方向  1 BUY 2 SELL
			"tradeType": 1,//交易类型 1 LIMIT 2 MARKET
			"createTime": 1666692340695,//创建时间
			"closeType": 1,//
			"leverage": 3 //杠杆
		}
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/order/pending/v1`

<aside class="notice">
   查询期货当前委托单(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

无

## 查询期货订单历史

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": {
		"list": [{
			"orderId": 1584837328353017856,//订单编码
			"symbol": "BTCUSD",//symbol
			"volume": 0.0010000000000000,//订单面额
			"fillVolume": 0E-16,//成交面额
			"price": 18999.0000000000000000,//订单价格
			"avgPrice": 0E-8,//均价
			"fee": 0E-16,//手续费
			"pnl": 0E-16,//已实现盈亏
			"tradeSide": 2,//交易方向 1 BUY 2 SELL
			"tradeType": 1,//交易类型 1 LIMIT 2 MARKET
			"createTime": 1666689638588,//创建时间
			"state": 3,//订单状态
			"closeType": 1,//
			"leverage": 3 // 杠杆
		}],
		"pageTotal": 2 //总页数
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/order/history/v1?pageSize=10&page=1&startTime=111&endTime=333`

<aside class="notice">
   获取期货订单历史(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

name  | value  | 是否必传 | 说明
-------------- | -------------- | -------------- | --------
pageSize | 10 | 是 | 一页数量
page | 1 | 是 | 页码
startTime | 1000000 | 是 |  数据开始时间
endTime | 200000 | 是 | 数据结束时间

## 查询期货订单薄

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": {
		"symbol": "BTCUSD",//symbol
		"bids": [{
			"volume": 0.001,//挂单量
			"price": "18801"//挂单价
		}],
		"asks": [{
			"volume": 0.992,//挂单量
			"price": "18898"//挂单价
		}]
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/order/orderbook/v1/{symbol}`

<aside class="notice">
   获取期货订单薄
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

无


## 查询期货成交历史

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": {
		"list": [{
			"id": 1574775822713806849,//交易id
			"contractId": null,//合约id
			"symbol": "ETHUSD",//symbol
			"tradeSide": 1,//交易方向 1 BUY 2 SELL
			"tradeType": 1,//交易类型 1 LIMIT 2 MARKET
			"price": 1389.00000000,//成交价
			"volume": 1.00000000,//成交量
			"markPrice": null,//标记价格
			"indexPrice": 1389.26000000,//指数价格
			"orderId": 1574775820017352705,//订单编码
			"tradeId": 1574775820805869568,//交易编码
			"fee": 0.13890000,//成交手续费
			"time": 1664290788701,//成交时间
			"closeType": null,
			"leverage": 5 //杠杆
		}],
		"pageTotal": 1 //总页数
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/trade/history/v1?pageSize=10&page=1&startTime=111&endTime=333`

<aside class="notice">
   获取期货成交历史(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

name  | value  | 是否必传 | 说明
-------------- | -------------- | -------------- | --------
pageSize | 10 | 是 | 一页数量
page | 1 | 是 | 页码
startTime | 1000000 | 是 |  数据开始时间
endTime | 200000 | 是 | 数据结束时间

## 查询期货最近成交记录

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": [{
		"symbol": "BTCUSD",//symbol
		"price": 18898,//成交价
		"volume": 0.001,//成交量
		"time": 1666754916559,//成交时间
		"tradeSide": 1 //交易方向
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/trade/lasttrade/v1/{symbol}`

<aside class="notice">
   获取期货最近成交记录
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

无

## 设置杠杆倍数

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

> 接口返回值:

```json
{
  "code": 0,//状态
  "msg": "success",//提示信息
  "i18nArgs": null,
  "data": null
}
```


### HTTP Request

`POST http://api.coincall.com/open/futures/leverage/set/v1`
<aside class="notice">
    设置杠杆倍数
</aside>


**header**

name  | value  | 是否必传 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是
X-REQ-TS-DIFF | 100 | 是

**参数**

name  | value  | 是否必传 
-------------- | -------------- | --------------
symbol | BTCUSD | 是
leverage | 10 | 是



## 查询当前杠杆倍数

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

> 接口返回值:

```json
{
  "code": 0,//状态码
  "msg": "success",
  "i18nArgs": null,
  "data": {
    "userId": 123,//用户编码
    "symbol": "BTCUSD",//symbol
    "currentLeverage": 5 //当前杠杆倍数
  }
}
```


### HTTP Request

`GET http://api.coincall.com/open/futures/leverage/current/v1`

<aside class="notice">
    查询当前设置的的杠杆倍数
</aside>

**header**

name  | value  | 是否必传 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是
X-REQ-TS-DIFF | 100 | 是

**参数**

无
