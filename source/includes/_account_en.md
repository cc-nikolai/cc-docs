# User Account Related

## Get User Info(SIGNED)

Get user information

> Response:

```json
{
    "code":0,
    "msg":"Success",
    "i18nArgs":null,
    "data":{
        "name":"xxxx",
        "email":"xxxx",
        "userId":123456
    }
}
```

**HTTP Request**

`GET https://api.coincall.com/open/user/info/v1`

**Parameter**

Null


## Get Account Summary(SIGNED)

Get account summary

> Response:

```json
{
	"code": 0,
	"msg": "Success",
	"i18nArgs": null,
	"data": {
		"totalBtcValue": 1450291.99007375, // Balance in BTC
		"totalDollarValue": 50014750313.273344637523471200000000, // Balance in USD
		"totalUsdtValue": 50000314222.5510097100000000, // Balance in USDT
		"accounts": [{
			"accountId": null, // Account ID
			"coin": "ETH", // Coin name
			"coinIconUrl": "https://file.coincall.com/statics/symbol/GETH.png",
			"coinDesc": "Ethereum",
			"coinView": "ETH",
			"equityAmount": "0", // Total assets value in account
			"availableBalance": "0", // Available balance
			"canWithdrawAmount": "0", // Maximum amount can be withdrawn
			"marginMode": 1, // Margin mode （1 SM 2 PM)
			"marginBalance": "0", // Margin balance
			"unrealizedAmount": "0", // Total unrealized P/L of the account
			"imAmount": "0", // Total initial margin of account
			"mmAmount": "0", // Total maintenance margin of the account
			"delta": null,
			"chainType": null,
			"btcValue": 0,
			"dollarValue": 0,
			"usdtValue": 0,
			"decimal": 18
		}, {
			"accountId": 698897965,
			"coin": "USDT",
			"coinIconUrl": "https://file.coincall.com/statics/symbol/USDT.png",
			"coinDesc": "Tether USD",
			"coinView": "USDT",
			"equityAmount": "49999934983.83391905",
			"availableBalance": "49999781762.68412424",
			"canWithdrawAmount": "49999781762.68412424",
			"marginMode": 1,
			"marginBalance": "49999783525.20670462",
			"unrealizedAmount": "49154.89968042",
			"imAmount": "1762.52258038",
			"mmAmount": "3.18161452",
			"delta": null,
			"chainType": null,
			"btcValue": 1450280.99000541,
			"dollarValue": 50014370965.0624515791081160,
			"usdtValue": 49999934983.83391905,
			"decimal": 6
		}}]
	}
}

```

**HTTP Request**

`GET https://api.coincall.com/open/account/summary/v1`

**Parameter**

Null

<!-- ## Switch Margin Mode -->

## Get Query API (SIGNED)

`GET /open/auth/user/query-api`

**Request Parameters:**

Headers:

| Key         | Value      | required | description             |
| ----------- | ---------- | -------- | ----------------------- |
| X-CC-APIKEY | aabcdadfse | TRUE     | apikey  <br>User apikey |

**Response Parameters**

| Name      | Type    | Value        | Note                                                                                                              |
| --------- | ------- | ------------ | ----------------------------------------------------------------------------------------------------------------- |
| userId    | integer | 123456       |                                                                                                                   |
| apiKey    | string  | asj198BDS981 |                                                                                                                   |
| readOnly  | integer | 0, 1         | 0:Read and Write. 1:Read only                                                                                     |
| isMaster  | boolean | true, false  |                                                                                                                   |
| parentUid | Long    | 123456789    | API，UID；API，0  <br>If it is a sub-account API, return the main account UID; if it is a main account API, return 0 |

> Response:

```JSON
{
    "code":0,
    "msg":"Success",
    "i18nArgs":null,
    "data":{
        "userId": 123456,
        "apiKey": "xxxxxxxx",
        "readOnly": 0, //0:Read and Write. 1:Read only
        "isMaster": true, //mainaccount:true. sub-account:false
        "parentUid": "0", //The main account uid. Returns "0" when the endpoint is called by main account
    }
}
```
# Get Equity Snapshot (SIGNED)

`GET https://api.coincall.com/open/account/equity_snapshot/v1`

- If no parameters are passed, all dates after the launch will be returned. If there is more data, the operation and maintenance will archive it.
- For assets, 0 does not return
- Add to the new liquidation

**Parameter:**

| Name | Type | Value         | Required | Note |
| ---- | ---- | ------------- | -------- | ---- |
| time | long | 1666771200000 | FALSE    |      |

> Response:

```JSON
{
  "code":0,
    "msg":"Success",
    "i18nArgs":null,
    "data": [
      {
        "date": "2024-12-23",
          {
            "coin": "USDT",
            "equityAmount": 1.12345678,
          }    
          {
            "coin": "BTC",
            "equityAmount": 1.12345678,
          }    
          {
            "coin": "ETH",
            "equityAmount": 1.12345678,
          }  
      },
      {
        "date": "2024-12-22",
        {
            "coin": "USDT",
            "equityAmount": 1.12345678,
          }    
          {
            "coin": "BTC",
            "equityAmount": 1.12345678,
          }    
          {
            "coin": "ETH",
            "equityAmount": 1.12345678,
          }  
      },
      {
        "date": "2024-12-21",
        {
            "coin": "USDT",
            "equityAmount": 1.12345678,
          }    
          {
            "coin": "BTC",
            "equityAmount": 1.12345678,
          }    
          {
            "coin": "ETH",
            "equityAmount": 1.12345678,
          }  
      },
    ],
    "records_total": 58
  }
}
```
