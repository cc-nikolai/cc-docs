# WebSocket

* 适用于期权的wss接口：wss://ws.coincall.com/options

  * 连接示例：wss://ws.coincall.com/options?code=10&apiKey=xxx

* 适用于合约的wss接口：wss://ws.coincall.com/futures

  * 连接示例：wss://ws.coincall.com/futures?code=10&apiKey=xxx

**Options**

<aside class="notice">
    期权请求响应中数据字段请参照以下字段简写说明：
</aside>

| 简写 | 说明 |
| --- | --- |
| c | code，请求协议执行的操作 |
| rc | responseCode，返回协议的状态 |
| d | data，请求/返回的payload |
| p | position，订阅数据的页面位置 |
| s | symbol，产品名称 |
| pr | price，价格 |
| ts | timestamp，时间戳 |
| v | volume，交易量 |
| oi | openInterest，开仓量 |
| cr | changeRate，涨跌幅度 |
| cv | changeVolume，涨跌量 |
| mp | markPrice，标记价格 |
| lp | lastPridce，最新价格 |
| biv | bidIv，隐含波动率 |
| aiv | askIv，隐含波动率 |
| u | user，用户编码 |
| b | balance，余额 |
| pe | period，K线颗粒度 |
| si | side，订单方向 |
| am | amount，数量 |
| ap | avgPrice，平均价 |
| elp | estimatedLiquidationPrice，预估爆仓价 |
| pnl | profitAndLoss，盈亏 |
| im | initialMargin初始保证金 |
| mm | maintenanceMargin维持保证金 |
| uid | userId，用户id |

**Futures**

<aside class="notice">
    合约请求响应中数据字段请参照以下字段简写说明：
</aside>

| 简写 | 说明 |
| --- | --- |
| c | code，请求协议执行的操作 |
| rc | response code，返回协议的状态 |
| d | data，请求/返回的payload |
| p | position，订阅数据的页面位置 |
| s | symbol，合约名称 |
| pr | price，价格 |
| ts | timestamp，时间戳 |
| v | volume，交易量 |
| oi | openInterest，开仓量 |
| cr | changeRate，涨跌幅度 |
| cv | changeVolume，涨跌量 |
| mp | markPrice，标记价格 |
| lp | lastPrice，最新价格 |
| u | user，用户编码 |
| pe | period，K线颗粒度 |
| si | side，订单方向 |
| am | amount，数量 |
| ap | avgPrice，平均价 |
| elp | estimatedLiquidationPrice，预估爆仓价 |
| pnl | profitAndLoss，盈亏 |
| im | initialMargin，初始保证金 |
| mm | maintenanceMargin，维持保证金 |
| uid | userId，用户id |

## 期权. 订阅现货指数价格
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
    "dt":7,
    "c":20,
    "d":{
        "mm":0,
        "ab":100000000000,
        "dv":100000000000,
        "im":0,
        "u":9804819366,
        "e":100000000000,
        "mb":100000000000,
        "delta":"0",
        "btcv":3791193.92847875,
        "wb":100000000000,
        "upnl":0
    }
}
```

## 期权. 订阅k线数据
{
    "action":"subscribe",
    "dataType":"kline",
    "payload":{
        "symbol":"BTCUSD-27MAY23-24000-P",
        "period":"h1"
    }
}

```json
Payload:

{
    "dt":2,
    "c":20,
    "d":{
        "high":0.62451964,
        "s":"BTCUSD-27MAY23-24000-P",
        "low":0.47677071,
        "pe":"h1",
        "v":0,
        "close":0.57590514,
        "open":0.61780836,
        "ts":1685088000000
    }
}

```

## 期权. 订阅定价信息
{
    "action":"subscribe",
    "dataType":"bsInfo",
    "payload":{
        "symbol":"BTCUSD-27MAY23-23500-C"
    }
}

```json
Payload:

{
    "dt":3,
    "c":20,
    "d":{
        "tv":0,
        "rt":-3178263,
        "mp":0,
        "lp":16507.565,
        "ip":26498.05,
        "delta":0,
        "h":16588.9,
        "l":16194.165,
        "iv":1.1833,
        "theta":0,
        "cp":34.265,
        "pr0":16473.3,
        "cr":0.0021,
        "s":"BTCUSD-26MAY23-10000-C",
        "uv24":0,
        "v24":0,
        "oi":0,
        "up":26498.05,
        "gamma":0,
        "vega":0,
        "tva":0,
        "ts":1685091178263
    }
}

```

## 期权. 订阅T型报价表数据

{
    "action":"subscribe",
    "dataType":"tOption",
    "payload":{
        "symbol":"BTCUSD",
        "end":1685174400000
    }
}

```json
Payload:

