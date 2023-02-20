# 用户，账户

## 获取用户信息

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

> 接口返回值:

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
    获取用户信息(SIGNED)----需要签名
</aside>


**header**

name  | value  | 是否必传 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是
X-REQ-TS-DIFF | 100 | 是

**参数**
无


## 获取账户信息

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

> 接口返回值:

```json
{
	"code": 0,//状态码
	"data": {
    "accountId": 0,//账户主键
    "availableBalance": 0,//账户可用余额
    "canWithdrawAmount": 0,//可提现余额
    "equityAmount": 0,//账户资产净值
    "imAmount": 0,//账户总IM
    "marginBalance": 0,//账户保证金余额
    "marginMode": 0,//账户模式 （1 SM 2 PM)
    "mmAmount": 0,//账户总MM
    "unrealizedAmount": 0,//账户总未实现盈亏
	},
	"i18nArgs": [],
	"msg": ""//提示信息
}

```


### HTTP Request

`GET http://api.coincall.com/open/account/summary/v1`

<aside class="notice">
    获取账户信息(SIGNED)----需要签名
</aside>

**header**

name  | value  | 是否必传 
-------------- | -------------- | --------------
X-CC-APIKEY | rSclsRyRsiAfcoNjv73iD4B80BfW49q7IsIWjU0orf8= | 是
X-REQ-TS-DIFF | 100 | 是

**参数**

无

## 切换保证金模式
