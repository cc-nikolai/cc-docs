# Public Endpoints

## Get Public Configurations

Get trading-related configuration

> Response:

```json
{
  "code": 1,
  "msg": "Success",
  "i18nArgs": null,
  "data": {
    // Options configuration
    "optionConfig": {
      "BTCUSD": {
        "volumeDecimal": 2,// Decimal of the volume
        "symbol": "BTCUSD",// Symbol
        "takerFee":0.0003,// Taker fee
        "multiplier": 0.01,// Multiplier
        "settle": "USD",// Settlement currency
        "limitMaxVolume": 1000,// Limit of the maximum volume
        "priceDecimal": 2,// Price decimal
        "maxVolume": 1000,// Maximum volume
        "tickDecimal": 1,// Ticker decimal
        "tickSize": 0.1,// Tick size
        "greeksDecimal": 6,// Greeks decimal
        "marketMaxVolume": 1000,//
        "makerFee":-0.0001,//Maker fee
        "maxOrderSize": 200,// Maximum order size
        "base": "BTC"// Base token
      }
    },
    // Futures Configuration
    "futuresConfig": {
      "BTCUSD": {
        "volumeDecimal": 3,// Volume Decimal
        "symbol": "BTCUSD",// Symbol
        "marketMaxVolume": 100,//
        "minVolume": 0.001,// Minimum volume
        "settle": "USD",// Settlement currency
        "positionVolume":40000000,
        "triggerLimit":20,
        "maxOrderSize": 200,// Maximum order size
        "priceDecimal": 2,// Price decimal
        "limitMaxVolume": 1000,// Limit of the maximum volume
        "tickDecimal": 1,// ticker decimal
        "base": "BTC",// Base token
        "tickSize": 0.1// Tick size
      }
    }
  }
}
```


### HTTP Request

`GET https://api.coincall.com/open/public/config/v1`

**Parameter**

Null

## Get Funding Rate

Get real-time funding rates

> Response:

```json
{
  "code": 0,// Status code
  "msg": "Success",// Message
  "i18nArgs": null,
  "data": [
    {
      "symbol": "BTCUSD",// Symbol
      "rate": "-0.00500000",// Margin rate
      "contractId": "1"// Contract ID
    }
  ]
}
```

### HTTP Request

`GET https://api.coincall.com/open/public/fundingRate/v1`

**Parameter**

Null
