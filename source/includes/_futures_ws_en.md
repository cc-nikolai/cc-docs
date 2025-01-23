# Futures WebSocket

```python
# Sample code 

import hashlib
import hmac
import time
import websocket
import json
import threading

# API INFO
api_key = "YOUR_API_KEY"
api_sec = "YOUR_API_SECRET"

def on_open(ws):
    print("WebSocket connection opened.")
    # Send a subscribe message after the connection opened.
    ws.send(json.dumps({ "action":"subscribe", "dataType":"spotPrice", "payload":{ "symbol":"BTCUSD" } }))

def on_close(ws, status, message):
    print(f'WebSocket connection closed. status: {status}, message: {message}')

def on_error(ws, error):
    print(f'WebSocket error: {error}')

def on_message(ws, message):
    data = json.loads(message)
    print(data)

def get_signed_header(ts):
    verb='GET'
    uri = '/users/self/verify'
    auth = verb + uri + '?uuid=' + api_key + '&ts=' + str(ts)
    signature = hmac.new(api_sec.encode('utf-8'), auth.encode('utf-8'), hashlib.sha256).hexdigest()
    signature = signature.upper()
    return signature
    
ts = int(time.time()*1000)
sign = get_signed_header(ts)
socket = 'wss://ws.coincall.com/futures?code=10&uuid=' + api_key +'&ts='+ str(ts) +'&sign=' + sign + '&apiKey=' + api_key
ws = websocket.WebSocketApp(socket, on_open=on_open, on_close=on_close, on_error=on_error, on_message=on_message)

def run():
    ws.run_forever()

ws_thread = threading.Thread(target=run)
ws_thread.start()

while True:
    # Wait for the WebSocket connection to be established
    if ws.sock and ws.sock.connected:
        # Send heartbeat
        msg = {"action":"heartbeat"}
        ws.send(json.dumps(msg))
        time.sleep(3)
    else:
        # If the WebSocket connection is not established, wait 3 seconds
        time.sleep(3)

```

