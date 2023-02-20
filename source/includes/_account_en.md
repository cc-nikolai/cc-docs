# User Account Related

## Get User Info

```shell
curl "http://api.coincall.com/open/user/info/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.userInfo()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.userInfo()
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let user = api.user.info();
``` -->

> Response:

```json
{
	"code": 0,
	"data": {
		"email": "",
		"name": "",
		"userId": "xxxx"
	},
	"i18nArgs": [],
	"msg": ""
}
```


### HTTP Request

`GET http://api.coincall.com/open/user/info/v1`
<aside class="notice">
    Get User Information(SIGNED)---- Signature Required
</aside>


**header**

name  | value  | Required 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true
X-REQ-TS-DIFF | 100 | true

**Parameter**
Null


## Get Account Summary

```shell
curl "http://api.coincall.com/open/account/summary/v1" \
  -H "X-CC-APIKEY: TEST"
  -H "X-REQ-TS-DIFF:1222"
```
<!-- 
```java
import coincall

CoincallClient api = new CoincallClient("key","secret");
api.accountSummary()
```

```python
import coincall

api = coincall.authorize('key','secret')
api.account.summary()
```



```javascript
const cc = require('coincall');

let api = cc.authorize('test','test');
let account = api.account.summary();
``` -->

> Response:

```json
{
	"code": 0,// Status code
	"data": {
    "accountId": 0,// Account ID
    "availableBalance": 0,// Available balance
    "canWithdrawAmount": 0,// Maximum amount can be withdrawn
    "equityAmount": 0,// Total assets value in account
    "imAmount": 0,// Total initial margin of account
    "marginBalance": 0,// Margin balance
    "marginMode": 0,// Margin mode （1 SM 2 PM)
    "mmAmount": 0,// Total maintenance margin of the account
    "unrealizedAmount": 0,// Total unrealized P/L of the account
	},
	"i18nArgs": [],
	"msg": ""// Message
}

```


### HTTP Request

`GET http://api.coincall.com/open/account/summary/v1`

<aside class="notice">
    Get account summary(SIGNED)---- Signature Required
</aside>

**header**

name  | value  | Required 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | true
X-REQ-TS-DIFF | 100 | true

**Parameter**

Null

## Switch Margin Mode
