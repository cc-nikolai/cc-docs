# RFQ Endpoint  
## Create RFQ(SIGNED)

Create RFQ

> Request:

```sh
curl -X POST 
-H "X-CC-APIKEY: cYW/BtS6YsMFZYvUA2pW+1FeFN4ceM+Wv0aS+PQc1hc=" 
-H "sign: D0E928B7322729CC6B0D4B0675206DD929B72B422A976F79D163BCD487AC139D" 
-H "ts: 1761633329230" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/json" 
-d '{
    "legs": [
        {
            "instrumentName": "BTCUSD-29OCT25-109000-C",
            "side": "BUY",
            "qty": "0.2"
        },
        {
            "instrumentName": "BTCUSD-29OCT25-109000-P",
            "side": "SELL",
            "qty": "0.2"
        }
    ]
}' "https://beta.seizeyouralpha.com/open/option/blocktrade/request/create/v1"
```

> Response:

```json
{
  "code": 0,
  "msg": "Success",
  "i18nArgs": null,
  "data": {
    "requestId": "1983060031318396928",
    "createTime": 1761633329597,
    "expiryTime": 1761636929597,
    "legs": [
      {
        "instrumentName": "BTCUSD-29OCT25-109000-C",
        "qty": "0.2",
        "side": "BUY"
      },
      {
        "instrumentName": "BTCUSD-29OCT25-109000-P",
        "qty": "0.2",
        "side": "SELL"
      }
    ],
    "state": "ACTIVE"
  }
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/blocktrade/request/create/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
legs | array of object |  | true | Json object
-> instrumentName | string | BTCUSD-13SEP24-56000-C | true | quote symbol
-> side | string | BUY OR SELL| true | trade side
-> qty | string | 10.1 | true | quote quantity

**Parameter Example** 

*RequestBody* 

{
    "legs": [
        {
            "instrumentName": "BTCUSD-29OCT25-109000-C",
            "side": "BUY",
            "qty": "0.2"
        },
        {
            "instrumentName": "BTCUSD-29OCT25-109000-P",
            "side": "SELL",
            "qty": "0.2"
        }
    ]
}

## Cancel RFQ by ID(SIGNED)

Cancel RFQ 

> Request:

```sh
curl -X POST 
-H "X-CC-APIKEY: cYW/BtS6YsMFZYvUA2pW+1FeFN4ceM+Wv0aS+PQc1hc=" 
-H "sign: C682166D0936C406AEDD4BC3DEEA278D59EBE5EB5220656E1871AB49F7CF6255" 
-H "ts: 1761650065385" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/x-www-form-urlencoded" 
-d 'requestId=1983130245586358272' "https://beta.seizeyouralpha.com/open/option/blocktrade/request/cancel/v1"

