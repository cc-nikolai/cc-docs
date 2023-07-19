# Overview

Welcome to the Coincall API! You can use our API to access Coincall  Open API endpoints.

We have language bindings in Java, Curl, Shell, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

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
* For `POST`endpoint, the parameters must be sent in the `request body` with content type `application/json`.
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
Get Historical Order / Transactions | 4 / 1s | per User ID
Get Account Information | 2 / 1s | per User ID
Get Orderbook | 30 / 2s | per User ID
Place Order | 30 / 2s | per User ID
Cancel Order | 30 / 2s | per User ID

<aside class="notice">
    It is strongly recommended to use websocket stream for getting data as much as possible, which can not only ensure the timeliness of the message, but also reduce the access restriction pressure caused by the request.
</aside>

## Authentication

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
* `sign` The Base64-encoded signature (see Signing Messages subsection for details).
* `ts` The timestamp of your request .e.g : 1688436087184
* `X-REQ-TS-DIFF` sent to specify the number of milliseconds after `ts` the request is valid for. If `X-REQ-TS-DIFF` is not sent, **it defaults to 5000**.

Request bodies should have content type `application/json` and be in valid JSON format.

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

* Add `?` after request uri path, separate each parameter with a `&` which represents Parameters concatenation, sort them alphabetically. (If no prameter here, can only add `?` after request uri path)
* Create a prehash string of `method + uri + &uuid=your_api_key&ts=your_timestamp&x-req-ts-diff=your_ts_diff ` (where `+` represents String concatenation, if no prameter here, please use `method + uri + uuid=your_api_key&ts=your_timestamp&x-req-ts-diff=your_ts_diff ` instead).
* Sign the prehash string with the apiSecret using the HMAC SHA256.
* Encode the signature in the Base64 format.
* The `sign` should be UPPER.

**Example:**

`your_prehash_string=POST/open/futures/leverage/set/v1?leverage=1&symbol=BTCUSD&uuid=xdtHWn32rsuDQConutzl9JDZB+Y1leitFl356YHrmts=&ts=1688436087184&x-req-ts-diff=3000`

`sign=hmac.new(your_api_secret.encode('utf-8'), your_prehash_string.encode('utf-8'), hashlib.sha256).hexdigest()`

The timestamp value is the same as the `ts` header with UNIX millisecond timestamp of when the request was created and sent, e.g. 1688436087184

The request `method` should be in UPPERCASE: e.g. `GET` and `POST`.

The `uri` is the path of requesting an endpoint, separate each parameter with a `&`, `?` represents Parameters concatenation.

Example: `/open/futures/leverage/set/v1?leverage=1&symbol=BTCUSD`

<aside class="notice">
    GET request parameters are counted as uri, not body
</aside>

Your API Secret is generated when you create an APIKey.


## Field Type Enumeration

Name | Product | Note
---- | ------- | ----
type | options | Option order type: 1 CALL, 2 PUT
tradeSide | options/futures/websocket | Trade side: 1 BUY, 2 SELL
tradeType | options/futures/websocket | Trade type: 1 LIMIT, 2 MARKET, 3 POST_ONLY, 4 STOP_LIMIT, 5 STOP_MARKET
reduceOnly | options/futures/websocket | Reduce only: 0 FALSE, 1 TRUE
state | options/websocket | Order status: -10 ILLEGAL, -1 PRE, 0 NEW, 1 FILLED, 2 PARTIALLY_FILLED, 3 CANCELED, 4 PRE_CANCEL, 5 CANCELING, 6 INVALID, 10 CANCEL_BY_EXERCISE
state | futures/websocket | Order status: -2 WAITING_EFFECT, -1 PRE, 0 NEW, 1 FILLED, 2 PARTIALLY_FILLED, 3 CANCELED, 4 PRE_CANCEL, 5 CANCELING, 6 INVALID
isTaker | options/futures/websocket | Filled by taker side: 0 FALSE 1 TRUE
period | websocket | granularity of K-line: m1 1minute, m5 5minutes, m15 15minutes, m30 30minutes, h1 1hour, h4 4hours, d1 1day, w1 1week, mn1 1month, quarter 3months

## Error Information

```javascript
{
  "code": -40004,
  "msg": "Invalid symbol."
}
```

* All endpoints return error payload:

* Specific error codes and messages defined in [Error Codes](#error-codes)