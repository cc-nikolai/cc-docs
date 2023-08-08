# Referrals
## Referrals Record(SIGNED)

Get referrals record

> Response:

```json
{
    "code": 0,
    "msg": null,
    "data": {
        "list": [
            {
                "inviteeUserId": 9804700, // User ID of invitee
                "level": 0, // 0 user, 1 sub-agent
                "commissions": 0, // Commission earned from this user himself and his invitees
                "verification": 0, // 0 false, 1 true
                "deposit": 0, // 0 false, 1 true
                "futures": 1, // 0 false, 1 true
                "options": 0, // 0 false, 1 true
                "regTime": 1675845379145 // Time of registration (ms)
            }
        ],
        "pageTotal": 2,
        "total": 14
    }
}
```


**HTTP Request**

`GET https://api.coincall.com/open/referral/sub/v1`

**Parameter**

Name | Type | Value | Required | Note
---- | ---- | ----- | -------- | ----
subAgentId |integer | 9905700 | false |
page | integer | 1,2,3 | false |

**Notice**

`subAgentId` UID of the sub-agent; if it is not passed, it will return all invitees, and if it is passed, it will return the invitees of the user and the user itself