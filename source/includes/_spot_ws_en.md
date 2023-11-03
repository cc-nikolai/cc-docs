# Spot WebSocket

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
    # public topic
    ws.send(json.dumps({ "sub":"market.XRPUSDT.kline.1min", "id":"1698208992286"}))
    # private topic
    ws.send(json.dumps({ "sub":"order", "id":"1698208992286"}))

def on_close(ws):
    print("WebSocket connection closed.")

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
# public spot
# socket = 'wss://ws.coincall.com/spot/ws'
# private spot
socket = 'wss://ws.coincall.com/spot/ws/private?ts='+ str(ts) +'&sign=' + sign + '&apiKey=' + api_key
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

* WSS interface for futures: `wss://ws.coincall.com/spot`

  * Public connection example: `wss://ws.coincall.com/spot/ws`

  * Private connection example: `wss://ws.coincall.com/spot/ws/private?ts=1687326076897&sign=CF58E8C7BE6C10EF7D8A65F3D0538F7D6C73182C6AFCA26D2CBE2318E085E494&apiKey=7PvIEreC1g5Kd17S7Ei1mEd3ppyuoixhqlzqM0Rqfhw=`

**Value of Private Connection Parameters**

Name | Required | Note |
--- | -------- | ---- |
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

## Public Orderbook
* Once you have subscribed successfully, you will receive a snapshot.
* The WebSocket will keep pushing delta messages every time the orderbook changes. If you receive a new snapshot message, you will have to reset your local orderbook.

{
	"sub": "market.$symbol.mbp.$step",
	"id": "$timestamp"
}

$step value: 1, 50, 100, 200

**Update Speed:**

Level 1 data, push frequency:**10ms**

Level 50 data, push frequency:**20ms**

Level 100 data, push frequency:**100ms**

Level 200 data, push frequency:**100ms**

```json
Payload:

// snapshot
{
	"ch": "market.XRPUSDT.mbp.50",
	"ts": 1698824389345,
	"status": "ok",
	"tick": {
		"s": "XRPUSDT",
		"b": [
			[0.5958, 6198.0], // Price, Size
			[0.5956, 15113.0],
			[0.5954, 30156.0],
			[0.5952, 23570.0],
			[0.595, 24491.0],
			[0.5948, 14661.0],
			[0.5946, 26620.0],
			[0.5942, 22317.0],
			[0.5939, 23840.0],
			[0.5936, 767.0],
			[0.5935, 24077.0],
			[0.5933, 31702.0],
			[0.5915, 2371.0],
			[0.5905, 12671.0],
			[0.5897, 901.0],
			[0.5891, 2566.0],
			[0.5885, 11754.0]
		],
		"a": [
			[0.5967, 19808.0], // Price, Size
			[0.597, 2614.0],
			[0.5972, 55037.0],
			[0.5974, 84102.0],
			[0.5976, 957.0],
			[0.5978, 64141.0],
			[0.598, 2134.0],
			[0.5982, 79251.0],
			[0.5984, 10784.0],
			[0.599, 32038.0],
			[0.5996, 1757.0],
			[0.6002, 964.0],
			[0.6008, 23247.0],
			[0.6014, 11966.0],
			[0.6022, 2562.0],
			[0.6028, 25037.0],
			[0.6036, 1229.0],
			[0.6042, 31042.0]
		],
		"type": "snapshot", // Data type
		"u": 93639 // Update ID
	}
}

// delta
{
	"ch": "market.XRPUSDT.mbp.50",
	"ts": 1698824394244,
	"status": "ok",
	"tick": {
		"s": "XRPUSDT",
		"b": [ // Bids to be updated
			[0.5958, 0.0] // Price, Size
		],
		"a": [], // // Asks to be updated
		"type": "delta", // Data type
		"prevU": 93640, // Last update ID
		"u": 93641 // Update ID
	}
}

```

## Public Trade Streams
{
	"sub": "market.$symbol.trade.detail",
	"id": "$timestamp"
}

```json
Payload:

{
	"ch": "market.XRPUSDT.trade.detail",
	"ts": 1698825567210,
	"status": "ok",
	"tick": [{
		"tradeId": "64171106369742529", // Trade ID
		"symbol": "XRPUSDT", // Symbol name
		"price": 0.5981, // Trade price
		"qty": 814.0, // Trade quantity
		"side": 2, // Trade side
		"ts": 1698825550425 // Trade time
	}]
}

```

## Public Kline/Candlestick Streams
{
  "sub": "market.$symbol.kline.$interval",
  "id": "$timestamp"
}

**Value of period**

| Key | Note |
| --- | ---- |
| 1min | 1 minute|
| 5min | 5 minutes|
| 15min | 15 minutes |
| 30min | 30 minutes |
| 60min | 1 hour |
| 4hour | 4 hours |
| 1day | 1 day |
| 1week | 1 week |
| 1mon | 1 month |
| 1year | 1 year |