* WSS interface for futures: `wss://ws.coincall.com/futures`

  * Connection example: `wss://ws.coincall.com/futures?code=10&uuid=65905c2be07f49e79ac26aca4b0b3988&ts=1687326076897&sign=CF58E8C7BE6C10EF7D8A65F3D0538F7D6C73182C6AFCA26D2CBE2318E085E494&apiKey=7PvIEreC1g5Kd17S7Ei1mEd3ppyuoixhqlzqM0Rqfhw=`

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
| ty | trade type |
| uid | userId |
| elp | estimated Liquidation Price |
| mm | maintenance Margin |
| upnl | Unrealized Pnl |
| dt | dataType, websocket channels |
| ct | createTime |
| ro | reduceOnly |
| tid | trade ID |
| rq | remainQty, Unfilled Quantity |
| mpr | match price |
| mq | match quantity |
| le | leverage |
| it | isTaker |
| cq | canceled quantity |

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
### subscribe
{
    "action":"subscribe",
    "dataType":"spotPrice",
    "payload":{
        "symbol":"BTCUSD"
    }
}
### unsubscribe
{
    "action":"unsubscribe",
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
### subscribe
{
    "action":"subscribe",
    "dataType":"kline",
    "payload":{
        "symbol":"BTCUSD",
        "period":"h1"
    }
}
### unsubscribe
{
    "action":"unsubscribe",
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
### subscribe
{
    "action":"subscribe",
    "dataType":"orderBook",
    "payload":{
        "symbol":"BTCUSD"
    }
}
### unsubscribe
{
    "action":"unsubscribe",
    "dataType":"orderBook",
    "payload":{
        "symbol":"BTCUSD"
    }
}

**Update Speed: 200ms**

Message channel for the 100 best ask/bid full data.

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
### subscribe
{
    "action":"subscribe",
    "dataType":"lastTrade",
    "payload":{
        "symbol":"BTCUSD"
    }
}
### unsubscribe
{
    "action":"unsubscribe",
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
### subscribe
{
"action":"subscribe",
"dataType":"order"
}
### unsubscribe
{
"action":"unsubscribe",
"dataType":"order"
}

```json
Payload:

Status: 0 NEW
{
  "dt": 35,
  "c": 20,
  "d": {
    "coid":1000200000, // Client order id
    "oid": 1663004711982333952, // Order id
    "uid": "8095151726", // User id
    "s": "BTCUSD",// Futures symbol name
    "q": "1", // Order Quantity
    "pr": "500", // Price
    "si": 1,  // Trade side > si
    "ty": 1,  // Trade type > ty
    "ct": 1685326195118,// Time of the order created
    "ts": 1685326195118,// Time of this event
    "ro": 0,  //Reduce only
    "le": 3,  //  Leverage
    "os": 0 //Status NEW
  }
}

Status: 1 FILLED
{
  "dt": 35,
  "c": 20,
  "d": {
    "coid":1000200000, // Client order id
    "oid": 1663004711982333952, // Order id
    "uid": "8095151726", // User id
    "s": "BTCUSD",// Futures symbol name
    "q": "1", // Order Quantity
    "fq": "1", // Filled Quantity(accumulated)
    "rq": "0", // Unfilled Quantity
    "pr": "500", // Order Price
    "mpr": "499", // filled price in this trade
    "mq": "0.5", // filled quantity in this trade
    "ap": "0", // Average filled price(accumulated)
    "si": 1,  // Trade side
    "ty": 1,  // Trade type
    "ct": 1685326195118,// Time of the order created
    "ts": 1685326195118,// Time of this event
    "ro": 0,  //Reduce only
    "le": 3,  //  Leverage
    "it": 0, // Taker or Maker, 1 TRUE 0 FALSE
    "os": 1 // FILLED
  }
}

Status: 2 PARTIALLY_FILLED
{
  "dt": 35,
  "c": 20,
  "d": {
    "coid":1000200000, // Client order id  
    "oid": 1663004711982333952, // Order id 
    "uid": "8095151726", // User id
    "s": "BTCUSD",// Futures symbol name
    "q": "1", // Order Quantity
    "fq": "0.5", // Filled Quantity(accumulated)
    "rq": "0.5", // Unfilled Quantity
    "pr": "500", // Price
    "mpr": "499", // filled price in this trade
    "mq": "0.5", // filled quantity in this trade
    "ap": "0", // Average filled price(accumulated)
    "si": 1,  // Trade side
    "ty": 1,  // Trade type
    "ct": 1685326195118,// Time of the order created
    "ts": 1685326195118,// Time of this event
    "ro": 0,  //Reduce only
    "le": 3,  //  Leverage
    "it": 0, // Taker or Maker, 1 TRUE 0 FALSE
    "os": 2 // PARTIALLY_FILLED
  }
}

Status: 3 CANCELED
{
  "dt": 35,
  "c": 20,
  "d": {
    "coid":1000200000, // Client order id
    "oid": 1663004711982333952, // Order id
    "uid": "8095151726", // User id
    "s": "BTCUSD",// Futures symbol name
    "q": "1", // Order Quantity
    "fq": "0.5", // Filled Quantity(accumulated)
    "cq": "0.5", // Canceled Quantity
    "pr": "500", // Price
    "ap": "0", // Average filled price(accumulated)
    "si": 1,  // Trade side
    "ty": 1,  // Trade type
    "ct": 1685326195118,// Time of the order created
    "ts": 1685326195118,// Time of this event
    "ro": 0,  // Reduce only
    "le": 3,  // Leverage
    "os": 3 // CANCELED
  }
}

Status: 6 INVALID
{
  "dt": 35,
  "c": 20,
  "d": {
    "coid":1000200000, // Client order id
    "oid": 1663004711982333952, // Order id
    "uid": "8095151726", // User id
    "s": "BTCUSD",// Futures symbol name
    "q": "1", // Order Quantity
    "fq": "0.5", // Filled Quantity(accumulated)
    "rq": "0.5", // Unfilled Quantity
    "pr": "500", // Price
    "ap": "0", // Average filled price(accumulated)
    "si": 1,  // Trade side
    "ty": 1,  // Trade type
    "ct": 1685326195118,// Time of the order created
    "ts": 1685326195118,// Time of this event
    "ro": 0,  // Reduce only
    "le": 3,  // Leverage
    "os": 6 // INVALID
  }
}

```

## Trade
### subscribe
{
    "action":"subscribe",
    "dataType":"trade"
}
### unsubscribe
{
    "action":"unsubscribe",
    "dataType":"trade"
}

```json
Payload:

{
    "dt": 38,
    "c": 20,
    "d": {
        "coid": "1734123406279839744", // client order id
        "fr": "0.0006", // feeRate
        "tf":"-0.1234", // tradeFee
        "it": "0", // isTaker
        "mpr": "22180", // matchPrice
        "mq": "2", // matchQty
        "mv": "44360", // matchValue
        "oid": "1734123406279839744", // order id
        "si": "1", // trade side
        "rq": "0", // remainQty
        "s": "BTCUSD", // symbol
        "tid": "1734129035131924480", // tradeId
        "ts": "1702282213169" // trade time
    }
}

```

## Positions
### subscribe
{
    "action":"subscribe",
    "dataType":"position"
}
### unsubscribe
{
    "action":"unsubscribe",
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
