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
    auth = verb + uri + '?uuid=' + api_key + '&ts=' + str(ts)
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

## RFQ list
### subscribe
{
    "action":"subscribe",
    "dataType":"blockTrade"
}
### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"blockTrade"
}

```json
Payload:

// New Order msgType:1
{
    "dt": 20,
    "c": 20,
    "d": {
        "msg": {
            "msgType": 1,  //-1 - UNKNOWN，1 - ADD_SEEK，2 - CANCEL_SEEK，3 - EXPIRE_CANCEL_SEEK，4 - ADD_QUOTE，5 - CANCEL_QUOTE，6 - EXPIRE_CANCEL_QUOTE，7 - DEAL_NOTIFY_MARKET_MAKER，8 - MSG_FOR_MARKET_MAKER，9 - MSG_FOR_COMMONUSER
            "content": {
                "seekVOList": [
                    {
                        "symbol": "BTCUSD-11OCT24-64000-C",
                        "amount": 0.1,
                        "role": 1,
                        "tradeSide": 1,
                        "displayName": "BTC-11OCT24-64000-C",
                        "seekId": 1840692011045359616,
                        "uid": 8098448373,
                        "price": 1986.02321251,
                        "ctime": 1727690148510,
                        "id": 1840692011118247938,
                        "state": 0,
                        "underSymbol": "BTC",
                        "tradeType": 1
                    }
                ],
                "endTime": 1727691948510,
                "seekId": 1840692011045359616
            }
        }
    },
    "ts": 1727690148550
}

// Cancel Order msgType:2
{
    "dt": 20,
    "c": 20,
    "d": {
        "msg": "{"msgType":2,"content":[1840692011045359616]}"
    },
    "ts": 1727690155297
}

```

## K-line Data
### subscribe
{
    "action":"subscribe",
    "dataType":"kline",
    "payload":{
        "symbol":"BTCUSD-27MAY23-24000-P",
        "period":"h1"
    }
}
### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"kline",
    "payload":{
        "symbol":"BTCUSD-27MAY23-24000-P",
        "period":"h1"
    }
}

```json
Payload:

{
    "dt": 2,
    "c": 20,
    "d": {
        "high": 4056.40850000, // The highest price
        "s": "BTCUSD-4JUL23-27000-C", // symbol 
        "low": 4056.40850000, // The lowest price
        "pe": "m1", // period
        "v": 0, // volume 
        "close": 4056.40850000, // close price
        "open": 4056.40850000, // open price
        "ts": 1688449080000 // timestamp
    }
}

```

## Pricing Information
### subscribe
{
    "action":"subscribe",
    "dataType":"bsInfo",
    "payload":{
        "symbol":"BTCUSD-27MAY23-23500-C"
    }
}

### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"bsInfo",
    "payload":{
        "symbol":"BTCUSD-27MAY23-23500-C"
    }
}

```json
Payload:

{
    "dt": 3,
    "c": 20,
    "d": {
        "uv": 30783000.00000000, // tradeValue
        "rt": 2081914160, // remian timestamp
        "mp": 834.28262809, // markPrice 
        "lp": 834.29106136, // last price 
        "ip": 31059.68000000, // indexprice 
        "delta": 0.34898, // delta
        "h": 783.67149194, // price24hHigh, Highest price in 24hrs
        "l": 665.61113639, // price24hLow, Lowest price in 24hrs
        "iv": 0.4728, // Implied Volatility
        "theta": -29.14546, // theta
        "cp": -64.84120504, // changePrice, Price change in value
        "pr0": 899.13226640, // price24hOpen, Open price on UTC 00:00:00
        "cr": -0.0721, // changeRate, Price change in percentage
        "s": "BTCUSD-28JUL23-33000-C", // symbol
        "uv24": 30783000.00000000, // volumeUsd24h, USD volume in 24hrs
        "v": 1000.00000000, // volume
        "v24": 1000.00000000, // volume24h, Volume in 24hrs
        "oi": 1000.00000000, // openInterest
        "up": 31248.97, // underlyingPrice
        "gamma": 0.00010, // gamma
        "vega": 29.70793, // vega
        "ts": 1688449285840 // timestamp
    }
}

```

## Option Chain Data
### subscribe
{
    "action":"subscribe",
    "dataType":"tOption",
    "payload":{
        "symbol":"BTCUSD",
        "end":1685174400000
    }
}

### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"tOption",
    "payload":{
        "symbol":"BTCUSD",
        "end":1685174400000
    }
}

