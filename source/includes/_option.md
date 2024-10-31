# 期权接口

## Cancel batchOrders(SIGNED)

Cancel batch Orders by ids

> Request:

```json
POST http://api.coincal.com/open/option/batchorders/cancel/v1
body
[
    {
        "symbol":"BTCUSD",
        "ordId":"590908157585625111"
    },
    {
        "instId":"BTCUSD",
        "ordId":"590908544950571222"
    }
]
```

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

`POST http://api.coincal.com/open/option/batchorders/cancel/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | string | BTCUSD | true | symbol name
orderId | list | BTCUSD | false | coin index symbol name
orderId | list | BTCUSD | false | coin index symbol name

**Notice**:

orderId and clientOrderId, one of the two parameters must be entered.



## 查询T型报价表

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": [{
		"strike": 22000.00000000,//行权价
		"callOption": {
			"optionId": 1584505132356345856,//期权id
			"underSymbol": "BTCUSD",//标的symbol
			"optionName": "BTCUSD-26OCT22-22000-C",//期权名
			"endTime": 1666771200000,//行权时间
			"strike": 22000.00000000,//行权价
			"lastPrice": 0,//最新价
			"markPrice": 0.0,//标记价格
			"tradeVolume": 0,//成交量
			"openInterest": 0,//未平仓量
			"ask": 0,//卖一
			"askIv": 0.0,//卖一 IV
			"askVolume": 0,//卖一量
			"bid": 0,//买一
			"bidIv": 0.0,//买一 IV
			"bidVolume": 0,//买一量
			"markIv": 0.0,//标记IV
			"type": 1,//期权类型 1 CALL 2 PUT
			"lastPriceIv": 1.7976931348623157E308,//最新价IV
			"underlyingPrice": 20278.25,//标的价格
			"delta": 0.0,//greeks delta
			"gamma": 0.0,//greeks gamma
			"vega": 0.0,//greeks vega
			"theta": 0.0//greeks theta
		},
		"putOption": {
			"optionId": 1584505132356345856,//期权id
			"underSymbol": "BTCUSD",//标的symbol
			"optionName": "BTCUSD-26OCT22-22000-C",//期权名
			"endTime": 1666771200000,//行权时间
			"strike": 22000.00000000,//行权价
			"lastPrice": 0,//最新价
			"markPrice": 0.0,//标记价格
			"tradeVolume": 0,//成交量
			"openInterest": 0,//未平仓量
			"ask": 0,//卖一
			"askIv": 0.0,//卖一 IV
			"askVolume": 0,//卖一量
			"bid": 0,//买一
			"bidIv": 0.0,//买一 IV
			"bidVolume": 0,//买一量
			"markIv": 0.0,//标记IV
			"type": 2,//期权类型 1 CALL 2 PUT
			"lastPriceIv": 1.7976931348623157E308,//最新价IV
			"underlyingPrice": 20278.25,//标的价格
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
   获取T型报价表
</aside>

**header**

name  | value  | 是否必传 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是
X-REQ-TS-DIFF | 100 | 是

**参数**

name  | value  | 是否必传  | 备注
-------------- | -------------- | -------------- | --------
endTime | 1233 | 是 | 期权到期时间


## 查询期权详情

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",
	"i18nArgs": null,
	"data": {
		"optionId": 1584505132293431296,//期权id
		"optionName": "BTCUSD-26OCT22-20000-P",//期权名
		"endTime": 1666771200000,//行权时间
		"remainTime": 13565073,//剩余时间
		"strike": 20000.00000000,//行权价
		"markPrice": 10.231632230252217,//标记价格
		"tradeVolume": 1.00000000,//交易量
		"tradeValue": 1.00000000,//交易价值
		"openInterest": 0,//未平仓量
		"lastPrice": 10.231632230252217,//最新价
		"premium": 0,//权利金
		"changeRate": 2.87,//涨跌幅
		"changeVolume": 473.78165573,//涨跌额
		"iv": 0.58,//隐含波动率
		"type": 2,//期权类型 1 CALL 2 PUT
		"indexPrice": 20239.96000000,//指数价格
		"price24hHigh": 0,//24h最高价
		"price24hLow": 0,//24h最低价
		"volumeUsd24h": 0,//24h成交额（usd）
		"price24hOpen": 18215.964000000,//UTC 0点开盘价
		"volume24h": 0,//24h成交量
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
   获取期权详情
</aside>

**header**

name  | value  | 是否必传 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是
X-REQ-TS-DIFF | 100 | 是

**参数**

无


## 查询期权仓位信息

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": [{
		"id": 1584736851047620608,//仓位主键
		"positionId": 1584736851047620609,//仓位编码
		"updateTime": 1666665682934,//更新时间
		"orderId": 1584736036348895232,//订单编码
		"userId": 1536933707941347382,//用户编码
		"value": 11294.2000000000000000,//仓位价值
		"volume": 1.00000000,//仓位面额
		"closeVolume": 0E-8,//平仓面额
		"initMargin": 0,//仓位维持保证金
		"maintMargin": 0,//仓位维持保证金
		"avgPrice": 11294.20000000,//持仓均价
		"markPrice": 12260.310000000001,//标记价格
		"elp": null,//预估强平价
		"pnl": 966.11000000000100000000,//已实现盈亏
		"roi": 8.55403659,//回报率
		"unpl": 966.11000000000100000000,//未实现盈亏
		"optionName": "BTCUSD-25NOV22-8000-C",//期权名
		"tradeSide": 1,//交易方向 1 BUY 2 SELL
		"tradeType": 1,//交易类型 1 LIMIT 2 MARKET
		"lockVolume": 0,//冻结面额
		"delta": 1.0,//greeks delta
		"gamma": 0.0,//greeks gamma
		"vega": 0.0,//greeks vega
		"theta": 0.0,//greeks theta
		"rho": 6.610892947742262//greeks rho
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/position/get/v1`

