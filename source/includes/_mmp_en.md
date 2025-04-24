# Mmp Endpoint

## Set MMP Config (SIGNED)

Use this interface to configure MMP. 

**HTTP Request** 

`POST https://api.coincall.com/open/mmp/set-mmp-config/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
indexName | string | BTCUSD	| TRUE	| Index identifier of derivative 
intervalTime | integer	| 5,000	 | TRUE | 	MMP Interval(ms), if set to 0 MMP is removed. And this setting must be between 1000 ms and 100000000 ms.
frozenTime	| integer	| 5,000	 | TRUE	| MMP frozen time(ms), if set to 0 manual reset is required. And this setting must be between 1000 ms and 100000000 ms.
qtyLimit	| number	| 5000	| FALSE	 | Quantity, this setting must be greater than or equal to 0.01.
deltaLimit	| number	| 10	| FALSE	 | Delta, this setting must be greater than or equal to 0.01.

> Request:

```json
{
curl -X POST 
    -H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU=" 
    -H "sign: 673C79B65E37AD3871B132A4707B958EC8B32C3DE021471E642D0D1FFED76D98" 
    -H "ts: 1745477450599" 
    -H "X-REQ-TS-DIFF: 5000" 
    -H "Content-Type: application/json" -d '{
            "indexName":"BTCUSD", //Index names, such as BTCUSD and ETHUSD.
            "intervalTime":"5000", //Time interval, in milliseconds. "0" - disables MMP. The default is "0". To enable MMP, set a value within the range [1000, 1000000000].
            "frozenTime":"5000", //Freeze interval, in milliseconds. "0" means the state remains frozen until the "Reset MMP Status" API is called to unfreeze it.For non-permanent freeze, set a value within the range [1000, 1000000000]
            "qtyLimit": "5000",  //Trade notional limit, must be greater than 0. Valid range: ≥ 0.01.
            "deltaLimit": "10"   //Net trade delta limit, must be greater than 0.Valid range: ≥ 0.01.
        }' "https://beta.seizeyouralpha.com/open/mmp/set-mmp-config/v1"
}

```

> Response:

```json 
{
  "code": 0,
  "msg": "success",
  "i18nArgs": null,
  "data": true
}

```

## Get MMP Config (SIGNED) 

Get MMP config.

**HTTP Request**  

`GET https://api.coincall.com/open/mmp/get-mmp-config/v1`

**Parameter** 

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
indexName | 	String | 	BTCUSD	|TRUE	 | Index identifier of derivative

> Request:

```json
{
    curl -X GET 
    -H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU=" 
    -H "sign: 4C8ADD9FBCA839970C9871E993EA29BE2EC5AC36CF946FC03DCAF07E7E98A69D" 
    -H "ts: 1745477060021" 
    -H "X-REQ-TS-DIFF: 5000" 
    -H "Content-Type: "
     "https://beta.seizeyouralpha.com/open/mmp/get-mmp-config/v1?indexName=BTCUSD"
}
```

> Response:

```json 
{
  "code": 0,
  "msg": "success",
  "i18nArgs": null,
  "data": {
    "id": 26,
    "uid": 1695796692726153,
    "indexName": "BTCUSD", //Index name
    "intervalTime": 5000, //Time interval, in milliseconds.
    "frozenTime": 5000, //Freeze interval
    "qtyLimit": 5000,  //Trade notional limit
    "deltaLimit": 10, //net trade delta limit
    "mmpFrozen": false,  //Indicates whether MMP is triggered: TRUE or FALSE.
    "mmpFrozenUntil": 2326882,  //If frozenTime is configured and mmpFrozen = true, this field represents the unfreeze timestamp (in milliseconds); otherwise, it is an empty string "".
    "ctime": "2025-04-24T06:37:37.000+00:00",
    "mtime": "2025-04-24T06:40:15.000+00:00"
  }
}

``` 


## Reset MMP Config (SIGNED) 

Reset MMP config (Once MMP is triggered, this API can be used to unfreeze it.)

**HTTP Request**  

`POST https://api.coincall.com/open/mmp/reset-mmp/v1`

**Parameter** 

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
instType | string	| OPTION	| FALSE	| Trading product type: OPTION (default is option)
indexName	| string	| BTCUSD	| TRUE	| indexName

> Request:

```json
{
    curl -X POST 
    -H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU="
    -H "sign: 5C43A5D221115018E2E9E11F0175CB889F810B7F7B816E96CC83604B14702B91" 
    -H "ts: 1745477573313" 
    -H "X-REQ-TS-DIFF: 5000" 
    -H "Content-Type: application/json" -d '{
            "instType":"OPTION",
            "indexName":"BTCUSD"
        }' "https://beta.seizeyouralpha.com/open/mmp/reset-mmp/v1"
}
```

> Response:

```json 
{
    "code":"0",
    "msg":"",
    "data":[
        {
            "result":true
        }
    ]
}


``` 

