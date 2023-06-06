# Options Endpoint

## Get Option Chain

Get option chain

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": [{
		"strike": 22000.00000000,// Strike price
		"callOption": {
			"optionId": 1584505132356345856,// Option ID
			"underSymbol": "BTCUSD",// Underlying symbol
			"optionName": "BTCUSD-26OCT22-22000-C",// Option name
			"baseToken":"BTC",
			"displayName":"BTC-31MAY23-30000-C",
			"endTime": 1666771200000,// Time of expiration
			"strike": 22000.00000000,// Strike price
			"lastPrice": 0,// Last price
			"markPrice": 0.0,// Mark price
			"tradeVolume": 0,// Trade volume
			"openInterest": 0,// Open interest
			"ask": 0,// Best ask price
			"askIv": 0.0,// Best ask IV
			"askVolume": 0,// Best ask volume
			"bid": 0,// Best bid price
			"bidIv": 0.0,// Best bid IV
			"bidVolume": 0,// Bid volume
			"markIv": 0.0,// Mark IV
			"type": 1,// Option type 1 CALL 2 PUT
			"lastPriceIv": 1.7976931348623157E308,// Last priceIV
			"underlyingPrice": 20278.25,// Price of the underlying
			"breakeven":30000,
			"changeRate":null,
			"changeVolume":null,
			"changePrice":null,
			"userPositionVolume":0,
			"delta": 0.0,//greeks delta
			"gamma": 0.0,//greeks gamma
			"vega": 0.0,//greeks vega
			"theta": 0.0,//greeks theta
			"rho":0
		},
		"putOption": {
			"optionId": 1584505132356345856,// Option ID
			"underSymbol": "BTCUSD",// Underlying symbol
			"optionName": "BTCUSD-26OCT22-22000-C",// Option name
			"baseToken":"BTC",
			"displayName":"BTC-31MAY23-30000-P",
			"endTime": 1666771200000,// Time of expiration
			"strike": 22000.00000000,// Strike price
			"lastPrice": 0,// Last price
			"markPrice": 0.0,// Mark price
			"tradeVolume": 0,// Trade volume
			"openInterest": 0,// Open interest
			"ask": 0,// Best ask price
			"askIv": 0.0,// Best ask IV
			"askVolume": 0,// Best ask volume
			"bid": 0,// Best bid price
			"bidIv": 0.0,// Best bid IV
			"bidVolume": 0,// Bid volume
			"markIv": 0.0,// Mark IV
			"type": 2,// Option type 1 CALL 2 PUT
			"lastPriceIv": 1.7976931348623157E308,// Last priceIV
			"underlyingPrice": 20278.25,// Price of the underlying
			"breakeven":27138.005,
			"changeRate":null,
			"changeVolume":null,
			"changePrice":null,
			"userPositionVolume":0,
			"delta": 0.0,//greeks delta
			"gamma": 0.0,//greeks gamma
			"vega": 0.0,//greeks vega
			"theta": 0.0,//greeks theta
			"rho":-0.02204
		}
	}]
}
```

### HTTP Request

`GET https://api.coincall.com/open/option/get/v1/{}`

**Parameter**

Name  | Value  |  Required  |  Note
-------------- | -------------- | -------------- | --------
endTime | 1666771200000 | true | Expiration time(timestamp)
underlyingSymbol | BTCUSD-26OCT22-22000-C | true | Underlying symbol

## Get Option Details

Get option details

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",
	"i18nArgs": null,
	"data": {
		"optionId": 1584505132293431296,// Option ID
		"optionName": "BTCUSD-26OCT22-20000-P",// Option name
		"underSymbol":"BTCUSD",
        "displayName":"BTC-31MAY23-24000-C",
		"endTime": 1666771200000,// Time of expiration
		"remainTime": 13565073,// Time remain until expiration
		"strike": 20000.00000000,// Strike price
		"markPrice": 10.231632230252217,// Mark price
		"underlyingPrice":27181.6936,
		"tradeVolume": 1.00000000,// Trade volume
		"tradeValue": 1.00000000,// Trade value
		"openInterest": 0,// Open interest
		"lastPrice": 10.231632230252217,// Last price
		"premium": 0,// Premium
		"changeRate": 2.87,// Price change in percentage
		"changeVolume": 473.78165573,// Price change in value
		"changePride":null,
		"iv": 0.58,// Implied volatility
		"multiplier":0.01,
		"type": 2,// Option type 1 CALL 2 PUT
		"indexPrice": 20239.96000000,// Index price
		"price24hHigh": 0,// Highest price in 24hrs
		"price24hLow": 0,// Lowest price in 24hrs
		"volumeUsd24h": 0,// USD volume in 24hrs
		"price24hOpen": 18215.964000000,// Open price on UTC 00:00:00
		"volume24h": 0,// 24h Trade volume
		"breakeven":27171.65,
		"delta": -0.10808987585883545,//greeks delta
		"gamma": 0.0009475995953294489,//greeks gamma
		"vega": 0.7794498985827641,//greeks vega
		"theta": 0.0,//greeks theta
		"rho": -0.009454405809863273,//greeks rho
		"maxDelta": null//max delta
	}
}
```


### HTTP Request

`GET https://api.coincall.com/open/option/detail/v1/{}`

