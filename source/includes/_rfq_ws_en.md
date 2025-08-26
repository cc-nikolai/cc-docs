# RFQ WebSocket

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
    ws.send(json.dumps({ "action":"subscribe", "dataType":"orderBook", "payload":{ "symbol":"BTCUSD-27DEC24-65000-C" } }))

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
    auth = verb + uri + '?apiKey=' + api_key + '&ts=' + str(ts)
    signature = hmac.new(api_sec.encode('utf-8'), auth.encode('utf-8'), hashlib.sha256).hexdigest()
    signature = signature.upper()
    return signature

ts = int(time.time()*1000)
sign = get_signed_header(ts)
socket = 'wss://ws.coincall.com/options?code=10&uuid=' + api_key +'&ts='+ str(ts) +'&sign=' + sign + '&apiKey=' + api_key
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

* WSS interface for options: `wss://ws.coincall.com/options`

  * Connection example: `wss://ws.coincall.com/options?code=10&uuid=65905c2be07f49e79ac26aca4b0b3988&ts=1687326076897&sign=CF58E8C7BE6C10EF7D8A65F3D0538F7D6C73182C6AFCA26D2CBE2318E085E494&apiKey=7PvIEreC1g5Kd17S7Ei1mEd3ppyuoixhqlzqM0Rqfhw=`

**Value of Connection Parameters**

Name | Required | Note |
--- | -------- | ---- |
code | true | 10, build connection
uuid | false | Custom id by user
ts | true | Timestamp, 1687326076897
sign | true | Signature
apiKey | true | your api key

**sign:** signature string, the signature algorithm is as follows:

First concatenate `method + uri + ?apiKey=your_api_key&ts=your_timestamp` (where `+` represents String concatenation), then use HMAC SHA256 method to encrypt the concatenated string with `apiSecret`, and then perform Base64 encoding.

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

<!-- ## options -->

## RFQ Maker 

### subscribe 

{ "action":"subscribe", "dataType":"rfqMaker" }

### unsubscribe 

{ "action":"unSubscribe", "dataType":"rfqMaker" }


```json
1.create new RFQ request:

{    
    "dt": 28,
    "c": 20,
    "d": {
        "createTime": 1755225804558,
        "expiryTime": 1755229404540,
        "updateTime": 1755229404540,
        "legs": [
            {
                "instrumentName": "BTCUSD-22AUG25-120000-C",
                "price": "1788.51759065",
                "quantity": "11",
                "side": "BUY"
            },
            {
                "instrumentName": "BTCUSD-29AUG25-120000-C",
                "price": "2902.39496504",
                "quantity": "22",
                "side": "SELL"
            }
        ],
        "requestId": "1956184923266224128",
        "state": "ACTIVE"
    },
    "ts": 1755225804597
} 

``` 

```json
2. RFQ request cancel:
{
    "dt": 28,
    "c": 20,
    "d": {
        "createTime": 1755225804558,
        "expiryTime": 1755261085596,
        "updateTime": 1755229404540,
        "legs": [
            {
                "instrumentName": "BTCUSD-22AUG25-119000-C",
                "price": "2025.72422884",
                "quantity": "11",
                "side": "BUY",
                "instrumentType": "OPTION",
            },
            {
                "instrumentName": "BTCUSD-5SEP25-119000-C",
                "price": "4018.83713307",
                "quantity": "22",
                "side": "BUY"
            }
        ],
        "requestId": "1956317803187408896",
        "state": "CANCELLED"
    },
    "ts": 1755257506166
}
``` 

```json
3.RFQ Filled:

{  
    "dt": 28,
    "c": 20,
    "d": {
        "createTime": 1755225804558,
        "expiryTime": 1755229404540,
        "updateTime": 1755229404540,
        "legs": [
            {
                "instrumentName": "BTCUSD-22AUG25-120000-C",
                "price": "1788.51759065",
                "quantity": "11",
                "side": "BUY"
            },
            {
                "instrumentName": "BTCUSD-29AUG25-120000-C",
                "price": "2902.39496504",
                "quantity": "22",
                "side": "SELL"
            }
        ],
        "requestId": "1956184923266224128",
        "state": "FILLED"
    },
    "ts": 1755225804597
}
 
``` 

```json
4. RFQ trade away:

{  
   "dt": 28,
    "c": 20,
    "d": {
        "createTime": 1755225804558,
        "expiryTime": 1755229404540,
        "updateTime": 1755229404540,
        "legs": [
            {
                "instrumentName": "BTCUSD-22AUG25-120000-C",
                "price": "1788.51759065",
                "quantity": "11",
                "side": "BUY",
            },
            {
                "instrumentName": "BTCUSD-29AUG25-120000-C",
                "price": 2902.39496504,
                "quantity": 22,
                "side": "SELL",
            }
        ],
        "requestId": 1956184923266224128,
        "state": "TRADED_AWAY"
    },
    "ts": 1755225804597
}

```


## RFQ Quote

### subscribe 

{ "action":"subscribe", "dataType":"rfqQuote" }

