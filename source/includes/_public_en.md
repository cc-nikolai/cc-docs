# Public Endpoints

## Get Public Configurations

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

> Response:

```json
{
  "code": 1,
  "msg": "succ",
  "i18nArgs": null,
  "data": {
    // Ladder margin
    "ladderMargin": {
      "1": {
        "mmLevel": 0.01,// Maintnance margin ratio
        "level": 1,// Margin level
        "start": 0,// Min position at current margin level
        "end": 100000,// Max position at current margin level
        "maxLevarage": 50 // Max leverage
      }
    },
    // Options configuration
    "optionConfig": {
      "BTCUSD": {
        "volumeDecimal": 2,// Decimal of the volume
        "symbol": "BTCUSD",// Symbol
        "multiplier": 0.01,// Multiplier
        "settle": "USD",// Settlement currency
        "limitMaxVolume": 1000,// Limit of the maximum volume
        "priceDecimal": 2,// Price decimal
        "maxVolume": 1000,// Maximum volume
        "tickDecimal": 1,// Ticker decimal
        "tickSize": 0.1,// Tick size
        "greeksDecimal": 6,// Greeks decimal
        "marketMaxVolume": 1000,//
        "maxOrderSize": 200,// Maximum order size
        "base": "BTC"// Base token
      }
    },
    // Futures Configuration
    "futuresConfig": {
      "BTCUSD": {
        "volumeDecimal": 3,// Volume Decimal
        "symbol": "BTCUSD",// Symbol
        "marketMaxVolume": 100,//
        "minVolume": 0.001,// Minimum volume
        "settle": "USD",// Settlement currency
        "maxOrderSize": 200,// Maximum order size
        "priceDecimal": 2,// Price decimal
        "limitMaxVolume": 1000,// Limit of the maximum volume
        "tickDecimal": 1,// ticker decimal
        "base": "BTC",// Base token
        "tickSize": 0.1// Tick size
      }
    }
  }
}
```


### HTTP Request

`GET http://api.coincall.com/open/public/config/v1`
<aside class="notice">
    Get trading-related configuration
</aside>


**header**

name  | value  | Required 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true
X-REQ-TS-DIFF | 100 | true

**Parameter**

Null


## Get Funding Rate


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

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",// Message
  "i18nArgs": null,
  "data": [
    {
      "symbol": "BTCUSD",// Symbol
      "rate": "-0.00500000",// Margin rate
      "contractId": "1"// Contract ID
    }
  ]
}
```


### HTTP Request

`GET http://api.coincall.com/open/public/fundingRate/v1`

<aside class="notice">
    Get real-time funding rates
</aside>

**header**

name  | value  | Required
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true
X-REQ-TS-DIFF | 100 | true

**Parameter**

Null