**Parameter**

Name  | Value  |  Required  |  Note
-------------- | -------------- | -------------- | --------
optionName | BTCUSD-26OCT22-15000-C | true | option name


## Get Option Positions(SIGNED)

Get option positions

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": [{
		"id": 1584736851047620608,// ID
		"positionId": 1584736851047620609,// Position ID
		"updateTime": 1666665682934,// Opdate time
		"orderId": 1584736036348895232,// Order ID
		"userId": 1536933707941347382,// User ID
		"value": 11294.2000000000000000,// Value
		"volume": 1.00000000,// Volume
		"closeVolume": 0E-8,// Close volume
		"initMargin": 0,// Initial Margin
		"maintMargin": 0,// Maintnance Margin
		"avgPrice": 11294.20000000,// Average Price
		"markPrice": 12260.310000000001,// Mark price
		"elp": null,// Estimated liquidation Price
		"pnl": 966.11000000000100000000,// Realized PnL
		"roi": 8.55403659,// Return on investment
		"unpl": 966.11000000000100000000,// Unrealized PnL
		"optionName": "BTCUSD-25NOV22-8000-C",// Option name
		"tradeSide": 1,// Trade Side 1 BUY 2 SELL
		"tradeType": 1,// Trade Type 1 LIMIT 2 MARKET
		"lockVolume": 0,// Lock volume
		"delta": 1.0,// greeks delta
		"gamma": 0.0,// greeks gamma
		"vega": 0.0,// greeks vega
		"theta": 0.0,// greeks theta
		"rho": 6.610892947742262// greeks rho
	}]
}
```

### HTTP Request

`GET https://api.coincall.com/open/option/position/get/v1`

**Parameter**

Null

## Place Orders(SIGNED)

Place option orders

> Response:

```json
{
    "code":0,
    "msg":"Success",
    "i18nArgs":null,
    "data":"1663820914095300608"
}
```


### HTTP Request

`POST https://api.coincall.com/open/option/order/create/v1`

**Parameter**


Name  | Value  |  Required  |  Note
-------------- | -------------- | -------------- | --------
optionName | BTCUSD-26OCT22-15000-C | true |  Option name
price | 19000 | false | Price required for limit orders
volume | 0.5 | true | Quantity 
tradeSide | 1 | true | Trade Side 1 BUY 2 SELL
tradeType | 1 | true | Trade Type 1 LIMIT 2 MARKET


## Cancel an Option Order(SIGNED)

Cancel an option order

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data":"success"
}
```


### HTTP Request

`GET https://api.coincall.com/open/option/order/cancel/v1/{}`

**Parameter**

name | value | Required | Note
-------------- | -------------- | -------------- | --------------
orderId | 1663820914095300608 | true | query string


## Get option open orders(SIGNED)

Get option open orders

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": {
		"list":[
			{
				"id": 1665910350698258432,// ID
				"orderId": 1665910350698258432,// Order ID
				"optionName": "BTCUSD-6JUN23-24000-C",// Option name
				"displayName":"BTC-6JUN23-24000-C",// Option display name
				"volume": 0.5,// Volume
				"remainVolume":0.5,// Unfilled volume
				"fillVolume": 0,// Filled volume
				"price": 2095.6,// Price
				"avgPrice": null,// Avrage price
				"initMargin": 1047.8,// Initial Margin
				"tradeSide": 1,// Trade side 1 BUT 2 SELL
				"tradeType": 1,// Trade type 1 LIMIT 2 MARKET
				"createTime": 1666667584739,// Time of the order created
				"isClose":0,
				"indexPrice":25782.815
			}
		],
		"pageTotal":1,
		"total":1
	}
}
```


### HTTP Request

`GET https://api.coincall.com/open/option/order/pending/v1`