### unsubscribe 

{ "action":"unSubscribe", "dataType":"rfqQuote" }


```json
 1. Create quote:

{    
    "dt": 20,
    "c": 20,
    "d": {
        "createTime": 1755260869424,
        "expiryTime": 1755229404540,
        "updateTime": 1755260869424, // same as createTime if newly created
        "legs": [
            {
                "instrumentName": "BTCUSD-5SEP25-119000-C",
                "price": "1",
                "quantity": "22",
                "side": "BUY"
            },
            {
                "instrumentName": "BTCUSD-22AUG25-119000-C",
                "price": "2",
                "quantity": "11",
                "side": "SELL"
            }
        ],
        "quoteId": "1956331996126527489",
        "requestId": "1956318807450587136",
        "state": "OPEN",
        "userId": "1695796692726153" // this should be the maker's userId
    },
    "ts": 1755260869548
}
```  

```json
2. cancel quote: 

{    
    "dt": 20,
    "c": 20,
    "d": {
        "createTime": 1755443848829,
        "expiryTime": 1755229404540,
        "updateTime": 1755229404540,
        "legs": [
            {
                "instrumentName": "BTCUSD-29AUG25-119000-C",
                "price": "33",
                "quantity": "22",
                "side": "BUY"
            },
            {
                "instrumentName": "BTCUSD-22AUG25-119000-C",
                "price": "44",
                "quantity": "11",
                "side": "SELL"
            }
        ],
        "quoteId": "1957099467376836610",
        "requestId": "1957099347237801984",
        "state": "CANCELLED",
        "userId": "1695796692726153"
    },
    "ts": 1755443859795
}


```  

```json
3. Quote filled: 

{
    "dt": 20,
    "c": 20,
    "d": {
        "createTime": 1755507249763,
        "expiryTime": 1755229404540,
        "updateTime": 1755229404540,
        "legs": [
            {
                "instrumentName": "BTCUSD-29AUG25-116000-C",
                "price": "1",
                "quantity": "111",
                "side": "SELL"
            }
        ],
        "quoteId": "1957365390167916545",
        "requestId": "1957365371585564672",
        "state": "FILLED",
        "userId": "1695796692726153"
    },
    "ts": 1755507257415
}

```  

## RFQ Trade Detail(private)
**Subscribe to this WebSocket channel to receive private blockTrade transaction details.** 

### subscribe
{
    "action":"subscribe",
    "dataType":"blockTradeDetail"
}

### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"blockTradeDetail"
}

```json
Payload:
{
    "dt": 22,
    "c": 20,
    "d": {
        "blockTradeId": "1957110513105780738",
        "quoteId": "1957110513105780738",
        "requestId": "1957110456250404864",
        "role": "MAKER",
        "legs": [
            {
                "baseToken": "BTC",
                "fee": "0",
                "indexPrice": "118293.60725",
                "instrumentName": "BTCUSD-29AUG25-119000-C",
                "iv": "0.0183",
                "markPrice": "2518.45453728",
                "orderId": "1957110512533770240",
                "price": "33",
                "profit": "0",
                "quantity": "22",
                "quoteToken": "USDT",
                "createTime": "1755446489697",
                "tradeId": "1957110543978504192",
                "side": "BUY",
            },
            {
                "baseToken": "BTC",
                "fee": "0",
                "indexPrice": "118293.60725",
                "instrumentName": "BTCUSD-22AUG25-119000-C",
                "iv": "0.0413",
                "markPrice": "1374.04138652",
                "orderId": "1957110512600879104",
                "price": "44",
                "profit": "0",
                "quantity": "11",
                "quoteToken": "USDT",
                "createTime": 1755446490017,
                "tradeId": "1957110545320681472",
                "side": "SELL",
            }
        ],
        "userId": "1695796692726153"
    },
    "ts": 1755446491444
}

```


## RFQ Trade Detail(public) 
**Subscribe to this WebSocket channel to receive all blockTrade transaction details.**  

### subscribe
{
    "action":"subscribe",
    "dataType":"blockTradePublic"
}

### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"blockTradePublic"
}

```json
Payload:
{
    "dt": 23,
    "c": 20,
    "d": {
        "requestId": 1957108525360615424,
        "legs": [
            {
                "baseToken": "BTC",
                "indexPrice": "118246.51",
                "instrumentName": "BTCUSD-29AUG25-119000-C",
                "iv": "0.0198",
                "markPrice": "2494.75991149",
                "price": "33",
                "quantity": "22",
                "quoteToken": "USDT",
                "createTime": 1755446402009,
                "side": "SELL",
            },
            {
                "baseToken": "BTC",
                "indexPrice": "118246.51",
                "instrumentName": "BTCUSD-22AUG25-119000-C",
                "iv": "0.0434",
                "markPrice": "1359.43197954",
                "price": "44",
                "quantity": "11",
                "quoteToken": "USDT",
                "createTime": 1755446402155,
                "side": "BUY",
            }
        ],
    },
    "ts": 1755446403440
}

```