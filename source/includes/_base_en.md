# Coincall API v2.0.1
# Overview

Welcome to the Coincall API! You can use our API to access Coincall  Open API endpoints.

## General Information

* Some endpoints will require an API Key to access. Please refer to this page to setup API Key.
* Base endpoint for REST: **https://api.coincall.com**
* While setting API Key, it is recommended to set IP access whitelist for security.
* Never share your API Key/Secret with anyone.
* The default permission of newly created API is read-only.
* Endpoint returns a JSON object.
* All time and timestamp related fields are in **milliseconds**.

## Working with Endpoints

* For `GET`endpoints, parameters must be sent as a `query string`.
* For `POST` endpoints, send parameters with the `Content-Type` documented for that endpoint. Most order endpoints use `application/json`; some signed endpoints use `application/x-www-form-urlencoded`.
* Parameters may be sent in any order.
* Because the API system is asynchronous, it is normal and expected that there will be a delay in the returned data.

## Rate Limits
<aside class="notice">
    Coincall has the right to further tighten the rate limits on users with intent to attack.
</aside>
  
Endpoint | Rate Limit | Rule
-------------- | -------------- | -------------- 
Get Public Configuration | 10 / 2s | per IP address and product
Get Funding Rate | 10 / 2s | per IP address
Get Position / Open Orders | 5 / 1s | per User ID
Get Historical Order / Transactions | 5 / 1s | per User ID
Get Account Information | 2 / 1s | per User ID
Get Orderbook | 30 / 2s | per User ID
Place Order | 30 / 2s | per User ID
Cancel Order | 30 / 2s | per User ID
Get Pending Order | 5 / 1s | per User ID

<aside class="notice">
    It is strongly recommended to use websocket stream for getting data as much as possible, which can not only ensure the timeliness of the message, but also reduce the access restriction pressure caused by the request.
</aside>

## Authentication

### API Resources

If you have any API related issues, please contact `api@coincall.com`.

