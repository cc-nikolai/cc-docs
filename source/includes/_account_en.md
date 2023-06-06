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

### HTTP Request

`GET https://api.coincall.com/open/user/info/v1`

**Parameter**

Null


## Get Account Summary(SIGNED)

Get account summary

> Response:

```json
{
    "code":0,// Status code
    "msg":"Success",// Message
    "i18nArgs":null,
    "data":{
        "accountId":123456,// Account ID
        "coin":"USD",
        "coinIconUrl":"xxxx",
        "coinDesc":"USD Stablecoins",
        "coinView":"USD",
        "equityAmount":100000,// Total assets value in account
        "availableBalance":99999.16966405,// Available balance
        "canWithdrawAmount":99999.16966405,// Maximum amount can be withdrawn
        "marginMode":1,// Margin mode （1 SM 2 PM)
        "marginBalance":100000,// Margin balance
        "unrealizedAmount":0,// Total unrealized P/L of the account
        "imAmount":0,// Total initial margin of account
        "mmAmount":0,// Total maintenance margin of the account
        "delta":null,
        "chainType":null,
        "btcValue":3.6848964,
        "dollarValue":100000,
        "decimal":8
    }
}

```

### HTTP Request

`GET https://api.coincall.com/open/account/summary/v1`

**Parameter**

Null

<!-- ## Switch Margin Mode -->