**Parameter**

Null

## Get Option Order History(SIGNED)

Get Option Order History

> Response:

```json
{
    "code": 0,// Status code
	"msg": "Success",// Message
    "i18nArgs":null,
    "data":{
        "list":[
            {
                "orderId":1665914294812024832,// Order ID
                "optionName":"BTCUSD-6JUN23-24000-C",// Option name
                "displayName":"BTC-6JUN23-24000-C",// Option display name
                "volume":0.5,// Volume
                "fillVolume":0,// Filled volume
                "price":1900,// Order price
                "avgPrice":null,// Average Price
                "fee":0,// Fees
                "pnl":null,// Realized PnL
                "tradeSide":1,// Trade side
                "tradeType":1,// Trade type
                "createTime":1686019893731,// Time of the order created
                "state":3,// Order status
                "isClose":0
            }
        ],
        "pageTotal":1,
        "total":1
    }
}
```



### HTTP Request

`GET https://api.coincall.com/open/option/order/history/v1/{}`

**Parameter**

Name  | Value  |  Required | Note
-------------- | -------------- | -------------- | --------
pageSize | 10 | true | Quantity per page 
page | 1 | true | Numbe of pages
startTime | 1000000 | true |  Start time of the history
endTime | 200000 | true | End time of the history

## Get Option Order Book

Get option order book

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": {
		"optionName": "BTCUSD-26OCT22-15000-C",// Option name
		"displayName": null,
		"strike": 15000,// Strike price
		"bids": [{
			"volume": 0.5,// Volume
			"price": "5251"// Price
		}],
		"asks": [{
			"volume": 1,// Volume
			"price": "8888"// Price
		}]
	}
}
```


### HTTP Request

`GET https://api.coincall.com/open/option/order/orderbook/v1/{}`

**Parameter**

Name  | Value  |  Required | Note
-------------- | -------------- | -------------- | --------
optionName | BTCUSD-26OCT22-15000-C | true | Option Name 


## Get Option Transaction History(SIGNED)

Get option transaction history

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": {
		"list": [
			{
				"id": 1584745240079241216,// ID
				"optionId": null,// Option ID
				"optionName":"BTCUSD-2JUN23-18000-C",// Option name
				"displayName":"BTC-2JUN23-18000-C",// Option display name
				"tradeSide": 1,// Trade side 1 BUY 2 SELL
				"tradeType": 1,// Trade type 1 LIMIT 2 MARKET
				"price": 951.00000000,// Price
				"volume": 2.00000000,// Trade volume
				"iv": 0.5606,// Implied Volatility
				"markPrice": 1419.5139928388217,// Mark price
				"indexPrice": 20247.0,// Index price
				"orderId": 1584744827800133632,// Order ID
				"tradeId": 1584745239911469056,// Trade ID
				"fee": 0.00190200,// Fees
				"time": 1666667683034,// Transaction time
				"closeType":null,
				"isTaker":0
			}
		],
		"pageTotal": 1 ,// Number of pages
        "total":1
	}
}
```


### HTTP Request

`GET https://api.coincall.com/open/option/trade/history/v1/{}`

**Parameter**

Name  | Value  |  Required | Note
-------------- | -------------- | -------------- | --------
pageSize | 10 | true | Quantity per page
page | 1 | true | Numbe of pages
startTime | 1000000 | true |  Start time of the history
endTime | 200000 | true | End time of the history

## Get Option Last Trade

Get option last trade

> Response:

```json
{
	"code": 0,// Status code
	"msg": "Success",// Message
	"i18nArgs": null,
	"data": [
		{
			"optionName": "BTCUSD-26OCT22-20000-P",// Option name
			"displayName":"BTC-6JUN23-24000-C",// Option display name
			"price": 10.3,// Trade price
			"volume": 1,// Trade volume
			"time": 1666757622819,// Trade time
			"tradeSide": 2// Trade side
		}
	]
}
```

### HTTP Request

`GET https://api.coincall.com/open/option/trade/lasttrade/v1/{}`

**Parameter**

Name  | Value  |  Required | Note
-------------- | -------------- | -------------- | --------
optionName | BTCUSD-6JUN23-24000-C | true | Option Name 