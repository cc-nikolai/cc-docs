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

## Get Deposit and Withdrawal History API (SIGNED)
Query deposit and withdrawal history


**HTTP Request**

`GET https://api.coincall.com/open/account/historyList/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
type | integer | -1,0,1 | false |  query type -1 all 0 deposit 1 withdrawal
startTime | number| 1686308840388 | false| Start time of the history
endTime | number | 1686308840388 | false | End time of the history
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
Transfer funds between subaccounts

**HTTP Request**

`POST https://api.coincall.com/open/user/subAccount/fund/transfer/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
fromUserId | integer | 1695796692726153 | true |  Sender user id for funds transfer (funds out)
toUserId | integer | 1695796692726100 | true |  Recipient user id for fund transfer (funds in)
amount | number | 20 | true |  Transfer amount
currency | String | ETH,USDT | true | Transfer currency


> Rquest: 

```json
curl 
-X POST "https://beta.seizeyouralpha.com/open/user/subAccount/fund/transfer/v1"
-H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU=" 
-H "sign: D6D850F24E488EFF8B859E748370345437757DDEFBAF921613D06B0D7BA220F9" 
-H "ts: 1744629390441" 
-H "X-REQ-TS-DIFF: 5000" 
-H "content-type: application/x-www-form-urlencoded;charset=UTF-8"
--data-raw "fromUserId=1695796692726153&toUserId=1695796692779320&currency=USDT&amount=111"

```


> Response: 

```json
{
    "code": 0,
    "msg": null,
    "i18nArgs": null,
    "data":  null
}

```


## Deposit Address  (SIGNED) 
Get Deposit Address

**HTTP Request**

`GET https://api.coincall.com/open/account/getDepositAddress/v1 `

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
coin | String | ETH | true | Type of coin for deposit
chainType | String | ETH | true |  Deposit chain type



> Rquest: 

```json
curl -X GET 
-H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU=" 
-H "sign: 47A64BBFE773FBF36FBDBEE4E695A207240B17721E72BECAB6FB6AA10E590222"
-H "ts: 1748593250583"
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " 
"https://beta.seizeyouralpha.com/open/account/getDepositAddress/v1?coin=ETH&chainType=ETH"

```


> Response: 

```json
{
  "code": 0,
  "msg": "Success",
  "i18nArgs": null,
  "data": {
    "address": "0x992a0737f23f3061e297620f56252c4dbcdf411",
    "coin": "ETH",
    "chainType": "ETH",
    "memo": null
  }
}

```


## Subaccount List (SIGNED) 
Get Subaccount info List 

**HTTP Request**

`GET https://api.coincall.com/open/user/subAccount/list/v1`



> Rquest: 

```json

curl -X GET 
-H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU=" 
-H "sign: A161477EB6C8F2D2CF490D792511D3084D23A0844752E6C01E8673532D30538D" 
-H "ts: 1748598187413" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " 
"https://beta.seizeyouralpha.com/open/user/subAccount/list/v1"

```


> Response: 

```json
{
  "code": 0,
  "msg": null,
  "i18nArgs": null,
  "data": {
    "subAccounts": [
      {
        "name": "",
        "email": "zzztest@gmail.com",
        "userId": 1695796692726153,
        "subAccountType": 1,
        "allowLogin": true,
        "equityAmount": 99544030.18015793,
        "availableBalance": 99524446.63267758,
        "canTransferSmAmount": 99524446.63267758,
        "canWithdrawAmount": 99524446.63267758,
        "marginMode": 2,
        "marginBalance": 99544030.18015793,
        "unrealizedAmount": -49193.5,
        "imAmount": 19582.45148035,
        "mmAmount": 16318.70956696,
        "trailAmount": 0
      },
      {
        "name": "hello",
        "email": "zzztest@163.com",
        "userId": 1695796692779320,
        "subAccountType": 2,
        "allowLogin": true,
        "equityAmount": 222.00002098,
        "availableBalance": 222.00002098,
        "canTransferSmAmount": 222.00002098,
        "canWithdrawAmount": 222.00002098,
        "marginMode": 1,
        "marginBalance": 222.00002098,
        "unrealizedAmount": 0,
        "imAmount": 0,
        "mmAmount": 0,
        "trailAmount": 0
      }
    ]
  }
}

```


## Lending Detail (SIGNED) 

Lending Detail

**HTTP Request**

`GET https://api.coincall.com/open/futures/lending/detail/v1 `





> Rquest: 

