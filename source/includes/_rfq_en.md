# RFQ
## Board list(SIGNED)

Get board list

> Response:

```json
{
    "code": 0,
    "msg": "Success",
    "i18nArgs": null,
    "data": {
        "requestList": [
            {
                "legList": [ // per request list
                    {
                        "type": 1, // trade type, 1 options, 2 futures, 3 spot
                        "tradeSide": 1, // trade side, 1 buy, 2 sell
                        "symbol": "BTCUSD-11OCT24-65000-C",
                        "amount": 0.5 // trade size
                    }
                ],
                "requestId": 1840600952218980352, // this request ID
                "expireTime": 1727670238401
            },
            {
                "legList": [
                    {
                        "type": 1,
                        "tradeSide": 1,
                        "symbol": "BTCUSD-13SEP24-56000-C",
                        "amount": 0.1
                    },
                    {
                        "type": 1,
                        "tradeSide": 1,
                        "symbol": "BTCUSD-20SEP24-56000-P",
                        "amount": 0.1
                    }
                ],
                "requestId": 1831961206433386496,
                "expireTime": 1725610362477
            }
        ],
        "currentPage": 1,
        "pageTotal": 1,
        "total": 2
    }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/blockTrade/seek/list/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
currentPage |integer | 1 | true | No default.
pageSize | integer | 10 | true | No default, max size is 1500

## Create quote(SIGNED)

Creates quote for RFQ

> Response:

```json
{
    "code": 0,
    "msg": null,
    "i18nArgs": null,
    "data": 1840685647012708354 // Quote ID
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/blockTrade/quote/create/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
requestId | integer | 1840685647012708354 | true | request RFQ ID.
orderOpenApiDetailReqs | string |  | true | Json Map
-> price | string | 10.1 | true | quote price
-> symbol | string | BTCUSD-13SEP24-56000-C | true | quote symbol
-> type | string | 1 | true | 1 Options, 2 Futures, 3 Spot

**Parameter Example**

body = {
            {'orderOpenApiDetailReqs': '[{"price":"2000","symbol":"BTCUSD-11OCT24-65000-C","type":"1"},{"price":"1000","symbol":"BTCUSD-11OCT24-60000-C","type":"1"}]', 
            'requestId': 1840600952218980352}
        }

## Cancel quote(SIGNED)

Cancel quote for RFQ

> Response:

```json
{
    "code": 0,
    "msg": "Success",
    "i18nArgs": null,
    "data": 1840685647012708354
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/blockTrade/quote/cancel/v1/{quoteId}`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
quoteId |integer | 1840685647012708354 | true | Quote ID


## Create (SIGNED)

Create block trade

**HTTP Request**  

`GET https://api.coincall.com/open/option/blockTrade/create/v1`

**Parameter** 

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
symbol | 	String | 	BTCUSD	|true	 |  symbol
orderList | String | [{"optionName":"BTCUSD-16MAY25-95000-C","contractId":1,"tradeType":1,"expiryDate":1747353600000,"strike":95000,"type":1,"tradeSide":1,"price":2036,"amount":10}] | true |   RFQ order info
role | Number | 0 | true | user role : 1.taker 0.maker
marginMode | Number | 2 | true |margin mode  1.SM 2.PM 3.MULTICURRENCY

> Request:

```json
{
curl -X POST 
-H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU=" 
-H "sign: A4B630A75F093D600F49A69BF4A79B25F3F9A04D3B54E598931F94B279DBF663" 
-H "ts: 1746604694445" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/x-www-form-urlencoded"
--data-raw 'symbol=BTCUSD&orderList=%5B%7B%22optionName%22%3A%22BTCUSD-16MAY25-95000-C%22%2C%22contractId%22%3A1%2C%22tradeType%22%3A1%2C%22expiryDate%22%3A1747353600000%2C%22strike%22%3A95000%2C%22type%22%3A1%2C%22tradeSide%22%3A1%2C%22price%22%3A2036%2C%22amount%22%3A10%7D%5D%0D%0A&role=0&marginMode=2'
"https://beta.seizeyouralpha.com/open/option/blockTrade/create/v1" 
}
```

> Response:

```json 
{
  "code": 0,
  "msg": null,
  "i18nArgs": null,
  "data":   // Block trade Code
"eyJyb2xlIjowLCJzaWduYXR1cmUiOiJbe1wiYnV5XCI6dHJ1ZSxcImNMb3NlXCI6ZmFsc2UsXCJjbGllbnRPcmRlcklkXCI6MTkyMDAyNTQwNTgzMDU5ODY1NixcImNsb3NlVHlwZVwiOjAsXCJjcmVhdGVUaW1lXCI6MTc0NjYwNDcwMzc1NCxcImRlYWxUeXBlXCI6MCxcImRlbGV0ZWRcIjowLFwiZW5kVGltZVwiOjE3NDczODI0MDAwMDAsXCJleHRcIjpcIntcXFwic29ydFxcXCI6XFxcIjFcXFwifVwiLFwiZmlsbFZvbHVtZVwiOjAsXCJmcmVlSW1Wb2x1bWVcIjowLFwiZnJvemVuRmVlXCI6NDI1LjEzOTY1NDk0MCxcImZyb3plblZvbHVtZVwiOjEwLFwiaW1DYWxjVm9sdW1lXCI6MTAsXCJvcHRpb25JZFwiOjE5MTUzMTUwMjU1ODU3NzQ2NjIsXCJvcHRpb25OYW1lXCI6XCJCVENVU0QtMTZNQVkyNS05NTAwMC1DXCIsXCJvcmRlcklkXCI6MTkyMDAyNTQwNTgzMDU5ODY1NixcInBlbmRpbmdWb2x1bWVcIjoxMCxcInByaWNlXCI6MjAzNixcInNlbGxcIjpmYWxzZSxcInN0YXRlXCI6MCxcInN0cmlrZVwiOjk1MDAwLjAwMDAwMDAwLFwidHJhZGVTaWRlXCI6MSxcInRyYWRlU3RyYXRlZ3lcIjowLFwidHJhZGVUeXBlXCI6MTQsXCJ1bmRlclN5bWJvbFwiOlwiQlRDVVNEXCIsXCJ1cGRhdGVUaW1lXCI6MTc0NjYwNDcwMzc1NCxcInVzZXJJZFwiOjE2OTU3OTY2OTI3MjYxNTMsXCJ2b2x1bWVcIjoxRSsxfV0iLCJzeW1ib2wiOiJCVENVU0QiLCJ0aW1lc3RhbXAiOjE3NDY2MDQ3MDM4MDUsInRyYWRlcyI6W3siYW1vdW50IjoxMCwiZXhwaXJ5RGF0ZSI6MTc0NzM1MzYwMDAwMCwib3B0aW9uTmFtZSI6IkJUQ1VTRC0xNk1BWTI1LTk1MDAwLUMiLCJwcmljZSI6MjAzNiwic29ydCI6MSwic3RyaWtlIjo5NTAwMCwidHJhZGVTaWRlIjoxLCJ0cmFkZVR5cGUiOjEsInR5cGUiOjF9XSwidXNlcklkIjoxNjk1Nzk2NjkyNzI2MTUzfQ=="
}

``` 

## Accept (SIGNED)

Create block trade

**HTTP Request**  

`GET https://api.coincall.com/open/option/blockTrade/accept/v1`

**Parameter** 

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
key | 	String | 	eyJyb2xlIjowLCJzaWduYXR1cmUiOiJbe1wiYnV5XCI6dHJ1ZSxcImNMb3NlXCI6ZmFsc2UsXCJjbGllbnRPcmRlcklkXCI6MTkyMDAyNTQwNTgzMDU5ODY1NixcImNsb3NlVHlwZVwiOjA	| true	 |  Block trade code 
role | Number | 1 | true |   RFQ order info
role | Number | 0 | true | user role : 1.taker 0.maker
marginMode | Number | 2 | true | margin mode  1.SM 2.PM 3.MULTICURRENCY

> Request:

```json
{
curl -X POST 
-H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU="
-H "sign: B03DE9E5353B5C32F60C6CC5B633B1F3F78D03D9472E1336423A7348D8BA1871" 
-H "ts: 1746609528249" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/json" 
-d '{"key":"eyJyb2xlIjowLCJzaWduYXR1cmUiOiJbe1wiYnV5XCI6dHJ1ZSxcImNMb3NlXCI6ZmFsc2UsXCJjbGllbnRPcmRlcklkXCI6MTkyMDAyNTQwNTgzMDU5ODY1NixcImNsb3NlVHlwZVwiOjAsXCJjcmVhdGVUaW1lXCI6MTc0NjYwNDcwMzc1NCxcImRlYWxUeXBlXCI6MCxcImRlbGV0ZWRcIjowLFwiZW5kVGltZVwiOjE3NDczODI0MDAwMDAsXCJleHRcIjpcIntcXFwic29ydFxcXCI6XFxcIjFcXFwifVwiLFwiZmlsbFZvbHVtZVwiOjAsXCJmcmVlSW1Wb2x1bWVcIjowLFwiZnJvemVuRmVlXCI6NDI1LjEzOTY1NDk0MCxcImZyb3plblZvbHVtZVwiOjEwLFwiaW1DYWxjVm9sdW1lXCI6MTAsXCJvcHRpb25JZFwiOjE5MTUzMTUwMjU1ODU3NzQ2NjIsXCJvcHRpb25OYW1lXCI6XCJCVENVU0QtMTZNQVkyNS05NTAwMC1DXCIsXCJvcmRlcklkXCI6MTkyMDAyNTQwNTgzMDU5ODY1NixcInBlbmRpbmdWb2x1bWVcIjoxMCxcInByaWNlXCI6MjAzNixcInNlbGxcIjpmYWxzZSxcInN0YXRlXCI6MCxcInN0cmlrZVwiOjk1MDAwLjAwMDAwMDAwLFwidHJhZGVTaWRlXCI6MSxcInRyYWRlU3RyYXRlZ3lcIjowLFwidHJhZGVUeXBlXCI6MTQsXCJ1bmRlclN5bWJvbFwiOlwiQlRDVVNEXCIsXCJ1cGRhdGVUaW1lXCI6MTc0NjYwNDcwMzc1NCxcInVzZXJJZFwiOjE2OTU3OTY2OTI3MjYxNTMsXCJ2b2x1bWVcIjoxRSsxfV0iLCJzeW1ib2wiOiJCVENVU0QiLCJ0aW1lc3RhbXAiOjE3NDY2MDQ3MDM4MDUsInRyYWRlcyI6W3siYW1vdW50IjoxMCwiZXhwaXJ5RGF0ZSI6MTc0NzM1MzYwMDAwMCwib3B0aW9uTmFtZSI6IkJUQ1VTRC0xNk1BWTI1LTk1MDAwLUMiLCJwcmljZSI6MjAzNiwic29ydCI6MSwic3RyaWtlIjo5NTAwMCwidHJhZGVTaWRlIjoxLCJ0cmFkZVR5cGUiOjEsInR5cGUiOjF9XSwidXNlcklkIjoxNjk1Nzk2NjkyNzI2MTUzfQ==","role":1,"marginMode":2}' "https://beta.seizeyouralpha.com/open/option/blockTrade/accept/v1"
}
```

> Response:

```json 
{"code":0,"msg":null,"i18nArgs":null,"data":"success"}

``` 


## Get Trade details (SIGNED)

Get RFQ Order Trade details.

**HTTP Request**  

`GET https://api.coincall.com/open/option/blockTrade/orderList/v1`

**Parameter** 

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
fromId | 	Number | 	1919971554599542784	|false	 | id
direction | String | NEXT | false |  direction: PREV or NEXT， Default: NEXT
pageSize | Number | 20 | false | pageSize:  The value should be less than 500, Default: 20
currency | String | BTC | false | Query currency type

> Request:

```json
{
curl -X GET 
-H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU=" 
-H "sign: 586509A6723EC934ED23F760571D8DAA9491F4136073E7FFE2BD33AEE3E0C825" 
-H "ts: 1746600242769"
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " 
"https://beta.seizeyouralpha.com/open/option/blockTrade/orderList/v1?fromId=1919971554599542784&direction=NEXT&pageSize=20&currency=BTC"
}
```

> Response:

```json 
{
  "code": 0,
  "msg": "Success",
  "i18nArgs": null,
  "data": {
    "list": [
      {
        "id": 1919971552695328800,
        "optionId": null,
        "symbol": "BTCUSD-16MAY25-95000-C",
        "displayName": "BTC-16MAY25-95000-C",
        "baseToken": "BTC",
        "quoteToken": "USDT", 
        "tradeSide": 1, // trade side, 1 buy, 2 sell
        "tradeType": 14,
        "price": 2053,
        "qty": 20,
        "iv": 0.4162,
        "markPrice": 2052.3415235,
        "indexPrice": 94475.478875,
        "orderId": 1919971058081992700,
        "clientOrderId": 1919971058081992700,
        "tradeId": 1919971552670163000,
        "fee": 850.27930988,
        "time": 1746591864166,
        "reduceOnly": null,
        "isTaker": 0,
        "profit": "0",
        "dealValue": 1889509.5775,
        "dealValueUnit": "USDT",
        "nlDisplayName": null
      },
      {
        "id": 1916777612861149200,
        "optionId": null,
        "symbol": "BTCUSD-9MAY25-95000-C",
        "displayName": "BTC-9MAY25-95000-C",
        "baseToken": "BTC",
        "quoteToken": "USDT",
        "tradeSide": 2,
        "tradeType": 14,
        "price": 111,
        "qty": 10,
        "iv": 0.0327,
        "markPrice": 2564.19894087,
        "indexPrice": 87569.71888889,
        "orderId": 1916776089900945400,
        "clientOrderId": 1916776089900945400,
        "tradeId": 1916777612844372000,
        "fee": 138.75,
        "time": 1745830369569,
        "reduceOnly": null,
        "isTaker": 0,
        "profit": "-8792.21",
        "dealValue": 875697.1888889,
        "dealValueUnit": "USDT",
        "nlDisplayName": null
      },
    "hasNext": false,
    "hasPrev": true
  }
}

``` 


