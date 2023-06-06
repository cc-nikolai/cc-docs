# Futures Endpoints

## Get Futures Symbol

Get futures symbol

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",// Message
	"i18nArgs": null,
	"data": [{
		"contractId": 1,// Contract ID
		"symbol": "BTCUSD",// Symbol
		"symbolName":"BTC/USD",// Symbol name
		"displayName":"BTC-PERP",// Symbol display name
		"baseToken":"BTC",
		"quoteToken":"USD",
		"price": 25614.7,// Price
		"changeRate": -0.003,// Change in percentage
		"changeVolume": 0,// Change in value
		"changePrice":-78.2,
		"markPrice": 25661.25861712,// Mark price
		"indexPrice": 25754.025,// Index Price
		"price24hHigh": 27065.7,// Highest price in 24hrs
		"price24hLow": 18000,// Lowest price in 24hrs
		"volumeUsd24h": 3846213875.0958,// USD volume in 24hrs
		"volume24h": 147370.135,// Volume in 24hrs
		"ts": 20201116024818,// Timestamp
		"price24hOpen":25692.9,// Open price on UTC 00:00:00
		"icon":"https://file.coincall.com/statics/symbol/BTC.png",
		"hasOption":true,
		"sortIdx":null
	}]
}
```


### HTTP Request

`GET https://api.coincall.com/open/futures/market/symbol/v1`


**Parameter**

Null


## Get Futures Position(SIGNED)

Get futures positions

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data":
    {
      "id": 1584467417583730700,// ID
      "positionId": 1584467417583730700,// Position ID
      "updateTime": 1666602220413,// Update time
      "userId": 1536933707941347300,// User ID
      "value": 176.7825,// Value
      "volume": 0.009,// Volume
      "initMargin": 35.3565,// Initial margin
      "maintMargin": 1.767825,// Maintnance margin
      "avgPrice": 19642.5,// Average price
      "markPrice": 18900.38311437,// Mark price
      "elp": null,// Estimated liquidation price
      "pnl": 0,// Realized PnL
      "roi": -0.03778118,// ROI
      "rspl": 0,//
      "unpl": -6.67905197067,// Unrealized Pnl
      "symbol": "BTCUSD",//symbol
      "tradeSide": 1,// Trade side 1 BUY  2 SELL
      "tradeType": null,// Trade type 1 LIMIT 2 MARKET  
      "lockVolume": 0,// Lock volume
      "leverage": 5,// Leverage
      "delta": 0.009// Position delta
    }
}
```


### HTTP Request

`GET https://api.coincall.com/open/futures/position/get/v1`

**Parameter**

Null

## Place a Futures Order(SIGNED)

 Place a futures order

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": null
}
```


### HTTP Request

`POST https://api.coincall.com/open/futures/order/create/v1`

**Parameter**

Name  | Value  | Required | Note
-------------- | -------------- | -------------- | -------
symbol | BTCUSD | true | Futures Symbol 
price | 19000 | false | Price required for limit orders
volume| 0.5 | true | Quantity of the order 
tradeSide | 1 | true | Trader side：1 buy, 2 sell
tradeType | 1 | true | Trade type：1 limit, 2 market
isClose | 1 | true | Clarify if the order is a close order 




## Cancel a Futures Order(SIGNED)

Cancel a futures order

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": null
}
```


### HTTP Request

`GET https://api.coincall.com/open/futures/order/cancel/v1/{orderId}`

**Parameter**

Name  | Value  | Required | Note
-------------- | -------------- | -------------- | --------------
orderId | 111 | true | query string


## Get Futures Open Orders(SIGNED)

Get open orders 

> Response:

```json
{
	"code": 0, // Status code
	"msg": "success", //Message
	"i18nArgs": null,
	"data":
		{
			"id": 1584848662192898000,// ID
			"orderId": 1584848661807022000,// Order ID
			"symbol": "BTCUSD",// Symbol
			"volume": 0.001,// Volume
			"remainVolume": 0.001,// Unfilled volume
			"fillVolume": 0,// Filled volume
			"price": 19000,// Price
			"avgPrice": 0,// Average price
			"initMargin": 6.333333,// Initial margin
			"tradeSide": 1,// Trade side  1 BUY 2 SELL
			"tradeType": 1,// Trade type 1 LIMIT 2 MARKET
			"createTime": 1666692340695,// Time of the order created
			"closeType": 1,//
			"leverage": 3 // Leverage
		}
}
```

### HTTP Request

`GET https://api.coincall.com/open/futures/order/pending/v1`

**Parameter**

Null

