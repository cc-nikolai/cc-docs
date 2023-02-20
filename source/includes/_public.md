# 公共接口

## 获取公共配置信息

```shell
curl "http://api.coincall.com/open/public/config/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.publicConfig()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.publicConfig()
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.public.config();
``` -->

> 接口返回值:

```json
{
  "code": 1,
  "msg": "succ",
  "i18nArgs": null,
  "data": {
    //阶梯保证金
    "ladderMargin": {
      "1": {
        "mmLevel": 0.01,//保证金率
        "level": 1,//保证金等级
        "start": 0,//当前等级最小持仓价值
        "end": 100000,//当前等级最大持仓价值
        "maxLevarage": 50 //最大杠杆倍数
      }
    },
    //期权配置
    "optionConfig": {
      "BTCUSD": {
        "volumeDecimal": 2,//面额精度
        "symbol": "BTCUSD",//symbol
        "multiplier": 0.01,//合约乘数
        "settle": "USD",//结算币种
        "limitMaxVolume": 1000,//最大开仓面额
        "priceDecimal": 2,//价格精度
        "maxVolume": 1000,//最大持仓面额
        "tickDecimal": 1,//ticker 精度
        "tickSize": 0.1,//ticker最小面额
        "greeksDecimal": 6,//希腊字母精度
        "marketMaxVolume": 1000,//
        "maxOrderSize": 200,//最大挂单数量
        "base": "BTC"//base token
      }
    },
    //期货配置
    "futuresConfig": {
      "BTCUSD": {
        "volumeDecimal": 3,//面额精度
        "symbol": "BTCUSD",//symbol
        "marketMaxVolume": 100,//
        "minVolume": 0.001,//最小挂单量
        "settle": "USD",//结算 token
        "maxOrderSize": 200,//最大挂单数量
        "priceDecimal": 2,//价格精度
        "limitMaxVolume": 1000,//最大开仓面额
        "tickDecimal": 1,//ticker 精度
        "base": "BTC",//base token
        "tickSize": 0.1//最小面额
      }
    }
  }
}
```


### HTTP Request

`GET http://api.coincall.com/open/public/config/v1`
<aside class="notice">
    获取交易相关的配置信息
</aside>


**header**

name  | value  | 是否必传 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是
X-REQ-TS-DIFF | 100 | 是

**参数**

无


## 获取资金费率


```shell
curl "http://api.coincall.com/open/public/fudingRate/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.fundingRate()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.public.fundingRate()
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let rates = api.public.fundingRate();
``` -->

> 接口返回值:

```json
{
  "code": 0,//状态码
  "msg": "success",//提示信息
  "i18nArgs": null,
  "data": [
    {
      "symbol": "BTCUSD",//symbol
      "rate": "-0.00500000",//保证金率
      "contractId": "1"//合约id
    }
  ]
}
```


### HTTP Request

`GET http://api.coincall.com/open/public/fundingRate/v1`

<aside class="notice">
    获取实时资金费率
</aside>

**header**

name  | value  | 是否必传 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是
X-REQ-TS-DIFF | 100 | 是

**参数**

无