{
    "dt":4,
    "c":20,
    "d":[
        {
            "mp":2463.01629839,
            "lp":2462.85874122,
            "delta":0.9979,
            "theta":-3.14435,
            "cp":-13.05416804,
            "biv":1.26,
            "aiv":2.97,
            "cr":-0.0053,
            "s":"BTCUSD-27MAY23-24000-C",
            "bv":0.52,
            "av":8.94,
            "ask":3065.9,
            "oi":0,
            "upv":0,
            "up":26462.455,
            "bid":2499.3,
            "gamma":0.00001,
            "vega":0.08962,
            "ts":1685091838557
        },
        {
            "tv":0.01,
            "mp":0.56129839,
            "lp":0.56374122,
            "delta":-0.0021,
            "theta":-3.14435,
            "cp":-2.04916804,
            "biv":0.5,
            "aiv":0.71,
            "cr":-0.7842,
            "s":"BTCUSD-27MAY23-24000-P",
            "bv":0,
            "av":0.54,
            "ask":1,
            "v24":0.01,
            "oi":0.01,
            "upv":0,
            "up":26462.455,
            "bid":0,
            "gamma":0.00001,
            "vega":0.08962,
            "ts":1685091838557
        }
      ]
}

```

## 期权. 订阅订单薄
{
    "action":"subscribe",
    "dataType":"orderBook",
    "payload":{
        "symbol":"BTCUSD-27MAY23-26000-C"
    }
}

```json
Payload:

{
    "dt":5,
    "c":20,
    "d":{
        "s":"BTCUSD-27MAY23-26000-C",
        "asks":[
            {
                "pr":"486.8",
                "v":0.34
            },
            {
                "pr":"649.1",
                "v":5.28
            },
            {
                "pr":"649.8",
                "v":3.1
            },
            {
                "pr":"651.1",
                "v":1.44
            },
            {
                "pr":"651.7",
                "v":0.55
            },
            {
                "pr":"653.1",
                "v":0.31
            },
            {
                "pr":"653.8",
                "v":0.29
            },
            {
                "pr":"784.6",
                "v":4.98
            }
        ],
        "bids":[
            {
                "pr":"477",
                "v":0.1
            },
            {
                "pr":"476.3",
                "v":9.59
            },
            {
                "pr":"475.6",
                "v":4.98
            },
            {
                "pr":"474.7",
                "v":1.95
            },
            {
                "pr":"473.3",
                "v":0.57
            },
            {
                "pr":"472.5",
                "v":0.59
            },
            {
                "pr":"471.2",
                "v":0.2
            },
            {
                "pr":"377",
                "v":4.71
            }
        ],
        "ts":1685092534839
    }
}

```

## 期权. 订阅最新成交
{
    "action":"subscribe",
    "dataType":"lastTrade",
    "payload":{
        "symbol":"BTCUSD-27MAY23-26000-C"
    }
}

```json
Payload:

{
    "dt":6,
    "c":20,
    "d":[
        {
            "sd":1,
            "pr":486.8,
            "s":"BTCUSD-27MAY23-26000-C",
            "v":0.1,
            "ts":1685092744132
        },
        {
            "sd":2,
            "pr":541.7,
            "s":"BTCUSD-27MAY23-26000-C",
            "v":0.19,
            "ts":1685077759928
        }
    ]
}

```

## 期权. 订阅账户实时保证金
{
    "action":"subscribe",
    "dataType":"accountBalance"
}

```json
Payload:

{
    "dt":7,
    "c":20,
    "d":{
        "mm":0,
        "ab":99999999902.0327645,
        "dv":100000000000.50153541,
        "im":47.7,
        "u":9804819366,
        "e":100000000000.50153541,
        "mb":99999999950.52660785,
        "delta":"0",
        "btcv":3781378.82686887,
        "wb":99999999902.0327645,
        "upnl":1.29492756
    }
}

```

## 期权. 订阅成交信息
{
    "action":"subscribe",
    "dataType":"fillSignal",
    "payload":{
        "symbol":"BTCUSD-27MAY23-26000-C"
    }
}

```json
Payload:

{
    "dt":8,
    "c":20,
    "d":{
        "s":"BTCUSD-27MAY23-26000-C",
        "et":2,
        "ts":1685092951072
    }
}

```

## 期权. 订阅订单
{
"action":"subscribe",
"dataType":"order"
}

```json
Payload:

```

## 期权. 订阅仓位
{
"action":"subscribe",
"dataType":"position",
"payload":{"symbol":["BTCUSD","ETHUSD"]}
}

```json
Payload:

```

<!-- ## futures -->

## 期货. 订阅现货指数价格
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
    "dt":30,
    "c":20,
    "d":{
        "pr":26443.9,
        "mp":26429.30181716,
        "lp":26443.9,
        "ip":26453.83,
        "h":26609.9,
        "l":26163.7,
        "cp":-20.4,
        "cr":-0.0008,
        "pr0":23799.51,
        "s":"BTCUSD",
        "cv":"0",
        "uv24":447242963.9206,
        "v24":16958.582
    }
}

```

## 期货. 订阅k线数据
{
    "action":"subscribe",
    "dataType":"kline",
    "payload":{
        "symbol":"BTCUSD",
        "period":"h1"
    }
}

```json
Payload:

{
    "dt":31,
    "c":20,
    "d":{
        "high":26471.7,
        "s":"BTCUSD",
        "low":26422.4,
        "pe":"h1",
        "v":351.656,
        "close":26440.7,
        "open":26461.7,
        "ts":1685091600000
    }
}

```

## 期货. 订阅订单薄
{
    "action":"subscribe",
    "dataType":"orderBook",
    "payload":{
        "symbol":"BTCUSD"
    }
}

```json
Payload:

{
    "dt":32,
    "c":20,
    "d":{
        "s":"BTCUSD",
        "asks":[
            {
                "pr":"26444.4",
                "v":0.686
            },
            {
                "pr":"26444.9",
                "v":0.686
            },
            {
                "pr":"26445.6",
                "v":0.264
            },
            {
                "pr":"26446.2",
                "v":0.684
            },
            {
                "pr":"26446.9",
                "v":0.49
            },
            {
                "pr":"26447.7",
                "v":0.047
            },
            {
                "pr":"26448.2",
                "v":0.346
            },
            {
                "pr":"26448.7",
                "v":0.609
            },
            {
                "pr":"26449.1",
                "v":0.671
            },
            {
                "pr":"26449.6",
                "v":0.824
            },
            {
                "pr":"26450",
                "v":0.69
            },
            {
                "pr":"26450.5",
                "v":0.135
            },
            {
                "pr":"26450.9",
                "v":0.705
            },
            {
                "pr":"26451.4",
                "v":0.38
            },
            {
                "pr":"26451.8",
                "v":0.683
            },
            {
                "pr":"26452.3",
                "v":0.661
            },
            {
                "pr":"26452.7",
                "v":0.321
            },
            {
                "pr":"26453.2",
                "v":0.198
            },
            {
                "pr":"26453.7",
                "v":0.802
            },
            {
                "pr":"26454.4",
                "v":0.244
            }
        ],
        "bids":[
            {
                "pr":"26428.3",
                "v":0.208
            },
            {
                "pr":"26427.9",
                "v":0.348
            },
            {
                "pr":"26427.4",
                "v":0.347
            },
            {
                "pr":"26427",
                "v":0.514
            },
            {
                "pr":"26426.5",
                "v":0.729
            },
            {
                "pr":"26426.1",
                "v":0.789
            },
            {
                "pr":"26425.6",
                "v":0.421
            },
            {
                "pr":"26425.2",
                "v":0.496
            },
            {
                "pr":"26424.6",
                "v":0.558
            },
            {
                "pr":"26424.1",
                "v":0.804
            },
            {
                "pr":"26423.8",
                "v":0.528
            },
            {
                "pr":"26423.2",
                "v":0.094
            },
            {
                "pr":"26422.9",
                "v":0.413
            },
            {
                "pr":"26422.5",
                "v":0.298
            },
            {
                "pr":"26422.3",
                "v":0.009
            },
            {
                "pr":"26422",
                "v":0.816
            },
            {
                "pr":"26421.6",
                "v":0.342
            },
            {
                "pr":"26421.1",
                "v":0.789
            },
            {
                "pr":"26420.7",
                "v":0.742
            },
            {
                "pr":"26420.3",
                "v":0.752
            }
        ],
        "ts":1685094461143
    }
}

```

## 期货. 订阅最新成交
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
    "dt":33,
    "c":20,
    "d":[
        {
            "sd":2,
            "pr":26427.5,
            "s":"BTCUSD",
            "v":0.009,
            "ts":1685096426138
        },
        {
            "sd":2,
            "pr":26427.4,
            "s":"BTCUSD",
            "v":0.064,
            "ts":1685096371947
        }
    ]
}

```

## 期货. 订阅成交信息
{
    "action":"subscribe",
    "dataType":"fillSignal"
}

```json
Payload:

{
    "dt":34,
    "c":20,
    "d":{
        "s":"BTCUSD",
        "et":2,
        "ts":1685096551612
    }
}

```

## 期货. 订阅订单
{
"action":"subscribe",
"dataType":"order"
}

```json
Payload:

```

## 期货. 订阅仓位
{
"action":"subscribe",
"dataType":"position"
}

```json
Payload:

```
