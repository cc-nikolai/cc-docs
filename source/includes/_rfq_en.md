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
requestId |integer | 1840685647012708354 | true | request RFQ ID.
orderOpenApiDetailReqs | string | 10 | true | Json Map
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