* [Python SDK](https://github.com/CoincallExchange/coincall-python-sdk)

### Generating API Keys

[Create an API Key](https://www.coincall.com/account/apikeys) on the website before signing any requests. After creating an APIKey, keep the following information safe:

* APIKey
* APISecret

The system returns randomly-generated APIKeys and APISecrets. We cannot recover the APISecrets if you have lost it. You will need to create a new set of APIKey.

ApiKeys and apiSecret **are case sensitive**.

There are two permissions below that can be associated with an API key. One or more permission can be assigned to any key.

<p>Read-Only - Can request and view public info such as public configurations.</p>
<p>Trade - Can place and cancel orders, and request and view account info such as bills and history.</p>

<aside class="notice">
    Each APIKey can be linked with up to 20 IP addresses, APIKey can be created for one user up to 20 API Keys.
</aside>

### Endpoint Security Type

* Each endpoint has a security type that determines how you will interact with it.
* Security type is stated next to the NAME of the endpoint. If no security type is stated, assume the security type is `NONE`.


Security Type | Description
------------ | ------------
NONE | Endpoint can be accessed freely.
SIGNED | Requires valid API-Key and Signed.

### Making Requests

All private REST requests must contain the following headers:

* `X-CC-APIKEY` The API Key as a String.
* `sign` The Hex-encoded signature (see Signing Messages subsection for details).
* `ts` The timestamp of your request .e.g : 1688436087184
* `X-REQ-TS-DIFF` sent to specify the number of milliseconds after `ts` the request is valid for. If `X-REQ-TS-DIFF` is not sent, **it defaults to 5000**.

Request bodies must match the documented endpoint `Content-Type`. For JSON endpoints, send valid compact JSON. For form endpoints, send `application/x-www-form-urlencoded` form fields.

```javascript
  if (timestamp < (serverTime + 1000) && (serverTime - timestamp) <= X-REQ-TS-DIFF) {
    // process request
  } else {
    // reject request
  }
```

**Serious trading is about timing.** 

Networks can be unstable and unreliable, which can lead to requests taking varying amounts of time to reach the servers. With `X-REQ-TS-DIFF`, you can specify that the request must be processed within a certain number of milliseconds or be rejected by the server.

<aside class="notice">
    It is recommended to use a `X-REQ-TS-DIFF` of 5000 or less.
</aside>

### Signature

**Sign Procedures:**

* Build a parameter map from the values that will be sent in the request. For `GET`, use query parameters. For `application/json`, flatten the top-level JSON fields. For `application/x-www-form-urlencoded`, use the form fields.
* Remove fields whose value is `null`.
* Serialize nested objects and arrays as compact JSON, without extra spaces.
* Sort parameters alphabetically by parameter name and join them as `key=value` pairs with `&`.
* Append the authentication fields `uuid`, `ts`, and `x-req-ts-diff` to the signing string.
* The prehash format is `METHOD + path + ? + sorted_params + &uuid=...&ts=...&x-req-ts-diff=...`. If the request has no parameters, use `METHOD + path + ?uuid=...&ts=...&x-req-ts-diff=...`.
* Sign the prehash string with the API secret using HMAC SHA256.
* Encode the signature in hex and send it in uppercase.

***Examples:***
**The following API key and secret are for demonstration purposes only**

key               | value
----------------- | ---------------------------------------------
apiKey(uuid)      | xdtHWn32rsuDQConutzl9JDZB+Y1leitFl356YHrmts=
secretKey         | fce1102b2a0dea92957fa7d2e981df826295cd85696e40f0d521a6b8707b94c8

**HMAC SHA256 Signature Calculation Principle**

`sign=hmac.new(your_api_secret.encode("utf-8"), your_prehash_string.encode("utf-8"), hashlib.sha256).hexdigest().upper()`

**Example 1: GET with query parameters**

* requestMethod:
      GET
* uri:
      /open/futures/leverage/current/v1
* queryString:
      symbol=BTCUSD
* prehashString:
`GET/open/futures/leverage/current/v1?symbol=BTCUSD&uuid=xdtHWn32rsuDQConutzl9JDZB+Y1leitFl356YHrmts=&ts=1688436087184&x-req-ts-diff=3000`

**Example 2: GET with no parameters**

* requestMethod:
      GET
* uri:
      /open/user/info/v1
* prehashString:
`GET/open/user/info/v1?uuid=xdtHWn32rsuDQConutzl9JDZB+Y1leitFl356YHrmts=&ts=1688436087184&x-req-ts-diff=3000`

**Example 3: POST with JSON body**

* requestMethod:
      POST
* uri:
      /open/option/order/batchCreate/v1
* contentType:
      application/json
* requestBody:
      {"name":"mike","orders":[{"clientOrderId":212112212112,"symbol":"BTCUSD-10JAN25-89000-C","tradeSide":1,"price":1,"qty":0.1,"timeInForce":"GTC","stp":null,"tradeType":1},{"clientOrderId":212112212113,"symbol":"BTCUSD-10JAN25-89000-C","tradeSide":1,"price":1,"qty":0.1,"timeInForce":"GTC","stp":1,"tradeType":1}]}
* prehashString:
      POST/open/option/order/batchCreate/v1?name=mike&orders=[{"clientOrderId":212112212112,"symbol":"BTCUSD-10JAN25-89000-C","tradeSide":1,"price":1,"qty":0.1,"timeInForce":"GTC","tradeType":1},{"clientOrderId":212112212113,"symbol":"BTCUSD-10JAN25-89000-C","tradeSide":1,"price":1,"qty":0.1,"timeInForce":"GTC","stp":1,"tradeType":1}]&uuid=xdtHWn32rsuDQConutzl9JDZB+Y1leitFl356YHrmts=&ts=1688436087184&x-req-ts-diff=3000

**Example 4: POST with form body**

* requestMethod:
      POST
* uri:
      /open/user/subAccount/fund/transfer/v1
* contentType:
      application/x-www-form-urlencoded
* formBody:
      fromUserId=1695796692726153&toUserId=1695796692779320&currency=USDT&amount=111
* prehashString:
      POST/open/user/subAccount/fund/transfer/v1?amount=111&currency=USDT&fromUserId=1695796692726153&toUserId=1695796692779320&uuid=xdtHWn32rsuDQConutzl9JDZB+Y1leitFl356YHrmts=&ts=1688436087184&x-req-ts-diff=3000

**Attentions:**

    The timestamp value is the same as the `ts` header with UNIX millisecond timestamp of when the request was created and sent, e.g. 1688436087184

    The request `method` should be in UPPERCASE: e.g. `GET` and `POST`.

    The `uri` is the path of requesting an endpoint, not the full URL.

    <aside class="notice">
        GET request parameters are counted as uri query parameters, not body fields.
    </aside>

    Your API Secret is generated when you create an APIKey.

    For signed POST requests, sort the request parameter fields and remove null values before signature calculation.


## Field Type Enumeration

Name | Product | Note
---- | ------- | ----
type | options | Option order type: 1 CALL, 2 PUT
tradeSide | options/futures/websocket | Trade side: 1 BUY, 2 SELL
tradeType | options/futures/websocket | Trade type: 1 LIMIT, 2 MARKET, 3 POST_ONLY, 4 STOP_LIMIT,5 STOP_MARKET, 14 BLOCK_TRADE
reduceOnly | options/futures/websocket | Reduce only: 0 FALSE, 1 TRUE
state | options/websocket | Order status: -10 ILLEGAL, -1 PRE, 0 NEW, 1 FILLED, 2 PARTIALLY_FILLED, 3 CANCELED, 4 PRE_CANCEL, 5 CANCELING, 6 INVALID, 10 CANCEL_BY_EXERCISE
state | futures/websocket | Order status: -2 WAITING_EFFECT, -1 PRE, 0 NEW, 1 FILLED, 2 PARTIALLY_FILLED, 3 CANCELED, 4 PRE_CANCEL, 5 CANCELING, 6 INVALID
isTaker | options/futures/websocket | Filled by taker side: 0 FALSE 1 TRUE
period | websocket | granularity of K-line: m1 1minute, m5 5minutes, m15 15minutes, m30 30minutes, h1 1hour, h4 4hours, d1 1day, w1 1week, mn1 1month, quarter 3months
stp | options | stp type: 1 CM, 2 CT, 3 CB

## Pagination query
Some APIs use cursor-based paging, where each query uses a reference record ID (fromId) and a paging direction (direction) to retrieve records that are newer or older than the given ID. This approach supports navigating through data using "Previous" and "Next" pages.

### Input Parameters
**fromId**  

- The reference ID for pagination
- Typically taken from a record on the previous or next page.
- null or 0L indicates the first (most recent) page. 
  
**direction**   

- Used to specify the pagination direction: 

Value | Meaning | Query Condition | Sort Order
----  | --------| ----------------| -----------
NEXT | Forward pagination (older data) |  id < fromId | ORDER BY id DESC
PREV | backward pagination (newer data) | id > fromId | ORDER BY id ASC (then reversed before display)

### Response Fields  
**hasNext** 

- Indicates if there is a next page
- In NEXT mode: Indicates if more older records exist
- In PREV mode: Indicates if newer records exist when paging back.

**hasPrev** 

- Indicates if there is a previous page 
- In NEXT mode: True if not on the first page 
- In PREV mode: True if not on the last page 
  
## Error Information

```javascript
{
  "code": -40004,
  "msg": "Invalid symbol."
}
```

* All endpoints return error payload:

* Specific error codes and messages defined in [Error Codes](#error-codes)