<aside class="notice">
   获取期权当前持仓(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

无

## 期权下单

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data":null
}
```


### HTTP Request

`POST http://api.coincall.com/open/option/order/create/v1`

<aside class="notice">
    期权下单(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传  | 备注
-------------- | -------------- | -------------- | ----
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 |
sign | xxx | 是 | 接口签名

**参数**

name  | value  | 是否必传 | 备注
-------------- | -------------- | --------------
optionName | BTCUSD-26OCT22-15000-C | 是 | 期权名
price | 19000 | 否 | 价格：限价单必传
volume| 0.5 | 是 | 数量 
tradeSide | 1 | 是 | 交易方向：1 buy 2 sell
tradeType | 1 | 是 | 交易类型：1 limit 2 market




## 取消期权委托单

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data":null
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/order/cancel/v1/{orderId}`

<aside class="notice">
   撤销期权委托单(SIGNED)----需要签名
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


## 查询期权委托单

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": [{
		"id": 1584744827800133633,//订单id
		"orderId": 1584744827800133632,//订单编码
		"optionName": "BTCUSD-25NOV22-20000-C",//期权名
		"volume": 5.00000000,//订单面额
		"remainVolume": 2.00000000,//未成交面额
		"fillVolume": 3.00000000,//已成交面额
		"price": 951.00000000,//挂单价格
		"avgPrice": 951.00000000,//均价
		"initMargin": 1902.0000000000000000,//委托IM
		"tradeSide": 1,//订单方向 1 BUT 2 SELL
		"tradeType": 1,//订单类型 1 LIMIT 2 MARKET
		"createTime": 1666667584739,//创建时间
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/order/pending/v1`

<aside class="notice">
   查询期权当前委托单(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

无

## 查询期权订单历史

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": {
		"list": [{
			"orderId": 1584784227935854592,//订单编码
			"optionName": "BTCUSD-25NOV22-14000-C",//期权名
			"volume": 5.00000000,//挂单面额
			"fillVolume": 0E-8,//成交面额
			"price": 0.50000000,//挂单价
			"avgPrice": null,//均价
			"fee": 0,//手续费
			"pnl": 0,//已实现盈亏
			"tradeSide": 1,//订单方向 1 BUY 2 SELL
			"tradeType": 2,//订单类型 1 LIMIT 2 MARKET
			"createTime": 1666676978465,//下单时间
			"state": 3,//订单状态
		}],
		"pageTotal": 1//总页数
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/order/history/v1?pageSize=10&page=1&startTime=111&endTime=333`

<aside class="notice">
   获取期权订单历史(SIGNED)----需要签名
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

## 查询期权订单薄

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": {
		"optionName": "BTCUSD-26OCT22-15000-C",//期权名
		"strike": 15000,//行权价
		"bids": [{
			"volume": 0.5,//挂单量
			"price": "5251"//挂单价
		}],
		"asks": [{
			"volume": 1,//挂单量
			"price": "8888"//挂单价
		}]
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/order/orderbook/v1/{optionName}`

<aside class="notice">
   获取期权订单薄
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

无


## 查询期权成交历史

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": {
		"list": [{
			"id": 1584745240079241216,//成交主键
			"optionId": null,//期权id
			"optionName": "BTCUSD-25NOV22-20000-C",//期权名
			"tradeSide": 1,//成交方向 1 BUY 2 SELL
			"tradeType": 1,//成交类型 1 LIMIT 2 MARKET
			"price": 951.00000000,//成交价
			"volume": 2.00000000,//成交量
			"iv": 0.5606,//隐含波动率
			"markPrice": 1419.5139928388217,//标记价格
			"indexPrice": 20247.0,//指数价格
			"orderId": 1584744827800133632,//订单编码
			"tradeId": 1584745239911469056,//交易编码
			"fee": 0.00190200,//成交手续费
			"time": 1666667683034//成交时间
		}],
		"pageTotal": 1 //总页码
	}
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/trade/history/v1?pageSize=10&page=1&startTime=111&endTime=333`

<aside class="notice">
   获取期权成交历史(SIGNED)----需要签名
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

## 查询期权最近成交记录

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"msg": "success",//提示信息
	"i18nArgs": null,
	"data": [{
		"optionName": "BTCUSD-26OCT22-20000-P",//期权名
		"price": 10.3,//成交价
		"volume": 1,//成交量
		"time": 1666757622819,//成交时间
		"tradeSide": 2//交易方向 1 BUY 2 SELL
	}]
}
```


### HTTP Request

`GET http://api.coincall.com/open/option/trade/lasttrade/v1/{optionName}`

<aside class="notice">
   获取期权最近成交记录
</aside>

**header**

name  | value  | 是否必传 | 备注
-------------- | -------------- | -------------- | --------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是 |
X-REQ-TS-DIFF | 100 | 是 | 
sign | xxx | 是 | 接口签名

**参数**

无