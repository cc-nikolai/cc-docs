# Error Codes


The Coincall API uses the following error codes:


Codes | Description
---------- | -------
0|Success
500|Internal servererror
2015|User does not exist.
2016|Public key not exist
2017|Private key not exist
4002|Token expired.
4003|Token auth fail.
4004|Token kicke out.
4005|Duplicate request.
4006|This country or region is not supported
7001|No Permission.
10000|Try again later
10001|This operation is not allowed
10002|Result api system error
10003|Result api resquest illegal
10004|Parameter illegal
10005|Parameter error
10006|Sign illegal
10007|Token is error
10008|IP illegal
10009|Request method not support
10010|Param illegal
10101|Result header build error
10102|Query exception
10103|System inner error
10104|Params is null
10105|Params is blank
10106|Param long is blank
10107|Param integer is blank
10108|Params type error
10500|Incorrect or expired email verification code.
10501|Incorrect 2FA code.
10502|Please enter email verification code.
10503|Please enter 2FA  code.
10504|You are not able to withdraw funds because of the abnormal status of this account.
10505|Invalid email address.
10506|Please enter your password
10507|Must be at least 8 characters .
10508|Invalid email address.
10509|Please enter your password
10510|Must be at least 8 characters .
10511|Must not exceed 32 characters.
10512|Must contain at least one number (0-9).
10513|Must contain at least one special character (!@#$%^&*).
10514|The passwords do not match.
10515|Please enter correct referral code.
10516|Please select a country or region.
10517|Please agree to the Terms of Service .
10518|Incorrect or expired email verification code.
10519|Account blocked
10520|Invalid account or password, 5-n attempts remaining.
10521|Your account has been restricted to log in.
10522|Please enter the email verification code
10523|Please enter the 2FA code
10524|Incorrect 2FA code.
10525|Position the piece in its slot
10526|Please enter 2FA code
10527|Incorrect the 2FA code.
10528|Incorrect password.
10529|Insufficient available balance.
10530|Please enter price
10531|Order price is higher than the maximum limit {0}.
10532|Order price is lower than the minimum limit {0}.
10533|Please enter amount
10534|Order size exceeds the maximum limit per order.
10535|The number of orders exceeds the maximum limit.
10536|Insufficient open positions.
10537|Order cancellation failed.
10538|Order IV is higher than the maximum limit 500%.
10539|Order IV is lower than the minimum limit 50%.
10540|Order has expired.
10541|The number of stop orders exceeds the maximum limit.
10542|Please enter stop price
10543|Please enable the 2FA code .
10544|Only 10 APIKeys can be created per account.
10545|Must not exceed 128 characters.
10546|Please enter a name.
10547|This name is already used.
10548|Each APIKey can bind up to 20 IP addresses.
10549|Invalid IP address.
10550|Please enter email verification code.
10551|The IP address is not in whitelist.
10552|Operation failed.
10553|The server is under maintenance, please try again later.
10554|You are not authorized to execute this request.
10555|API frozen
10556|APIKey does not match current environment.
10557|Timestamp request expired.
10560|Invalid CC-ACCESS-KEY.
10561|Invalid CC-ACCESS-TIMESTAMP.
10562|Invalid signature.
10563|Invalid authorization.
10564|Invalid request method.
10565|Endpoint request timeout
10566|API is offline or unavailable.
10567|Invalid content_type.
10568|Account does not exist.
10569|User ID cannot be empty.
10570|Parameter {0} cannot be empty.
10571|Parameter {0} does not match parameter {1}.
10572|Parameter {0} count exceeds the limit
10573|Parameter {0} error.
10574|Instrument ID does not exist.
10575|Either client order ID or order ID is required.
10576|Duplicated order ID.
10577|Duplicated client order ID.
10578|Token does not exist.
10579|Index does not exist.
10580|Instrument ID does not match instrument type.
10581|Position does not exist.
10582|Order timed out, please try again later.
10583|Cancellation timed out, please try again later.
10584|Order does not exist.
10585|Either order status or order ID is required.
10586|Channel subscription failed.
10587|Login failed.
10588|Please log in.
10589|Invalid request.
10590|Invalid args.
10591|Invalid url path.
10592|The {0} does not exist.
10593|Invalid op {0}
10594|Wrong passphrase
10595|Token subscription amount exceeds the limit
10596|Internal system error.
10597|Maximum receive of friends is XX%.
10598|The number of referral links exceeds the maximum limit.
10599|Please enter your name/date of birth/address
10600|Name contains numbers or symbols.
10601|Please select the type of address proof.
10602|Please upload the file
10603|File is too large, upload failed.
10604|The format of this file is not supported.
10605|Operation is too frequent.
10606|The number of exports this month exceeds the maximum limit.
10607|File not exists
10608|File expired
10609|You are not able to trade temporarily because the contract is abnormal.
10619|reject.order,Please check if the countdown setting needs to be reset. https://docs.coincall.com/#public-endpoints-reset-countdown-settings
20000|Coin not exist
20001|Account not found
20002|Coin not support
20003|User not found
20004|Please enable the 2FA code.
20005|Please select withdrawal coin.
20006|Please select withdrawal network.
20007|Please enter withdrawal address.
20008|Withdrawal network does not match the withdrawal address.
20009|Please enter an amount.
20010|Insufficient withdrawable balance.
20011|Exceed the 24 hours limit of withdrawal.
20012|Minimum withdrawal amount is 20 USDC.
20013|You are not able to withdraw funds within 24 hours after changing the password.
20014|Send code fail
20015|User not exist
20016|Sub user not allowed withdraw
20018|User withdraw restricted
20020|Not found withdraw record
20021|Not your withdraw record
20022|Not supported cancel, now is processing or completed
20023|not supported cancel, now is processing
20024|Account create fail
20025|Account update fail
20027|Target mode equals origin mode
20028|Option pending order exsist
20029|Option hold position exsist
20030|Future pending order exsist
20031|Future hold position exsist
20032|You need to transfer remainning funds to main account or other sub accounts
20033|Send code fail
20034|Start time and end time range exceeds three months
30000|User illegal
30001|Token illegal
30002|Check fail
30003|Google verification code is wrong
30004|Verification code is wrong
40001|User is freezed
40002|User over login max times
40003|Operate code timeout
40004|Token  error
40005|Too many failed attempts, and your account has been locked
40006|Error fund transfer type, transfer sub account's parent user wrong
40007|Error fund transfer type, transfer to user must be sub account
40008|Transfer trade type is invalid
40009|Transfer amount exceeds can withdraw balance amount
40010|Error fund transfer type, transfer from user must be sub account
40011|Sub account  size limit
40012|User name already used
40013|Email already used
40014|Sub account id error
40015|Referral not found
40016|Invite commission rate add invitee commission rate not equals referral total commission rate
40017|Company info is exist
40018|Age less than 18
40019|Company info not exist
40020|Jumio workflow not exist error
40021|Age format is error
40022|Kyc user status error
40023|Kyc user check error
40024|Upgrade error
40025|Check rate error
40026|Get temp url error
40027|Two grade auth error
40028|One grade step1 save error
40029|One grade save error
40030|Jumio user reference change
40031|Kyc processing
40032|Jumio status not exist
40033|Jumio status enum is not exist
40034|Option not exist
40035|Price illegal
40036|Volume illegal
40037|IM more than 100%
40038|You are not able to adjust leverage due to existing open positions or pending orders in the account.
40039|The price exceeds the maximum limit {0}
40040|File size limit
40041|Upload file frequently
40042|File type is unknow
40043|File type is error

