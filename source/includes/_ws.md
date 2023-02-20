# WebSocket

## options

<aside class="notice">
    字段说明
</aside>

| 简写  |说明  |
| --- | --- |
| c | 请求协议执行的操作  |
| rc | 返回协议的状态--response code  |
| d | 请求/返回的payload  |
|  s | symbol 产品名称 |
| pr|价格|
| ts | 时间戳|
| v | volume 交易量|
| oi | 开仓量|
| cr| 涨跌幅度|
| cv | 涨跌量|
| mp|标记价格|
| lp|最新价格|
| biv|bid 隐含波动率|
| aiv|ask 隐含波动率|
| u|用户编码|
| b|balance 余额|
| pe|K线period|


```
接口地址：ws://ws.coincall.com/options?apiKey=xx&code=10

心跳


{
 "c":11 //必填
}

心跳响应


{
 "c":11 //必填
 "rc":1 //必填  1-成功 其他失败
}


订阅现货价格

{
 "c":20      
 "dt":30                
 "d":{s:["BTCUSD","ETHUSD"]}   
}


订阅k线数据   

{
 "c":20      
 "dt":2                 
 "d":{s:"BTC-7FEB23-20500-P",pe:"m1"}   
}


k线响应


{
 "c":20
 "dt":2
 "d":{
    period:"m1",
    high:1000,
    open:999,
    low:433,
    close:122, 
    s:BTC-7FEB23-20500-P, //标的名称
    v:23323 //交易量
    ts:121212233 //开盘时间
 }
}


订阅order book

{
 "c":20      
 "dt":5               
 "d":{s:"BTC-7FEB23-20500-P"}   
}


order book 响应
  

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
    s:BTC-7FEB23-20500-P //标的名称
    ts:133434 时间戳
 }]
}


订阅last trade

{
 "c":20      
 "dt":6               
 “d":{s:"BTCUSD"}   
}

last trade 响应
  

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



订阅T型报价表核心数据

{
 "c":20      
 "dt":4               
 "d":{s:"BTC-7FEB23-20500-P"}   
}

    
推送T型报价表期权bs定价数据
  

{
	"dt": 4,
	"c": 20,
	"d": [{
		"tv": 0E-8,//交易量
		"mp": 3920.08500000,//标记价格
		"lp": 0,//最新价
		"delta": 1.00,
		"theta": 0.00,
		"biv": 0.0,//bid iv
		"aiv": 0.0,// ask iv
		"s": "BTCUSD-6FEB23-19000-C", //期权名
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



订阅bs定价信息

{
 "c":20      
 "dt":3               
 “d":{s:"BTCUSD-6FEB23-19000-C"}   
}


推送单个期权bs定价数据

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
    cr:1,//涨跌幅 
    cv:1,//涨跌量
    s:BTCUSD-6FEB23-19000-C,
    ts:1222,
 }
}



订阅账户余额

{
 "c":20      
 "dt":7                
}


账户信息响应
  
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
		"upnl": 0 //未实现盈亏
	}
}

```

## futures

<aside class="notice">
    字段简写说明
</aside>

| 简写  | 说明 |
| --- | --- |
| c | 请求协议执行的操作 |
| rc | 返回协议的状态--response code |
| d | 请求/返回的payload |
| p | 订阅数据的页面位置，position |
| s | symbol 合约名称 |
| pr | 价格 |
| ts | 时间戳 |
| v | volume 交易量 |
| oi | 开仓量 |
| cr | 涨跌幅度 |
| cv | 涨跌量 |
| mp | 标记价格 |
| lp | 最新价格 |
| u | 用户编码 |
| pe | K线period |

  
```  
接口地址：ws://ws.coincall.com/futures?apiKey=xx&code=10

 心跳

{
 "c":11 //必填
}

 心跳响应


{
 "c":11 //必填
 "rc":1 //必填  1-成功 其他失败
}


订阅现货价格

{
 "c":20      
 "dt":30                
 "d":{s:["BTCUSD","ETHUSD"]}   
}


订阅k线数据   


{
 "c":20      
 "dt":31                  
 "d":{s:"BTCUSD",pe:"m1"}   
}

k线响应
{
 "c":20
 "dt":31
 "p":1,
 "d":{
    high:1000,
    open:999,
    low:433,
    close:122, 
    s:BTCUSD, //标的名称
    v:23323 //交易量
    ts:121212233 //开盘时间
 }
}

订阅order book

{
 "c":20      
 "dt":32               
 "d":{s:"BTCUSD"}   
}


order book 响应
  

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
    s:BTCUSD //标的名称
    ts:133434 时间戳
 }]
}


订阅last trade

{
 "c":20      
 "dt":33               
 "d":{s:"BTCUSD"}   
}

last trade 响应


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
 

 