```json
Payload:

{
    "dt": 4,
    "c": 20,
    "d": [{
        "mp": 4038.58550000, // markPrice 
        "lp": 4038.58550000, // last price 
        "delta": 1.00000, // delta
        "theta": 0.00000, // theta
        "cp": -124.21240000, // changePrice, Price change in value
        "biv": 0.01, // bidIv, Best bid IV
        "aiv": 0.01, // askIv, Best ask IV
        "cr": -0.0298, // changeRate, Price change in percentage
        "bs": 0.2, // bidSize, Best bid size
        "as": 0, // askSize, Best ask size
        "s": "BTCUSD-4JUL23-27000-C", // symbol 
        "v": 1.00000000, // volume
        "ask": 0, // ask, Best ask price
        "v24": 1.00000000, // volume24h, Volume in 24hrs
        "oi": 1.00000000, // openInterest
        "upv": 0,
        "up": 31038.5855, // underlyingPrice
        "bid": 1, // bid, Best bid price
        "gamma": 0.00000, // gamma
        "vega": 0.00000, // vega
        "ts": 1688452774463 // timestamp
    }]
}

```

## OrderBook
### subscribe
{
    "action":"subscribe",
    "dataType":"orderBook",
    "payload":{
        "symbol":"BTCUSD-27MAY23-26000-C"
    }
}
### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"orderBook",
    "payload":{
        "symbol":"BTCUSD-27MAY23-26000-C"
    }
}

**Update Speed: 100ms**

Message channel for the 100 best ask/bid full data.

```json
Payload:

{
    "dt": 5,
    "c": 20,
    "d": {
        "s": "BTCUSD-4JUL23-27000-C", // symbol
        "asks": [{
            "pr": "4038.58", // price 
            "sz": "1" // size 
        }],
        "bids": [{
            "pr": "1",
            "sz": "0.2"
        }],
        "ts": 1688453641701 // timestamp
    }
}

```

## Last Trades
### subscribe
{
    "action":"subscribe",
    "dataType":"lastTrade",
    "payload":{
        "symbol":"BTCUSD-27MAY23-26000-C"
    }
}
### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"lastTrade",
    "payload":{
        "symbol":"BTCUSD-27MAY23-26000-C"
    }
}

```json
Payload:

{
    "dt": 6,
    "c": 20,
    "d": [{
        "q": "1", // qty, quantity
        "sd": 1, // tradeSide
        "pr": "2757.03", // price
        "s": "BTCUSD-4JUL23-27000-C", // symbol
        "ts": 1688454356810 // timestamp
    }]
}

```

## Real-Time Account Margin
### subscribe
{
    "action":"subscribe",
    "dataType":"accountBalance"
}

### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"accountBalance"
}

```json
Payload:
{
	"dt": 7,
	"c": 20,
	"d": {
		"mm": 3.18161452, // pmMmAmount maintenanceMargin in PM
		"uid": 8095151726, // UID
		"ab": 49999781762.68412425, // available balance
		"dv": 49999935154.66088082, // Value in dollar
		"assets": [{
			"availableBalance": 138.00000000,
			"coin": "XRP"
		}, {
			"availableBalance": 3999989.00000000,
			"coin": "TRX"
		}, {
			"availableBalance": 49999781762.68412425,
			"coin": "USDT"
		}],
		"im": 1762.52258038, // pmImAmount initialMargin in PM
		"e": 49999935154.66088082, // equityAmount 
		"mb": 49999783525.20670463, // marginBalance
		"delta": "0",
		"btcv": 1448491.54875762, // btc value
		"wb": 49999781762.68412425, // canWithdrawPmAmount 
		"upnl": 49325.72664219 // unrealizedAmount 
	}
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
    "action":"unSubscribe",
    "dataType":"order"
}

```json
Payload:

Status: 0 NEW
{
  "dt": 11,
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
    "os": 0, //Status NEW
    "tif": 0 //timeInForce 0 - GTC ,  1 - GTC (POSTONLY) , 2 - IOC , 3 - FOK
  }
}

Status: 1 FILLED
{
  "dt": 11,
  "c": 20,
  "d": {
    "oid": 1665910350698258432,// Order ID
    "coid": 123123123,// Client order id
    "uid": "8095151726", // User id
    "s": "BTCUSD-6JUN23-24000-C",// Option symbol name
    "rq":"0.5",// Unfilled Quantity
    "fq": "0",// Filled Quantity
    "q": "0.5",// Order Quantity
    "pr": "2095.6",// Price
    "mpr": "499", // filled price in this trade
    "mq": "0.5", // filled quantity in this trade
    "ap": "2095.6",// Average price
    "si": 1,// Trade side
    "ty": 1,// Trade type
    "ct": 1666667584739,// Time of the order created
    "ts": 1685326195118,// Time of this event
    "ro": 0, // Reduce only
    "it": 0, // Taker or Maker, 1 TRUE 0 FALSE
    "os": 1, // FILLED
    "tif": 0 //timeInForce 0 - GTC ,  1 - GTC (POSTONLY) , 2 - IOC , 3 - FOK
  }
}