```json
curl -X GET 
-H "X-CC-APIKEY: yc9GYhc/tBBNq4VJGpCyDPvxM6iaUrjphQnoCRnv0TU=" 
-H "sign: 718CA489C948A432999824B5B825D34B78765DE21D8E43C80A63010A6A156B2B" 
-H "ts: 1748600547440" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " 
"https://beta.seizeyouralpha.com/open/futures/lending/detail/v1"

```


> Response: 

```json
{
  "code": 0,
  "msg": "Success",
  "i18nArgs": null,
  "data": {
    "amount": "100012761.00835726",   //Current lent amount or debt amount
    "currency": "USDT",               //Currency type
     "status": 1,                     //1-Earning 2-Loaning
    "annualRate": "0.0570",           //Annual interest rate: a return value of 0.0570 indicates 5.70%
    "lastDayEarnings": "0.13660546",  //Earnings sum for yesterday
    "totalEarnings": "1.44159264"     //Total accumulated earnings
  }
}

```


## SubAccount Transfer Records (SIGNED)
Get SubAccount Transfer Records 

**HTTP Request**

`GET https://api.coincall.com/open/user/subAccount/transfer/records/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
page | Number | 1 | false | Number of query records default is 1
pageSize | Number | 20 | false |  Number of records per page default is 20



> Rquest: 

```json
curl -X GET 
-H "X-CC-APIKEY: I+VmVk6wW84DiXiBkabjFo9OIOCXs3nzsVXtIbI/yRk=" 
-H "sign: D69C271BF12C8288D5C4FA7C532E929F07D931E0DF479C4E619E478A4EEA936F" 
-H "ts: 1749033885633" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " 
"https://beta.seizeyouralpha.com/open/user/subAccount/transfer/records/v1?page=1&pageSize=20"
```


> Response: 

```json
{
  "code": 0,
  "msg": null,
  "i18nArgs": null,
  "data": {
    "list": [
      {
        "id": 1694,
        "mainUserId": 1695796692726153,       //Main account UserId
        "sourceUserId": 1695796692726153,     //Transfer-out user ID
        "toUserId": 1695796692779320,         //Transfer-in user ID
        "sourceUserType": 1,                  //Transfer-out user type {1: Main account, 2: Sub-account}
        "toUserType": 2,                      //Transfer-out user type {1: Main account, 2: Sub-account}
        "sourceUserName": null,               // Transfer-out username
        "toUserName": "hello",                // Transfer-in username
        "amount": 20,                         // Transfer amount
        "token": "USDT",                      //Currency (coin)
        "createTime": 1749006859150
      },
      {
        "id": 1693,
        "mainUserId": 1695796692726153,
        "sourceUserId": 1695796692726153,
        "toUserId": 1695796692779320,
        "sourceUserType": 1,
        "toUserType": 2,
        "sourceUserName": null,
        "toUserName": "hello",
        "amount": 20,
        "token": "USDT",
        "createTime": 1749005491786
      }
    ],
    "pageTotal": 1,
    "total": 4
  }
}

```


## Get DepositAddress List(SIGNED) 
Get Deposit Address List

**HTTP Request**

`GET https://api.coincall.com/open/account/getDepositAddressList/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
coin | String | ETH | false | Type of coin for deposit
chainType | String | ETH | false |  Deposit chain type

**Parameter description**  

* coin=null, chainType=null: Get all coin and chain address information for the user.

* coin=USDT, chainType=null: Get all chain addresses for the specified coin (e.g. USDT).

* coin=USDT, chainType=ETH: Get the the specified chain (e.g. ETH) address for the coin (e.g.USDT).

* coin=null, chainType=ETH: Return the addresses of all coins on the specified chain(e.g. ETH).
  

> Rquest: 

```json
curl -X GET 
-H "X-CC-APIKEY: gPAprrmTmwU/SEnwd23GE/SeSox7YSHu6VxHqT8eNvA=" 
-H "sign: 759340BCA23728724B00098FF77083BE62AD1F62E0924FBBB1E8B94F16D44BB8" 
-H "ts: 1750320144430" 
-H "X-REQ-TS-DIFF: 5000" 
-H "Content-Type: " "https://beta.seizeyouralpha.com/open/account/getDepositAddressList/v1?chainType=ETH&coin=USDT"

```


> Response: 

```json
{
  "code": 0,
  "msg": "Success",
  "i18nArgs": null,
  "data": [
    {
      "address": "0x2eaf68a26900f1f21c51423150820a36ac5d164f",
      "coin": "USDT",
      "chainType": "BSC",
      "memo": null
    },
    {
      "address": "TDWiDUUUafKDT9cavPrmv8CK7VagupS2XA",
      "coin": "USDT",
      "chainType": "TRON",
      "memo": null
    }
  ]
}

```