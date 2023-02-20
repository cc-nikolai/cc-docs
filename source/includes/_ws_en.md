# WebSocket

## options

<aside class="notice">

</aside>

| Name  |Description  |
| --- | --- |
| c | Request  |
| rc | Response code  |
| d | Request / Response payload  |
|  s | Symbol |
| pr|Price|
| ts | Timestamps|
| v | Volume |
| oi | Open interest|
| cr| Change in percentage|
| cv | Change in value|
| mp|Mark price|
| lp|Last price|
| biv|Bid implied volatility|
| aiv|Ask implied volatility|
| u|User ID|
| b|Balance|
| pe|K-line period|


```
Endpoint：ws://ws.coincall.com/options?apiKey=xx&code=10

Heartbeats

{
 "c":11 // Required
}


Heartbeats response

{
 "c":11 // Required
 "rc":1 // Required  1-Sucsess Other-Fail
}


Subscribe spot price

{
 "c":20      
 "dt":30                
 "d":{s:["BTCUSD","ETHUSD"]}   
}


Subscribe Kline data  

{
 "c":20      
 "dt":2                 
 "d":{s:"BTC-7FEB23-20500-P",pe:"m1"}   
}


Kline response

{
 "c":20
 "dt":2
 "d":{
    period:"m1",
    high:1000,
    open:999,
    low:433,
    close:122, 
    s:BTC-7FEB23-20500-P, //Option name
    v:23323 // Volume
    ts:121212233 // Time of open
 }
}


Subscribe order book

{
 "c":20      
 "dt":5               
 "d":{s:"BTC-7FEB23-20500-P"}   
}


order book response
  

{
 "c":20
 "dt":32,    
 "p":1,
 "d":[{
    "bids": [
      {
        "v":222
        "pr":40000.13
      }
    ],
    "asks": [
      {
        "v":1.23
        "pr":40000.69
      }
    ],
    s:BTC-7FEB23-20500-P // Option name
    ts:133434 //  Timestamps
 }]
}


Subscribe last trade

{
 "c":20      
 "dt":6               
 “d":{s:"BTCUSD"}   
}

last trade Response
  

{
 "c":20
 "dt":6,    
 "d":[{
      "s": "BTC-7FEB23-20500-P",
      "pr":40001.35
      "v":1.93
      "ts": 1653004526965,
      "sd":1
    }]
}



Subscribe option chain pricing

{
 "c":20      
 "dt":4               
 "d":{s:"BTC-7FEB23-20500-P"}   
}


Push service of option chain pricing
  
{
	"dt": 4,
	"c": 20,
	"d": [{
		"tv": 0E-8,// Trade volume
		"mp": 3920.08500000,// Mark price
		"lp": 0,// Last price
		"delta": 1.00,
		"theta": 0.00,
		"biv": 0.0,//bid iv
		"aiv": 0.0,// ask iv
		"s": "BTCUSD-6FEB23-19000-C", // Option name
		"bv": 0,//
		"av": 0,
		"ask": 0,
		"oi": 0,
		"upv": 0,
		"bid": 0,
		"gamma": 0.00,
		"vega": 0.00,
		"ts": 1675689068531
	}]
}



Subscribe B-S model pricing

{
 "c":20      
 "dt":3               
 “d":{s:"BTCUSD-6FEB23-19000-C"}   
}


Push service of a particular option

{
 "c":20
 "dt":3,
 "d":{  
    "v":1000
    "oi":999
    iv:433,           
    delta:122,        
    gamma:11,         
    vega:23323,      
    theta:121212233,
    cr:1,// Change in percentage 
    cv:1,// Change in value
    s:BTCUSD-6FEB23-19000-C,
    ts:1222,
 }
}



Subscribe account balance

{
 "c":20      
 "dt":7                
}


Account balance response
  
{
	"dt": 7,
	"c": 20,
	"d": {
		"mm": 0,
		"ab": 200000.00000000,
		"im": 0,
		"u": 7882585330726010026,
		"e": 200000.00000000,
		"mb": 200000.00000000,
		"delta": "0",
		"upnl": 0 // Unrealized PnL
	}
}

```

## futures

<aside class="notice">

</aside>

| Name  | Description |
| --- | --- |
| c | Request |
| rc | Response code |
| d | Request / Response payload |
| p | Position of the data subscribed |
| s | Symbol of contract |
| pr | Price |
| ts | Timestamps |
| v | Volume |
| oi | Open interest |
| cr | Change in percentage |
| cv | Change in value |
| mp | Mark price |
| lp | Last price |
| u | User ID |
| pe | Kline period |

  
```  
Kline period：ws://ws.coincall.com/futures?apiKey=xx&code=10

 Heartbeats

{
 "c":11 // Required
}

 Hearbeats response


{
 "c":11 // Required
 "rc":1 // Required  1-Sucsess Other-Fail
}


Subscribe spot price

{
 "c":20      
 "dt":30                
 "d":{s:["BTCUSD","ETHUSD"]}   
}


Subscribe Kline data  

{
 "c":20      
 "dt":31                  
 "d":{s:"BTCUSD",pe:"m1"}   
}

Response of Kline data
{
 "c":20
 "dt":31
 "p":1,
 "d":{
    high:1000,
    open:999,
    low:433,
    close:122, 
    s:BTCUSD, // Symbol
    v:23323 // Volume
    ts:121212233 // Timestamp of open
 }
}


Subscribe order book

{
 "c":20      
 "dt":32               
 "d":{s:"BTCUSD"}   
}


Response of order book 
  

{
 "c":20
 "dt":32,    
 "p":1,
 "d":[{
    "bids": [
      {
        "v":222
        "pr":40000.13
      }
    ],
    "asks": [
      {
        "v":1.23
        "pr":40000.69
      }
    ],
    s:BTCUSD // Symbol
    ts:133434 // Timestamp
 }]
}


Subscribe last trade

{
 "c":20      
 "dt":33               
 "d":{s:"BTCUSD"}   
}

Response of last trade

{
 "c":20
 "dt":33,    
 "p":1,
 "d":[{
      "s": "BTCUSD",
      "pr":40001.35
      "v":1.93
      "ts": 1653004526965,
      "sd":1
    }]
}

```
 

 