```

> Response:

```json
{
  "code": 0,
  "msg": "Success",
  "i18nArgs": null,
  "data": true
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/blocktrade/request/cancel/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
requestId | String | 1840685647012708354 | true | request ID

**Parameter Example**  

requestId=1978391652129181696



## Get Quotes Received(SIGNED)

Get RFQ quotes 


> Request:

```sh
curl -X GET 
-H "X-CC-APIKEY: cYW/BtS6YsMFZYvUA2pW+1FeFN4ceM+Wv0aS+PQc1hc=" 
-H "sign: 33F92DC129B7133F6772F977562FE1B08121D00839EBEB249E8F7575C0D737EB" 
-H "ts: 1761650261346" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/json" "https://beta.seizeyouralpha.com/open/option/blocktrade/request/getQuotesReceived/v1?requestId=1983130719395909632"
```

> Response:

```json
{
  "code": 0,
  "msg": null,
  "i18nArgs": null,
  "data": [
    {
      "quoteId": "1983131007357546497",
      "requestId": "1983130719395909632",
      "userId": "1695796692726153",
      "state": "OPEN",
      "createTime": 1761650251603,
      "updateTime": 1761650252000,
      "expiryTime": 1761650551603,
      "legs": [
        {
          "instrumentName": "BTCUSD-29OCT25-109000-C",
          "side": "SELL",
          "price": "1",
          "quantity": "0.2"
        },
        {
          "instrumentName": "BTCUSD-29OCT25-109000-P",
          "side": "BUY",
          "price": "2",
          "quantity": "0.2"
        }
      ]
    }
  ]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/blocktrade/request/getQuotesReceived/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
requestId |string | 198340374878321 | false | request RFQ ID



## Execute Quote(SIGNED)

The taker executes quote

> Request:

```sh
## Cancel RFQ by ID(SIGNED)

Cancel RFQ 

> Request:

```sh
curl -X POST 
-H "X-CC-APIKEY: cYW/BtS6YsMFZYvUA2pW+1FeFN4ceM+Wv0aS+PQc1hc=" 
-H "sign: F5551686049622DF067B4B93855D7EA6B6813E954131A684FA9EAF55D0743CFA" 
-H "ts: 1761650457177" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/x-www-form-urlencoded" 
-d 'requestId=1983130719395909632&quoteId=1983131007357546497' "https://beta.seizeyouralpha.com/open/option/blocktrade/request/accept/v1"

```

> Response:

```json
{
  "code": 0,
  "msg": "Success",
  "i18nArgs": null,
  "data": {
    "userId": null,
    "blockTradeId": "1983131007357546497",
    "requestId": "1983130719395909632",
    "quoteId": "1983131007357546497",
    "role": "TAKER",
    "legs": [
      {
        "instrumentName": "BTCUSD-29OCT25-109000-C",
        "baseToken": "BTC",
        "quoteToken": "USDT",
        "side": "BUY",
        "price": "1",
        "quantity": "0.2",
        "iv": "6.0E-4",
        "markPrice": "5365.90199481",
        "indexPrice": "109543.52",
        "orderId": "1983131927527428096",
        "tradeId": "1983131929700110336",
        "fee": "0.025000000",
        "createTime": 1761650471507,
        "profit": "0"
      },
      {
        "instrumentName": "BTCUSD-29OCT25-109000-P",
        "baseToken": "BTC",
        "quoteToken": "USDT",
        "side": "SELL",
        "price": "2",
        "quantity": "0.2",
        "iv": "0.3799",
        "markPrice": "18.06805125",
        "indexPrice": "109543.52",
        "orderId": "1983131927699394560",
        "tradeId": "1983131929729470464",
        "fee": "0",
        "createTime": 1761650471514,
        "profit": "0"
      }
    ]
  }
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/blocktrade/request/accept/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
requestId |String | 1983130719395909632 | true | request ID
quoteId|String| 1983131007357546497 | true| quote ID


**Parameter Example**  

seekId=1978394601173684224&blockTradeOrderId=1978394816938655746

```

> Response:

```json
{
  "code": 0,
  "msg": "Success",
  "i18nArgs": null,
  "data": true
}
```




## Get list of RFQs(SIGNED)

Get RFQ request list


> Request:

```sh
curl -X GET 
-H "X-CC-APIKEY: jV4mFZa4kBLczkrRfw77vcVSLfHc3Dm3wYyTG6RA58Y=" 
-H "sign: 73103DE66FA8D9CDB955F58442104E3B19B8552000B3B4E080903B7CFA764C01" 
-H "ts: 1756180090536" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " "https://beta.seizeyouralpha.com/open/option/blocktrade/rfqList/v1?requestId=123456789&state=OPEN&role=MAKER&startTime=1663490353000&endTime=1663490453000"
```

> Response:

```json
{
    "code": 0,                // API result code: 0 = success
    "msg": "Success",         // Response message
    "i18nArgs": null,         // Internationalization arguments (if any)
    "data":{
        "userId": "1695796692867071",
        "rfqList":[
            {
                "requestId": "1957272427713138688",
                "state": "ACTIVE", // CANCELLED | ACTIVE | FILLED | EXPIRED | TRADED_AWAY
                "role": "MAKER", // MAKER | TAKER
                "createTime": 1755485879163,
                "expiryTime": 1755485879163,
                "updateTime": 1755485879163,
                "legs":[{
                      "instrumentName": "BTCUSD-9AUG25-100000-C",
                      "side": "BUY",                    // Leg direction: BUY or SELL
                      "quantity": "10.5"
                },
                {
                      "instrumentName": "BTCUSD-9AUG25-100000-C",
                      "side": "SELL",                    // Leg direction: BUY or SELL
                      "quantity": "10.5"
                }]
            }
        ]
    }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/blocktrade/rfqList/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
requestId |string | 198340374878321 | false | request RFQ ID
state | string | OPEN, CLOSED| false | state of the rfq request
role  | string | TAKER, MAKER | false | user role
startTime | integer| 1725610332457 | false | Default to 3 days from current time
endTime | integer | 1725710332457 | false | Default to current time

## Create quote(SIGNED)

Create quote for RFQ

> Request:

```sh
curl -X POST 
-H "X-CC-APIKEY: jV4mFZa4kBLczkrRfw77vcVSLfHc3Dm3wYyTG6RA58Y=" 
-H "sign: 689C84E5EC2633337BFFE11D5622B07378CDDBE4F813BB6822990835FB6706EF" 
-H "ts: 1756180090536" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/json" 
-d '{
    "requestId": 1916777612861149201,
    "legs": [
        {
            "instrumentName": "BTCUSD-9AUG25-95000-C",
            "symbol": "BTCUSD",
            "side": "BUY",
            "price": "1250.75",
            "quantity": "10.5"
        },
        {
            "instrumentName": "BTCUSD-9AUG25-100000-C",
            "symbol": "BTCUSD",
            "side": "SELL",
            "price": "850.25",
            "quantity": "10.5"
        }
    ]
}' "https://beta.seizeyouralpha.com/open/option/blocktrade/quote/create/v1"
```

> Response:

```json
{
    "code": 0,                // API result code: 0 = success
    "msg": "Success",         // Response message
    "i18nArgs": null,         // Internationalization arguments (if any)
    "data":{
        "quoteId": "1957266294866329602",
        "requestId": "1916777612861149201",
        "createTime": 1755485875973,
        "updateTime": 1755485875973,
        "expiryTime": 1782460800000,
        "legs":[
            {
               "instrumentName": "BTCUSD-29AUG25-125000-C",
               "quantity": "0.1",
               "price": "22",
               "side": "BUY"
            }, 
            {
               "instrumentName": "BTCUSD-26JUN26-125000-C",
               "quantity": "0.1",
               "price": "123",
               "side": "SELL"
            }
        ]
    }
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/blocktrade/quote/create/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
requestId | integer | 1840685647012708354 | true | request RFQ ID.
legs | array of object |  | true | Json object
-> instrumentName | string | BTCUSD-13SEP24-56000-C | true | quote symbol
-> symbol | string | BTCUSD | true | symbol
-> price | string | 10.1 | true | quote price
-> side | string | BUY OR SELL| true | trade side
-> quantity | string | 10.1 | true | quote quantity

**Parameter Example** 

*RequestBody* 

{ 
    "requestId": 1916777612861149201, 
    "legs": [ 
        { 
            "instrumentName": "BTCUSD-9AUG25-95000-C", 
            "symbol": "BTCUSD", 
            "side": "BUY", 
            "price": "1250.75", 
            "quantity": "10.5" 
        }, 
        { 
            "instrumentName": "BTCUSD-9AUG25-100000-C", 
            "symbol": "BTCUSD", 
            "side": "SELL", 
            "price": "850.25", 
            "quantity": "10.5" 
        } 
    ] 
} 

## Cancel Quote by ID(SIGNED)

Cancel quote for RFQ

> Request:

```sh
curl -X POST 
-H "X-CC-APIKEY: jV4mFZa4kBLczkrRfw77vcVSLfHc3Dm3wYyTG6RA58Y=" 
-H "sign: 8C3BF7C0F9FA29905079503E18310FC4DB9A290E9BF64B96675D05CB6C5AECC0" 
-H "ts: 1756180090536" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/json" 
-d '{
        "quoteId": 1957266294866329602
     }
' "https://beta.seizeyouralpha.com/open/option/blocktrade/quote/cancel/v1"
```

> Response:

```json
{
    "code": 0,                // API result code: 0 = success
    "msg": "Success",         // Response message
    "i18nArgs": null,         // Internationalization arguments (if any)
    "data":{
        "quoteId": "1957266294866329602"
     }
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/blocktrade/quote/cancel/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
quoteId |integer | 1840685647012708354 | true | Quote ID

**Parameter Example**  

*requestBody:*  

{ 
 "quoteId": "1957266294866329602" 
}  


## Cancel All Quotes (SIGNED)

Cancel all quotes

> Request:

```sh
curl -X POST 
-H "X-CC-APIKEY: jV4mFZa4kBLczkrRfw77vcVSLfHc3Dm3wYyTG6RA58Y=" 
-H "sign: FD5B8FB3B09AD1B00E7193ABAA20EADEFCE7F5426A571FFC3E89048401025473" 
-H "ts: 1756180090536" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/x-www-form-urlencoded" 
-d '' "https://beta.seizeyouralpha.com/open/option/blocktrade/quote/cancel-all/v1"
```

> Response:

```json
{
    "code": 0,
    "msg": "Success",
    "i18nArgs": null,
    "data": null
}
```


**HTTP Request**

`POST https://api.coincall.com/open/option/blocktrade/quote/cancel-all/v1`



## Get List of Quotes(SIGNED)

Get user Quote records

> Request:

```sh
curl -X GET 
-H "X-CC-APIKEY: jV4mFZa4kBLczkrRfw77vcVSLfHc3Dm3wYyTG6RA58Y=" 
-H "sign: E3118A3D58827E3062B39B654F6B365DDC1FC1551AF5903E9C383972CAB3CA6C" 
-H "ts: 1756180090536" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/x-www-form-urlencoded" 
"https://beta.seizeyouralpha.com/open/option/blocktrade/list-quote/v1?requestId=123456&quoteId=123456&state=OPEN&symbol=ETHUSD&startTime=1755051650&endTime=1754792450000"
```

> Response:

```json
{
  "code": 0,
  "msg": "Success",
  "i18nArgs": null,
  "data": [
    {
      "quoteId": "1957269207860789249",
      "requestId": "1957268602021351424",
      "userId": "1695796693236896",
      "state": "OPEN", //OPEN | CANCEL | FILLED
      "createTime": 1755484318114,
      "updateTime": 1755513118000,
      "expiryTime": 1755484618114,
      "legs": [
        {
          "instrumentName": "ETHUSD-26SEP25-4400-C",
          "side": "BUY",
          "price": "4500",
          "quantity": "1"
        },
        {
          "instrumentName": "ETHUSD-29AUG25-4400-C",
          "side": "SELL",
          "price": "4600",
          "quantity": "1"
        }
      ]
    }
  ]
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/blocktrade/list-quote/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
quoteId |integer | 1840685647012708354 | false | Quote ID
requestId | integer | 1957268602021351424 | false | RFQ request ID
state   |string| OPEN,CLOSED| false| Default query all states
symbol |string|BTCUSD,ETHUSD | false |symbol name
startTime | integer | 1755484318114 | false| Default to 3 days from current time
endTime | integer | 1755484618114 | false | Default to current time



## Get List of Private Trades(SIGNED)

Get user RFQ trades

> Request:

```sh
curl -X GET 
-H "X-CC-APIKEY: jV4mFZa4kBLczkrRfw77vcVSLfHc3Dm3wYyTG6RA58Y=" 
-H "sign: 5DB15133873C1CF10FF38D01AC7CB897D1013998E646448C537F5F552BFF0095" 
-H "ts: 1756180090536" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: application/x-www-form-urlencoded" 
"https://beta.seizeyouralpha.com/open/option/blocktrade/orderList/v1?blocktradeId=1347832697683&direction=NEXT&pageSize=20"
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
        "blocktradeId": "123456789",   
        "requestId": "24601",  // rqf request id if any
        "symbol": "BTCUSD-16MAY25-95000-C",
        "baseToken": "BTC",
        "quoteToken": "USDT", 
        "side": "BUY", // trade side, 1 buy, 2 sell
        "price": "2053",
        "qty": "20",
        "iv": "0.4162",
        "markPrice": "2052.3415235",
        "indexPrice": "94475.478875",
        "orderId": "1919971058081992700",
        "tradeId": "1919971552670163000",
        "fee": "850.27930988",
        "createTime": 1746591864166,
        "profit": "0",
        "role": "MAKER"
      },
      {
        "blocktradeId": "123456799",   
        "requestId": "24602", 
        "symbol": "BTCUSD-9MAY25-95000-C",
        "displayName": "BTC-9MAY25-95000-C",
        "baseToken": "BTC",
        "quoteToken": "USDT",
        "side": "SELL",
        "price": "111",
        "qty": "10",
        "iv": "0.0327",
        "markPrice": "2564.19894087",
        "indexPrice": "87569.71888889",
        "orderId": "1916776089900945400",
        "tradeId": "1916777612844372000",
        "fee": "138.75",
        "createTime": 1745830369569,
        "profit": "-8792.21",
        "role": "MAKER"
      },
    "hasNext": false,
    "hasPrev": true
  }
}

