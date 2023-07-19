# Futures WebSocket

* WSS interface for futures: `wss://ws.coincall.com/futures`

  * Connection example: `wss://ws.coincall.com/futures?code=10&uuid=65905c2be07f49e79ac26aca4b0b3988&ts=1687326076897&sign=CF58E8C7BE6C10EF7D8A65F3D0538F7D6C73182C6AFCA26D2CBE2318E085E494&apiKey=22582BD0CFF14C41EDBF1AB98506286D`

**Value of Connection Parameters**

Name | Required | Note |
--- | -------- | ---- |
code | true | 10, build connection
uuid | false | Custom id by user
ts | true | Timestamp, 1687326076897
sign | true | Signature
apiKey | true | your api key

**sign:** signature string, the signature algorithm is as follows:

First concatenate `method + uri + ?uuid=your_api_key&ts=your_timestamp` (where `+` represents String concatenation), then use HMAC SHA256 method to encrypt the concatenated string with `apiSecret`, and then perform Base64 encoding.

`method`: always `GET`.

`uri` : always `/users/self/verify`

<aside class="notice">
   <p>If there’s a network problem, the system will automatically disable the connection.</p>

    <p>The connection will break automatically if the subscription is not established or data has not been pushed for more than 30 seconds.</p>

    <p>To keep the connection stable:</p>

    <p>1. Set a timer of N seconds whenever a response message is received, where N is less than 30.</p>

    <p>2. If the timer is triggered, which means that no new message is received within N seconds, send the HeartBeat action.</p>

    <p>3. Expect 'rc':1 as a response. If the response message is not received within N seconds, please raise an error or reconnect.</p>
</aside>

## Data Abbreviations

Please refer to the following field abbreviations for data fields in the futures request/response:

| Name | Note |
| --- | --- |
| c | code, Operations for Request Protocol Execution |
| rc | response code, Status of the Response Protocol |
| d | data, Request/Response payload |
| p | position, Subscription Data Page Location |
| s | symbol |
| pr | price |
| mp | mark Price |
| ip | index Price |
| h | price24hHigh, Highest price in 24hrs |
| l | price24hLow, Lowest price in 24hrs |
| cp | changePrice, Price change in value |
| cr | changeRate, Price change in percentage |
| pr0 | price24hOpen, Open price on UTC 00:00:00 |
| uv24 | volumeUsd24h, USD volume in 24hrs |
| v24 | volume24h, Volume in 24hrs |
| high | high, The highest price |
| low | low, The lowest price |
| pe | period, granularity of K-line |
| v | volume |
| close | close price |
| open | open price |
| ts | timestamp |
| sz | size |
| sd | tradeSide, buy or sell |
| q | qty, quantity |
| fq | filled quantity |
| ap | avgPrice, average price |
| coid | clientOrderId |
| os | order status |
| im | initial Margin |
| oid | orderId |
| si | trade side |
| ty | order type |
| uid | userId |
| elp | estimated Liquidation Price |
| mm | maintenance Margin |
| upnl | Unrealized Pnl |
| dt | dataType, websocket channels |

<!-- ## futures -->

## HeartBeat
{
    "action":"heartbeat"
}

```json
Payload:

{
    "c":11,
    "rc":1 // 1 Success
}

```

## Index Price
{
    "action":"subscribe",
    "dataType":"spotPrice",
    "payload":{
        "symbol":"BTCUSD"
    }
}

```json
Payload:

{
  "dt": 30,
  "c": 20,
  "d": {
    "pr": 1.1752, // last price
    "mp": 1.17521086, // mark Price 
    "ip": 1.17550000, // index Price
    "h": 1.18070000, // price24hHigh, Highest price in 24hrs
    "l": 1.12120000, // price24hLow, Lowest price in 24hrs
    "cp": 0.02410000, // changePrice, Price change in value
    "cr": 0.0209, // Price change in percentage
    "pr0": 1.05768, // price24hOpen, Open price on UTC 00:00:00
    "s": "ARBUSD", // symbol 
    "uv24": 320076.05815000, // volumeUsd24h, USD volume in 24hrs
    "v24": 278226.50000000 // volume24h, Volume in 24hrs
  }
}

```

## K-line Data
{
    "action":"subscribe",
    "dataType":"kline",
    "payload":{
        "symbol":"BTCUSD",
        "period":"h1"
    }
}

**Value of period**

| Key | Note |
| --- | ---- |
| m1 | 1 minute|
| m5 | 5 minutes|
| m15 | 15 minutes |
| m30 | 30 minutes |
| h1 | 1 hour |
| h4 | 4 hours |
| d1 | 1 day |
| w1 | 1 week |
| mn1 | 1 month |
| quarter | 3 months |

```json
Payload:

{
  "dt": 31,
  "c": 20,
  "d": {
    "high": 30831.73000000, // The highest price
    "s": "BTCUSD", // symbol 
    "low": 30831.73000000, // The lowest price
    "pe": "m1", // period, granularity of K-line
    "v": 1.00000000, // volume
    "close": 30831.73000000, // close price
    "open": 30831.73000000, // open price
    "ts": 1688383680000 // timestamp
  }
}

```

## OrderBook
{
    "action":"subscribe",
    "dataType":"orderBook",
    "payload":{
        "symbol":"BTCUSD"
    }
}

Message channel for the 100 best ask/bid full data. After subscription, when there are changes in the order book, the system will push the real-time ticker symbol information to you

```json
Payload:

{
  "dt": 32,
  "c": 20,
  "d": {
    "s": "BTCUSD", // symbol 
    "asks": [{
      "pr": "30831.73", // price 
      "sz": "180.30200000" // size 
    }, {
      "pr": "40000", 
      "sz": "0.40000000 "
    }],
    "bids": [{
      "pr": "1",
      "sz": "1 "
    }],
    "ts": 1688384138863 // timestamp
  }
}

```

## Last Trades
{
    "action":"subscribe",
    "dataType":"lastTrade",
    "payload":{
        "symbol":"BTCUSD"
    }
}

```json
Payload:

{
  "dt": 33,
  "c": 20,
  "d": [{
    "q": "1", // qty quantity
    "sd": 1, // tradeSide
    "pr": "30831.73000000", // price
    "s": "BTCUSD",  // symbol 
    "ts": 1688436545891 // timestamp
  }, {
    "q": "83.11100000",
    "sd": 1,
    "pr": "30139.37000000",
    "s": "BTCUSD",
    "ts": 1688370059868
  }]
}

```

## Orders
{
"action":"subscribe",
"dataType":"order"
}

```json
Payload:

{
  "dt": 35,
  "c": 20,
  "d": {
    "fq": "2", // filled quantity
    "ap": "0.3435", // average price
    "coid": "1676063763780026368", // client order id 
    "os": "1", // order status
    "oid": "1676063763800997888", // order id
    "pr": "0.3435", // price
    "s": "FTMUSD", // symbol
    "si": "1", // order side
    "ti": "1688439715857", // timestamp
    "ty": "1", // order type 
    "uid": "8095151726" // user id
  }
}

```

## Positions
{
    "action":"subscribe",
    "dataType":"position"
}

```json
Payload:

{
  "dt": 36,
  "c": 20,
  "d": {
    "q": "4", // filled quantity
    "ap": "0.3435", // average price
    "elp": "-20963.68918261", // Elp estimated Liquidation Price
    "im": "0.458", // initMargin
    "mm": "0.04122", // maintMargin 
    "mp": "0.3435", // mark price 
    "s": "FTMUSD", // symbol 
    "si": "1", // order side
    "uid": "8095151726", // user id
    "upnl": "0" // Unrealized Pnl
  }
}

```
