# Options WebSocket

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

Please refer to the following field abbreviations for data fields in the futures request/response:

| Name | Note |
| --- | --- |
| c | code, Operations for Request Protocol Execution |
| rc | responseCode, Status of the Response Protocol |
| d | data, Request/Response payload |
| p | position, Subscription Data Page Location |
| s | symbol |
| high | high, The highest price |
| low | low, The lowest price |
| pe | period, granularity of K-line |
| v | volume |
| close | close price |
| open | open price |
| ts | timestamp |
| uv | tradeValue |
| rt | rt, remian timestamp |
| mp | markPrice |
| lp | lastPrice |
| ip | indexPrice |
| delta | delta |
| iv | Implied Volatility |
| theta | theta |
| cp | changePrice, Price change in value |
| pr0 | price24hOpen, Open price on UTC 00:00:00 |
| cr | changeRate, Price change in percentage |
| uv24 | volumeUsd24h, USD volume in 24hrs |
| v24 | volume24h, Volume in 24hrs |
| oi | openInterest |
| up | underlyingPrice |
| gamma | gamma |
| vega | vega |
| biv | bidIv, Best bid IV |
| aiv | askIv, Best ask IV |
| bs | bidSize, Best bid size |
| as | askSize, Best ask size |
| ask | ask, Best ask price |
| bid | bid, Best bid price |
| pr | price, last price |
| sz | size |
| sd | tradeSide |
| q | qty, quantity |
| fq | fill qty |
| mm | pmMmAmount, maintenanceMargin in PM |
| ab | available balance |
| e | equityAmount |
| mb | marginBalance  |
| btcv | btc value |
| wb | canWithdrawPmAmount |
| atwt | availableTradeWithTrail |
| upnl | Unrealized Pnl |
| ap | average proce |
| coid | clientOrderId |
| os |  order status |
| im | initialMargin in PM |
| dv | Value in dollar |
| oid | orderId |
| si | trade side |
| ty | trade type |
| uid | userId |
| ct | createTime |
| ro | reduceOnly |
| tid | trade ID |
| rq | remainQty, Unfilled Quantity |
| mpr | match price |
| mq | match quantity |
| le | leverage |
| it | isTaker |
| cq | canceled quantity |
| tif | time in force |


<!-- ## options -->

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