## Get Futures Order History(SIGNED)

Get futures order history

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": {
		"list": [{
			"orderId": 1584837328353017856,// Order ID
			"symbol": "BTCUSD",// Symbol
			"volume": 0.0010000000000000,// Volume
			"fillVolume": 0E-16,// Filled volume
			"price": 18999.0000000000000000,// Price
			"avgPrice": 0E-8,// Average price
			"fee": 0E-16,// Fees
			"pnl": 0E-16,// Realized PnL
			"tradeSide": 2,// Trade side 1 BUY 2 SELL
			"tradeType": 1,// Trade type 1 LIMIT 2 MARKET
			"createTime": 1666689638588,// Time of the order created
			"state": 3,// Order state
			"closeType": 1,//
			"leverage": 3 // Leverage
		}],
		"pageTotal": 2 // Number of pages
	}
}
```


### HTTP Request

`GET https://api.coincall.com/open/futures/order/history/v1/{}`

**Parameter**

Name  | Value  | Required | Note
-------------- | -------------- | -------------- | --------
pageSize | 10 | true | Quantity per page
page | 1 | true | Numbe of pages
startTime | 1000000 | true |  Start time of the history
endTime | 200000 | true | End time of the history

## Get Futures Order Book 

 Get futures order book

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": {
		"symbol": "BTCUSD",//symbol
		"bids": [{
			"volume": 0.001,// Volume
			"price": "18801"// Volume
		}],
		"asks": [{
			"volume": 0.992,// Volume
			"price": "18898"// Volume
		}]
	}
}
```


### HTTP Request

`GET https://api.coincall.com/open/futures/order/orderbook/v1/{}`

**Parameter**

Name  | Value  | Required | Note
-------------- | -------------- | -------------- | --------
symbol | BTCUSD | true | Symbol name


## Get Futures Transaction History(SIGNED)

Get futrues transaction history

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": {
		"list": [{
			"id": 1574775822713806849,// ID
			"contractId": null,// Contract ID
			"symbol": "ETHUSD",//symbol
			"tradeSide": 1,//Trade side 1 BUY 2 SELL
			"tradeType": 1,//Trade type 1 LIMIT 2 MARKET
			"price": 1389.00000000,// Price
			"volume": 1.00000000,// Volume
			"markPrice": null,// Mark price
			"indexPrice": 1389.26000000,// Index Price
			"orderId": 1574775820017352705,// Order ID
			"tradeId": 1574775820805869568,// Trade ID
			"fee": 0.13890000,// Fees
			"time": 1664290788701,// Time of the transaction
			"closeType": null,
			"leverage": 5 // Leverage
		}],
		"pageTotal": 1 // Number of pages
	}
}
```


### HTTP Request

`GET https://api.coincall.com/open/futures/trade/history/v1/{}`

**Parameter**

Name  | Value  | Required | 说明
-------------- | -------------- | -------------- | --------
pageSize | 10 | true | Quantity per page
page | 1 | true | Numbe of pages
startTime | 1000000 | true |  Start time of the history
endTime | 200000 | true | End time of the history

## Get Futures Last Trade

Get futures last trade

> Response:

```json
{
	"code": 0,// Status code
	"msg": "success",//Message
	"i18nArgs": null,
	"data": [{
		"symbol": "BTCUSD",//symbol
		"price": 18898,// Price
		"volume": 0.001,// Volume
		"time": 1666754916559,// Time of the transaction
		"tradeSide": 1 // Trade side 1 BUY 2 SELL
	}]
}
```


### HTTP Request

`GET https://api.coincall.com/open/futures/trade/lasttrade/v1/{}`

**Parameter**

Name  | Value  | Required | Note
-------------- | -------------- | -------------- | --------
symbol | BTCUSD | true | Symbol name

## Set Futures Leverage

 Set futures leverage

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",//Message
  "i18nArgs": null,
  "data": null
}
```


### HTTP Request

`POST https://api.coincall.com/open/futures/leverage/set/v1`

**Parameter**

Name  | Value  | Required 
-------------- | -------------- | --------------
symbol | BTCUSD | true | Symbol name
leverage | 10 | true | leverage for this symbol



## Get futures leverage

Get current futrues leverage

> Response:

```json
{
  "code": 0,// Status code
  "msg": "success",
  "i18nArgs": null,
  "data": {
    "userId": 123,// User ID
    "symbol": "BTCUSD",// Symbol
    "currentLeverage": 5 // Current leverage
  }
}
```


### HTTP Request

`GET https://api.coincall.com/open/futures/leverage/current/v1`

**Parameter**

Null
