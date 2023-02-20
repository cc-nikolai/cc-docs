# General Information
## General API Information
* Base endpoint: **https://api.coincall.com**
* Endpoint returns JSON object
* All time and timestamp related fields are UNIX in **milliseconds**.

## Error Codes and Messages
* All endpoints return error payload as follows:


```javascript
{
  "code": -40004,
  "msg": "Invalid symbol."
}
```

* Specific error codes and messages defined in Error Codes


## **General Information on Endpoints**

* For `GET`endpoints, parameters must be sent as a `query string`.
* For `POST`endpoint, the parameters may be sent as a `query string`or in the `request body`
with content type `application/x-www-form-urlencoded`. You may mix parameters between both the query string and request body if you wish to do so.
* Parameters may be sent in any order.
* If a parameter sent in both the `query string`and`request body`, the `query string` parameter will be used.
* Because the API system is asynchronous, it is normal and expected that there will be a delay in the returned data.

# LIMITS
## **General Info on Limits**

* **Rate Limits**
  
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

# **Endpoint security type** 
* Each endpoint has a security type that determines how you will interact with it.
* Security type is stated next to the NAME of the endpoint. If no security type is stated, assume the security type is `NONE`.
* If API-keys are needed, send  `X-CC-APIKEY`in the HTTP header.
* API-keys and secret-keys are case sensitive.
* API-keys can be configured to only access certain types of secure endpoints. For example, one API-key could be used for TRADE only, while another API-key can access everything except for TRADE routes.
* By default, API-keys can access all secure routes.

Security Type | Description
------------ | ------------
NONE | Endpoint can be accessed freely.
SIGNED | Requires valid API-Key and Signed.

* SIGNED endpoint is the signature endpoint.

# SIGNED Endpoint Security
* `SIGNED` endpoints require an additional parameter, `sign`, to be sent in the `header`.
* Endpoints use `HMAC SHA256`signatures. The API-Secret corresponding to the API-KEY is used as the secret of `HMAC SHA256` , all other parameters are used as objects of`HMAC SHA256`, and the output is the signature.
* The `signature` is not case sensitive.

## Timing security
* All signed endpoints require a parameter, `ts`, to be sent in the header which should be the UNIX millisecond timestamp of when the request was created and sent.
* An additional parameter, `X-REQ-TS-DIFF` may be sent to specify the number of milliseconds after `ts` the request is valid for. If `X-REQ-TS-DIFF` is not sent, it defaults to 5000.

  ```javascript
  if (timestamp < (serverTime + 1000) && (serverTime - timestamp) <= X-REQ-TS-DIFF) {
    // process request
  } else {
    // reject request
  }
  ```

**Serious trading is about timing.** Networks can be unstable and unreliable, which can lead to requests taking varying amounts of time to reach the servers. With `X-REQ-TS-DIFF`
, you can specify that the request must be processed within a certain number of milliseconds or be rejected by the server. **It is recommended to use a `X-REQ-TS-DIFF` of 5000 or less.**