```json
Payload:

{
	"ch": "market.XRPUSDT.kline.1min",
	"ts": 1698825870620,
	"status": "ok",
	"tick": {
		"endTime": 1698825840000, // The end timestamp (ms)
		"open": 0.5985, // Open price
		"close": 0.5983, // Close price
		"low": 0.5974, // Lowest price
		"high": 0.5985, // Highest price
		"volume": 1498.0, // Trade volume
		"volumeUsd": 895.7453 // Trade volume in USD
	}
}

```

## Public Symbol Ticker Streams

Pushes any update to the best bid or ask's price or quantity in real-time for a specified symbol.

{
  "sub": "market.$symbol.bbo",
  "id": "$timestamp"
}

```json
Payload:

{
	"ch": "market.XRPUSDT.bbo",
	"ts": 1698826509820,
	"status": "ok",
	"tick": {
		"symbol": "XRPUSDT",
		"bidPrice": 0.6009,
		"bidSize": 14131.0,
		"askPrice": 0.6026,
		"askSize": 51025.0
	}
}

```

## Public Symbol 24Ticker Streams

{
  "sub": "market.overviewv2",
  "id": "$timestamp"
}

```json
Payload:

{
	"ch": "market.overviewv2",
	"status": "ok",
	"ts": 1698826877951,
	"tick": {
		"TRXUSDT": {
			"s": "TRXUSDT", // Symbol name
			"base": "TRX", // Base coin
			"quote": "USDT", // Quote coin
			"o": 0.09609, // Open price
			"h": 0.0982, // Highest price
			"l": 0.09506, // Lowest price
			"c": 0.09773, // Close price
			"a": 1502146.0, // Volume in base coin
			"v": 145298.5662, // Volume in quote coin
			"r": 0.01706733270891875, // Price change in value
			"cp": 0.0016400000000000026, // // Price change in percentage
			"i": 0.09783096 // Index price.
		}
	}
}

```

## Public Symbol 24Ticker Streams by a symbol

{
  "sub": "market.$symbol.overviewv2",
  "id": "$timestamp"
}

```json
Payload:

{
	"ch": "market.TRXUSDT.overviewv2",
	"status": "ok",
	"ts": 1698826877951,
	"tick": {
		"TRXUSDT": {
			"s": "TRXUSDT", // Symbol name
			"base": "TRX", // Base coin
			"quote": "USDT", // Quote coin
			"o": 0.09609, // Open price
			"h": 0.0982, // Highest price
			"l": 0.09506, // Lowest price
			"c": 0.09773, // Close price
			"a": 1502146.0, // Volume in base coin
			"v": 145298.5662, // Volume in quote coin
			"r": 0.01706733270891875, // Price change in value
			"cp": 0.0016400000000000026, // // Price change in percentage
			"i": 0.09783096 // Index price.
		}
	}
}

```

## Private Orders

{
  "sub": "order",
  "id": "$timestamp"
}

```json
Payload:

Status: 0 NEW
{
	"ch": "order",
	"ts": 1698893249297,
	"status": "ok",
	"tick": {
		"orderId": 66362398685069333,
		"clientOrderId": "66362398685069333",
		"symbol": "XRPUSDT",
		"price": "0.594",
		"qty": "1",
		"tradeSide": "buy",
		"tradeType": 1,
		"status": 0,
		"createTime": 1698893249252
	}
}

Status: 1 FILLED
{
	"ch": "order",
	"ts": 1698895342017,
	"status": "ok",
	"tick": {
		"orderId": 66362398685069357,
		"clientOrderId": "66362398685069357",
		"symbol": "XRPUSDT",
		"price": "0.6243",
		"qty": "100",
		"tradeSide": "buy",
		"status": 1,
		"avgPrice": "0.60920100",
		"remainQty": "0",
		"filledQty": "100",
		"createTime": 1698895341979,
		"matchTime": 1698895342004,
		"tradeId": "726474966362398685069357",
		"isTaker": 1,
		"matchPrice": "0.60920100",
		"matchQty": "100",
		"tradeType": 2
	}
}

Status: 2 PARTIALLY_FILLED
{
	"ch": "order",
	"ts": 1698899289854,
	"status": "ok",
	"tick": {
		"orderId": 66362398685069360,
		"clientOrderId": "66362398685069360",
		"symbol": "XRPUSDT",
		"price": "0.6",
		"qty": "10",
		"tradeSide": "buy",
		"status": 2,
		"avgPrice": "0.60000000",
		"remainQty": "9",
		"filledQty": "1",
		"createTime": 1698899237116,
		"matchTime": 1698899289843,
		"tradeId": "726475366362398685069360",
		"isTaker": 0,
		"matchPrice": "0.6",
		"matchQty": "1",
		"tradeType": 1
	}
}

Status: 3 CANCELED
{
	"ch": "order",
	"ts": 1698893719826,
	"status": "ok",
	"tick": {
		"orderId": 66362398685069333,
		"clientOrderId": "66362398685069333",
		"symbol": "XRPUSDT",
		"price": "0.594",
		"qty": "1",
		"tradeSide": "buy",
		"status": 3,
		"avgPrice": "0",
		"filledQty": "0",
		"createTime": 1698893249252,
		"canceledQty": "1",
		"tradeType": 1
	}
}

```