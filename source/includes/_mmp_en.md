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

> Response:

```json 
{
  "code": "0",
  "msg": "",
  "data": [
    {
        "indexName":"BTC-USD",   //Index names, such as BTCUSD and ETHUSD.
        "intervalTime":"5000",   //Time interval, in milliseconds. "0" - disables MMP. The default is "0". To enable MMP, set a value within the range [1000, 1000000000].
        "frozenTime":"5000",    //Freeze interval, in milliseconds. "0" means the state remains frozen until the "Reset MMP Status" API is called to unfreeze it.For non-permanent freeze, set a value within the range [1000, 1000000000]
        "qtyLimit": "5000",   //Trade notional limit, must be greater than 0. Valid range: ≥ 0.01.
        "deltaLimit": "10"    //Net trade delta limit, must be greater than 0.Valid range: ≥ 0.01.
    }
  ]
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

> Response:

```json 
{
  "code": "0",
  "data": [
    {
      "indexName":"BTC-USD",      //Index name
      "mmpFrozen": true,          //Indicates whether MMP is triggered: TRUE or FALSE.
      "mmpFrozenUntil": "2326882", //If frozenTime is configured and mmpFrozen = true, this field represents the unfreeze timestamp (in milliseconds); otherwise, it is an empty string "".
      "intervalTime":"5000", //Time interval, in milliseconds.
      "frozenTime":"5000",   //Freeze interval
      "qtyLimit": "5000",  //Trade notional limit
      "deltaLimit": "10"  //et trade delta limit
    }
  ],
  "msg": ""
}

``` 


## Reset MMP Config (SIGNED) 

Reset MMP config.

**HTTP Request**  

`POST https://api.coincall.com/open/mmp/reset-mmp/v1`

**Parameter** 

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
instType | string	| OPTION	| FALSE	| Trading product type: OPTION (default is option)
indexName	| string	| BTCUSD	| TRUE	| indexName

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

