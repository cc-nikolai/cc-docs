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
		"imAmount": "15647.08532640",  //initial margin amount
        "mmAmount": "10850.05133640", //maintenance margin amount
        "imRatio": "0.147982", //initial margin rate
        "mmRatio": "0.102614", //maintenance margin rate
        "equity": "99932.41659503000", //account equity
        "availableMargin": "90088.98159503", //aviliable margin amount
        "marginBalance": "105736.06692143", //margin balance amount
        "unrealizedPnL": "-43.65032640", //unrealized Profit and Loss
		"accounts": [{
			"accountId": null, // Account ID
			"coin": "ETH", // Coin name
			"coinIconUrl": "https://file.coincall.com/statics/symbol/GETH.png",
			"coinDesc": "Ethereum",
			"coinView": "ETH",
			"equityAmount": "0", // Total assets value in account
			"availableBalance": "0", // Available balance
			"cashBalanceAmount": 105736.06692143, //cash balance amount
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
			"cashBalanceAmount": 0,
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

`GET https://api.coincall.com/open/auth/user/query-api`

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

```json
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

## Deposit / Withdraw History API (SIGNED)  
### (not released) 
query deposit and withdrawal history


**HTTP Request**

`GET https://api.coincall.com/open/account/historyList/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
type | integer | -1,0,1 | false |  query type -1 all 0 deposit 1 withdrawal
page | integer | 1 | false | Page number, default is 1
pageSize | integer | 20 | false | Number of items per page, default is 20


> Response: 

```json
{
    "code": 0,
    "msg": null,
    "i18nArgs": null,
    "data": {
        "list": [
            {
        		"transactionRecordId": 2880637015540805600,      // transaction ID
        		"createTime": "2025-01-18T15:36:43.199+00:00",   //create time
        		"side": "deposit",   //deposit or withdraw
        		"coin": "SETH",      //currency
        		"amount": 0.5,       //amount
        		"serviceFee": 0,     //Deposit and withdrawal fee.
        		"address": "0x6595e62302e44b4c9db049e91fdb4b010c8b73bf",    //Deposit destination address.
        		"network": "Test SETH (ERC20)",   //network type 
        		"addressUrl": "https://sepolia.etherscan.io/address/\n0x6595e62302e44b4c9db049e91fdb4b010c8b73bf",   //chain adress url
        		"txId": "0x7c17c831db60ffa4cf3305859828e021fc9130fb95327c91896861e2422fd556",   //chain txId 
        		"txIdUrl": "https://sepolia.etherscan.io/tx/\n0x7c17c831db60ffa4cf3305859828e021fc9130fb95327c91896861e2422fd556",   //chain txId url
        		"status": "Completed",   //status includes: cancel,Processing,Cancelled,Completed,Failed
        		"confirmingThreshold": 64,   //Minimum confirmation count for the cryptocurrency.
        		"confirmedNum": 67,   //Confirmation count for the cryptocurrency
        		"type": "external"   // "external" refers to on-chain transactions; "internal" refers to Loop transactions.
            },
            {
                "transactionRecordId": 2905095341540290600,
                "createTime": "2025-03-27T03:11:39.045+00:00",
                "side": "withdraw",
                "coin": "USDT",
                "amount": 1200,
                "serviceFee": 2,
                "address": "0x18E03648Ab40A9DDFB8b6bD4A65C5317EbABdD9E",
                "network": "Tron (TRC20)",
                "addressUrl": "https://tronscan.org/#/address/0x18E03648Ab40A9DDFB8b6bD4A65C5317EbABdD9E",
                "txId": null,
                "txIdUrl": "https://tronscan.org/#/transaction/null",
                "status": "Cancelled",
                "confirmingThreshold": null,
                "confirmedNum": null,
                "type": null
            }
        ],
        "pageTotal": 0,
        "total": 0
    }
}

```



## Subaccount funds transfer API (SIGNED)  
### (not released) 
Transfer funds between subaccounts

**HTTP Request**

`GET https://api.coincall.com/open/user/subAccount/fund/transfer/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
fromUserId | integer | 1695796692726153 | true |  Sender user id for funds transfer (funds out)
toUserId | integer | 1 | 1695796692726100 | true |  Recipient user id for fund transfer (funds in)
amount | number | 20 | true |  Transfer amount
currency | String | 20 | true | Transfer currency


> Response: 

```json
{
    "code": 0,
    "msg": null,
    "i18nArgs": null,
    "data":  null
}

```