```


**HTTP Request**

`GET https://api.coincall.com/open/option/blocktrade/orderList/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
blocktradeId |integer | 1840685647012708354 | false | Private endpoint, user can only see own trades
fromId | integer | 1957268602021351424 | false | RFQ blocktradeId
direction   |string| NEXT,PREV| false| Default is NEXT
pageSize | integer | 20 | false| The value should be less than 500. Default: 20
currency | string | BTC,ETh | false | Query currency type


## Get List of RFQ Private Trades(SIGNED)

Get user private RFQ trades

> Request:

```sh
curl -X GET 
-H "X-CC-APIKEY: sf7D2eLvr+931g/mMugcbhdpwJIQWo+GncQr4rU19vA=" 
-H "sign: 3ABF3EEEE221FEE9CCF90AAE31BE1478F8E072ED9BD645221981FFB80E5A9134" 
-H "ts: 1768812827993" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " "https://beta.seizeyouralpha.com/open/option/blocktrade/trade-detail/private/v1?symbol=BTCUSD&fromId=0&pageSize=2"
```

> Response:

```json
{
  "code": 0,
  "msg": null,
  "i18nArgs": null,
  "data": {
    "list": [
      {
        "requestId": "2012860195142766592",
        "tradeSide": "BUY",
        "strategyPrice": "112.00000000",
        "strategyQuantity": "0.10000000",
        "description": "BTC Call Butterfly 23 Jan 26 95000/96000/97000",
        "strategyName": "Call Butterfly",
        "legs": [
          {
            "baseToken": "BTC",
            "createTime": 1768738265283,
            "indexPrice": "90682.04000000",
            "instrumentName": "BTCUSD-23JAN26-97000-C",
            "iv": "0.3642",
            "markPrice": "805.38458599",
            "price": "805.00000000",
            "quantity": "0.10000000",
            "quoteToken": "USDT",
            "side": "BUY",
            "tradeId": "2012860291485966336",
            "fee": "10.06250000",
            "orderId": "2012860288822546432",
            "profit": "0",
            "reduceOnly": null
          },
          {
            "baseToken": "BTC",
            "createTime": 1768738265277,
            "indexPrice": "90682.04000000",
            "instrumentName": "BTCUSD-23JAN26-96000-C",
            "iv": "0.3647",
            "markPrice": "1147.49001880",
            "price": "1149.00000000",
            "quantity": "0.20000000",
            "quoteToken": "USDT",
            "side": "SELL",
            "tradeId": "2012860291460800512",
            "fee": "0.00000000",
            "orderId": "2012860288742854656",
            "profit": "0",
            "reduceOnly": null
          },
          {
            "baseToken": "BTC",
            "createTime": 1768738265271,
            "indexPrice": "90682.04000000",
            "instrumentName": "BTCUSD-23JAN26-95000-C",
            "iv": "0.3694",
            "markPrice": "1604.81214548",
            "price": "1605.00000000",
            "quantity": "0.10000000",
            "quoteToken": "USDT",
            "side": "BUY",
            "tradeId": "2012860291435634688",
            "fee": "20.06250000",
            "orderId": "2012860288658968576",
            "profit": "0",
            "reduceOnly": null
          }
        ],
        "createTime": 1768738264776,
        "userId": "1695796693211199",
        "blockTradeId": "2012860289361002497",
        "quoteId": "2012860289361002497",
        "role": "TAKER"
      }
    ],
    "hasNext": true,
    "hasPrev": false
  }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/option/blocktrade/trade-detail/private/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
blocktradeId |integer | 1840685647012708354 | false | block trade id
fromId | integer | 1957268602021351424 | false | RFQ blocktradeId used for query comparison default 0
direction   |string| NEXT,PREV| false| Default is NEXT
pageSize | integer | 20 | false| The value should be less than 50. Default: 20
symbol | string | BTCUSD,ETHUSD | false | symbol name of option
 


## Get List of RFQ Public Trades(SIGNED)

Get public RFQ trades Info

> Request:

```sh
curl -X GET 
-H "X-CC-APIKEY: sf7D2eLvr+931g/mMugcbhdpwJIQWo+GncQr4rU19vA=" 
-H "sign: 67DC07EE12FEC4A792ACF5DCF4172604076E402AE340EC7B51FF6E5DB94E4CD2" 
-H "ts: 1768812346092" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " "https://beta.seizeyouralpha.com/open/option/blocktrade/trade-detail/public/v1?symbol=BTCUSD&fromId=0&pageSize=2"
```

> Response:

```json
{
  "code": 0,
  "msg": null,
  "i18nArgs": null,
  "data": {
    "list": [
      {
        "requestId": "2012860195142766592",
        "tradeSide": "BUY",
        "strategyPrice": "112.00000000",
        "strategyQuantity": "0.10000000",
        "description": "BTC Call Butterfly 23 Jan 26 95000/96000/97000",
        "strategyName": "Call Butterfly",
        "legs": [
          {
            "baseToken": "BTC",
            "createTime": 1768738265283,
            "indexPrice": "90682.04000000",
            "instrumentName": "BTCUSD-23JAN26-97000-C",
            "iv": "0.3642",
            "markPrice": "805.38458599",
            "price": "805.00000000",
            "quantity": "0.10000000",
            "quoteToken": "USDT",
            "side": "BUY",
            "tradeId": "2012860291485966336"
          },
          {
            "baseToken": "BTC",
            "createTime": 1768738265277,
            "indexPrice": "90682.04000000",
            "instrumentName": "BTCUSD-23JAN26-96000-C",
            "iv": "0.3647",
            "markPrice": "1147.49001880",
            "price": "1149.00000000",
            "quantity": "0.20000000",
            "quoteToken": "USDT",
            "side": "SELL",
            "tradeId": "2012860291460800512"
          },
          {
            "baseToken": "BTC",
            "createTime": 1768738265271,
            "indexPrice": "90682.04000000",
            "instrumentName": "BTCUSD-23JAN26-95000-C",
            "iv": "0.3694",
            "markPrice": "1604.81214548",
            "price": "1605.00000000",
            "quantity": "0.10000000",
            "quoteToken": "USDT",
            "side": "BUY",
            "tradeId": "2012860291435634688"
          }
        ],
        "createTime": 1768738264776
      },
      {
        "requestId": "2012858573230575616",
        "tradeSide": "SELL",
        "strategyPrice": "1147.00000000",
        "strategyQuantity": "0.10000000",
        "description": "BTC Call 23 Jan 26 96000",
        "strategyName": "Call",
        "legs": [
          {
            "baseToken": "BTC",
            "createTime": 1768737895819,
            "indexPrice": "90682.04000000",
            "instrumentName": "BTCUSD-23JAN26-96000-C",
            "iv": "0.3616",
            "markPrice": "1151.43744045",
            "price": "1147.00000000",
            "quantity": "0.10000000",
            "quoteToken": "USDT",
            "side": "SELL",
            "tradeId": "2012858741841629184"
          }
        ],
        "createTime": 1768737895480
      }
    ],
    "hasNext": true,
    "hasPrev": false
  }
}

```


**HTTP Request**

`GET https://api.coincall.com/open/option/blocktrade/trade-detail/public/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
blocktradeId |integer | 1840685647012708354 | false | block trade id
fromId | integer | 1957268602021351424 | false | RFQ blocktradeId used for query comparison default 0
direction   |string| NEXT,PREV| false| Default is NEXT
pageSize | integer | 20 | false| The value should be less than 50. Default: 20
symbol | string | BTCUSD,ETHUSD | false |  symbol name of option


## Create (SIGNED)

Create block trade

**HTTP Request**  

`POST https://api.coincall.com/open/option/blockTrade/create/v1`

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

Accept block trade

**HTTP Request**  

`POST https://api.coincall.com/open/option/blockTrade/accept/v1`

**Parameter** 

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
key | 	String | 	eyJyb2xlIjowLCJzaWduYXR1cmUiOiJbe1wiYnV5XCI6dHJ1ZSxcImNMb3NlXCI6ZmFsc2UsXCJjbGllbnRPcmRlcklkXCI6MTkyMDAyNTQwNTgzMDU5ODY1NixcImNsb3NlVHlwZVwiOjA	| true	 |  Block trade code 
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



