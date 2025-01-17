## AUTH
For each api request you should use this headers:
* ApiPublic: {your_public_key}
* ApiPrivate: {your_public_key}
## Payin
```POST
https://api.nirvanapay.pro/create/in
```

Request:
```JSON
{
	"clientID":"4test",
	"amount":13000,
	"token":"Humo UZS",
	"currency":"UZS",
	"callbackUrl":"https://my.app/callback?id=39021"
}
```
Response:
```JSON
{
	"trackerID": "3de82b67cddc7ad270532479352c79c4691f7fe1c1f4b5c1299105a3b8df621a",
	"amountCrypto": 0.9378,
	"rate": 13458.92,
	"receiver": "9860190112540546",
	"status": "CREATED",
	"extra": {
		"bankName": "Humo UZS",
		"recipientName": "Ivan Ivanov"
	}
}
```
Response error:
```JSON
{
	"status": "ERROR",
	"reason": "Internal Server Error",
	"extra": {}
}
```

## Payout
```POST
https://api.nirvanapay.pro/create/out
```
_ATENTION!!! If you received not standard responce - contact us_
_You can safely cancel Payout transaction ONLY_
1) _if received status `ERROR`_
2) _when we confirm the cancellation in the chat_

Request:
```JSON
{
	"clientID": "5test",
	"amount": 30000,
	"token": "Humo UZS",
	"currency": "UZS",
	"receiver": "9860170111367463",
	"extra": {
		"bankName": "Humo UZS",
		"recipientName": "Ivan Ivanov"
	},
	"callbackUrl": "https://my.app/callback?id=39022"
}
```
Responce:
```JSON
{
	"status": "CREATED",
	"trackerID": "ea3c8b2799395d0a8e13a08fbd5a6aef3162f6143d703240d8c910ed95f6e8c9"
}
```
Responce error:
```JSON
{
	"status": "ERROR",
	"reason": "Транзакция не создана. Ошибка с проверкой на лимиты. Было отправлено [1000.000000], минимальный лимит по валюте [30000.000000]"
}
```

##  Status
```POST
https://api.nirvanapay.pro/transaction/status
```
PAYIN top up the client with the amount specified in the field amountFiatReceived
Request:
```JSON
{
	"clientID": "3test"
}
```
Responce:
```JSON
{
	"status": "ERROR",
	"type": "IN",
	"createTime": "2025-01-15T15:00:17.278878Z",
	"amountCrypto": 0.9466,
	"amountFiatOrdered": 13000,
	"amountFiatReceived": 0,
	"baseRate": 13333.31,
	"rate": 13733.31,
	"commission": 0.0284,
	"trackerID": "8a1479fa698bf27cec1ab5aa75966a81b5f70c6fa89549cf47d66d6317042a91",
	"clientID": "11test",
	"token": "Humo UZS",
	"currency": "UZS",
	"receiver": "9860060932532835"
}
```
Responce error:
```JSON
{
	"reason": "Transaction not found",
}
```

## Balance
```GET
https://api.nirvanapay.pro/client/balance
```

Responce:
```JSON
{
	"available": {
		"USDT": 4990.9846
	},
	"frozen": {
		"USDT": 0
	}
}
```

## Tokens
Country Uzbekistan:(currency="UZS")

	Humo UZS
	UZ Card
	HumoVisa
	HumoMastercard
	UzcardVisa
	UzcardMastercard

Country Azerbaijan:(currency="AZN")

	AZN
	Mpay
	LeoBank
	M10
	Kapital Bank
	ABB

Country Türkiye:(currency="TRY")

	Enpara
	Garanti
	TRY
	Ecom TRY
	Payfix
	iBan
	Ininal
	Ziraat Bank
	Kuveyt
	Papara

Country Kazakhstan:(currency="KZT")

	ForteBank
	Altyn Bank
	Halyk Bank

Country Tajikistan:(currency="TJS")

	Алиф Банк
	Спитамен Банк
	Душанбе Сити Банк 

Country Abkhazia:(currency="ARUB")

	Сбербанк Абхазии 
	А-мобаил