Status: 2 PARTIALLY_FILLED
{
  "dt": 11,
  "c": 20,
  "d": {
	"oid": 1665910350698258432,// Order ID
    "coid": 123123123,// Client order id
	"uid": "8095151726", // User id
    "s": "BTCUSD-6JUN23-24000-C",// Option symbol name
    "rq":"0.5",// Unfilled Quantity
    "fq": "0",// Filled Quantity(accumulated)
	"q": "0.5",// Order Quantity
    "pr": "2095.6",// Price
	"mpr": "499", // filled price in this trade
	"mq": "0.5", // filled quantity in this trade
    "ap": "2095.6",// Average filled price(accumulated)
    "si": 1,// Trade side
    "ty": 1,// Trade type
    "ct": 1666667584739,// Time of the order created
	"ts": 1685326195118,// Time of this event
    "ro": 0, // Reduce only
	"it": 0, // Taker or Maker, 1 TRUE 0 FALSE
	"os": 2, // PARTIALLY_FILLED
    "tif": 0 //timeInForce 0 - GTC ,  1 - GTC (POSTONLY) , 2 - IOC , 3 - FOK
  }
}

Status: 3 CANCELED, 10 CANCEL_BY_EXERCISE
{
  "dt": 11,
  "c": 20,
  "d": {
    "oid": 1665910350698258432,// Order ID
    "coid": 123123123,// Client order id
	"uid": "8095151726", // User id
    "s": "BTCUSD-6JUN23-24000-C",// Option symbol name
	"cq": "0.5", // Canceled Quantity
    "fq": "0",// Filled Quantity(accumulated)
	"q": "0.5",// Order Quantity
    "pr": "2095.6",// Price
    "ap": "2095.6",// Average filled price(accumulated)
    "si": 1,// Trade side
    "ty": 1,// Trade type
    "ct": 1666667584739,// Time of the order created
	"ts": 1685326195118,// Time of this event
    "ro": 0, // Reduce only
	"os": 3, // 3 CANCELED, 10 CANCEL_BY_EXERCISE
    "tif": 0 //timeInForce 0 - GTC ,  1 - GTC (POSTONLY) , 2 - IOC , 3 - FOK
  }
}

Status: 6 INVALID
{
  "dt": 11,
  "c": 20,
  "d": {
    "oid": 1665910350698258432,// Order ID
    "coid": 123123123,// Client order id
	"uid": "8095151726", // User id
    "s": "BTCUSD-6JUN23-24000-C",// Option symbol name
    "rq":0.5,// Unfilled Quantity
	"q": 0.5,// Order Quantity
    "fq": 0,// Filled Quantity(accumulated)
    "pr": 2095.6,// Price
    "ap": 2095.6,// Average filled price(accumulated)
    "si": 1,// Trade side
    "ty": 1,// Trade type
    "ct": 1666667584739,// Time of the order created
	"ts": 1685326195118,// Time of this event
    "ro": 0, // Reduce only
	"os": 6, // INVALID
    "tif": 0 //timeInForce 0 - GTC ,  1 - GTC (POSTONLY) , 2 - IOC , 3 - FOK
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
    "action":"unSubscribe",
    "dataType":"trade"
}

```json
Payload:

{
	"dt": 15,
	"c": 20,
	"d": {
		"clientOrderId": "1734123406279839744",
		"feeRate": "-0.0006",
		"isTaker": "0",
		"matchPrice": "22180",
		"matchQty": "2",
		"matchValue": "44360",
		"orderId": "1734123406279839744",
		"orderSide": "1",
		"remainQty": "0",
		"symbol": "BTCUSD-22DEC23-20000-C",
		"tradeId": "1734129035131924480",
		"tradeTime": "1702282213169"
	}
}

```

## Position
### subscribe
{
    "action":"subscribe",
    "dataType":"position"
}

### unsubscribe
{
    "action":"unSubscribe",
    "dataType":"position"
}

```json
Payload:

{
    "dt": 12,
    "c": 20,
    "d": {
        "ap": "0.3435", // average price
        "elp": -63.31,  // Elp estimated Liquidation Price
        "im": "0.458", // Im initMargin 
        "mm": "0.04122", // Mm maintMargin 
        "mp": 0.3435, // mark price 
        "os": "5", // postition statues 1 - opening 5 - close
        "q": "0",  // filled quantity,Current quantity of this position, after any position changes. Snapshot value, not a delta.
        "s": "BTCUSD-12JUL24-63000-C",  // symbol
        "si": "1", // side 交易方向 1 - long 2 - short
        "tim": "", //Initial margin in this currency
        "tmm": "", //Maintenance margin in this currency
        "uid": "8098470908", // user id
        "upnl": "0",  // Unrealized Pnl calculated at the lastPrice
        "pnlbmp": "0",  // Unrealized Pnl  calculated at the markprice
        "roibmp": "0",  // Roi calculated at the markprice
        "rho": "0.009074", //greek letters
        "vega": "0.021028",//greek letters
        "delta": "0.09202", //greek letters
        "gamma": "1.05E-4", //greek letters
        "theta": "-3.583298" //greek letters
    },
    "ts": 1719908110173
}

```
