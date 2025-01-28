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
Responce can be without trackerID:
```JSON
{
	"status": "CREATED",
	"trackerID": ""
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
Possible statuses:
```JSON
["ERROR","CREATED","SUCCESS"]
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
Responce success:
```JSON
{
	"status": "SUCCESS",
	"type": "IN",
	"createTime": "2025-01-19T17:33:09.952418Z",
	"amountCrypto": 2.164,
	"amountFiatOrdered": 30000,
	"amountFiatReceived": 30000,
	"baseRate": 13459.28,
	"rate": 13863.06,
	"commission": 0.0649,
	"trackerID": "c7a2019fd0f4f511f698072911f55757861b4a11f9c96a476ff96b0ae76f410c",
	"clientID": "9c5041dd5052c9fec797d90fa3921bf808641fb1049eeceb95d60a517fc6af92",
	"token": "UZ Card",
	"currency": "UZS",
	"receiver": "5614682611279383"
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

 Country Russia:(currency="RUB")

	Тинькофф
	Сбербанк
	Райффайзен
	Открытие
	QIWI
	Рубль
	Альфабанк
	Наличные Рубли
	Совкомбанк
	МКБ
	ВТБ
	МТС-Банк
	Россельхозбанк
	Газпромбанк
	Почта банк
	Пополнение телефона
	Юмани
	СБП
	КБ СТРОЙЛЕСБАНК
	Хайс Банк
	КБ Новый век
	Точка ФК Открытие
	Банк Интеза
	КБ Пойдём!
	Русьуниверсалбанк
	Таврический Банк
	КБ Модульбанк
	АКБ Алеф-Банк
	КБ АРЕСБАНК
	Вайлдберриз Банк
	Банк ПСКБ
	ПНКО ЭЛПЛАТ
	МОБИ.Деньги
	НКО ЮМани
	КБ РостФинанс
	Экспобанк
	КБ РУСНАРБАНК |
	НИКО-БАНК
	Банк ВБРР
	АКИБАНК
	Банк Развитие-Столица
	АКБ МЕЖДУНАРОДНЫЙ ФИНАНСОВЫЙ КЛУБ
	Кузнецкбизнесбанк
	Кредит Европа Банк \(Россия\)
	АКБ СЛАВИЯ
	Индустриальный Сберегательный Банк
	Банк Национальный стандарт
	КБ Кубань Кредит
	АК БАРС БАНК
	Томскпромстройбанк
	Дальневосточный банк
	Бланк банк
	БАНК ОРЕНБУРГ
	Ставропольпромстройбанк
	Банк ИТУРУП
	КБ ВНЕШФИНБАНК
	ЮГ-Инвестбанк
	РЕАЛИСТ БАНК
	Банк АЛЕКСАНДРОВСКИЙ
	ФИНСТАР БАНК
	Азиатско-Тихоокеанский Банк
	КБ УБРиР
	ЧЕЛЯБИНВЕСТБАНК
	КБ Солидарность
	КБ СИНКО-БАНК
	КБ ЛОКО-Банк
	АКБ ТЕНДЕР-БАНК
	АКБ Трансстройбанк
	Банк Заречье
	Северный Народный Банк
	ВУЗ-банк
	СОЦИУМ-БАНК
	Банк БКФ
	КБ Гарант-Инвест
	Банк МБА-МОСКВА
	Газтрансбанк
	АКБ Держава
	банк Раунд
	Земский банк
	НС Банк
	МБ Банк
	АКБ Ланта-Банк
	ФФИН Банк
	Углеметбанк
	ИК Банк
	КБ Крокус-Банк
	СИБСОЦБАНК
	Банк Агророс
	УКБ Белгородсоцбанк
	Драйв Клик Банк
	УРАЛПРОМБАНК
	Банк Объединенный капитал
	Банк ЗЕНИТ
	КОШЕЛЕВ-БАНК
	Банк Аверс
	НОКССБАНК
	Эс-Би-Ай Банк
	МС Банк Рус
	ИШБАНК
	Промсвязьбанк
	Хоум кредит
	Банк ИПБ
	Росбанк
	АКБ Абсолют Банк
	БыстроБанк
	Нацинвестпромбанк
	Датабанк
	КБ ЭНЕРГОТРАНСБАНК
	АКБ Форштадт
	ВЛАДБИЗНЕСБАНК
	Первый Инвестиционный Банк
	Банк Йошкар-Ола
	КБ Долинск
	Банк ФИНАМ
	СДМ-Банк
	Банк Точка
	Банк Кремлевский
	Банк Венец
	Кредит Урал Банк
	Роял Кредит Банк
	Деньги.Мэйл.Ру
	УКБ Новобанк
	Хакасский муниципальный банк
	Промтрансбанк
	Тимер Банк
	Банк Акцепт
	МОРСКОЙ БАНК
	Инбанк
	Юникредитбанк
	банк Элита
	КБ АГРОПРОМКРЕДИТ
	АИКБ Енисейский объединенный банк
	ABC Code
	Озонбанк
	Уралсиб
	Межбанк
	АКБ АВАНГАРД
	ОТП Банк
	Банк Синара
	Газэнергобанк
	РНКБ Банк
	АБ РОССИЯ
	ДБО Фактура
	КБ Хлынов
	Банк ДОМ.РФ
	Банк Левобережный
	АКБ Алмазэргиэнбанк
	АКБ Энергобанк
	Банк РЕСО Кредит
	Банк Санкт-Петербург
	АКБ НОВИКОМБАНК
	РосДорБанк
	СКБ Приморья Примсоцбанк
	Банк Саратов
	Тольяттихимбанк
	ТКБ БАНК
	НБД-Банк
	БАНК СНГБ
	Банк Русский Стандарт
	ГЕНБАНК
	Банк Екатеринбург
	Авто Финанс Банк
	ЧЕЛИНДБАНК
	Автоградбанк
	АКБ Солид
	КБ Урал ФД
	ТАТСОЦБАНК
	Норвик Банк
	Джей энд Ти Банк
	МЕТКОМБАНК
	КБЭР Банк Казани
	КБ Центр-инвест
	АКБ ФОРА-БАНК
	МП Банк
	ГОРБАНК
	МОСКОМБАНК
	КБ Ситибанк
	Автоторгбанк
	БАНК УРАЛСИБ
	Ингосстрах Банк
	АКБ Приморье
	КБ Ренессанс Кредит
	Севергазбанк
	АКБ НРБанк
	КБ Москоммерцбанк
	Кубаньторгбанк
	НК Банк
	Тойота Банк
	ББР Банк
	Банк Финсервис
	КБ ЮНИСТРИМ
	БКС Банк
	АКБ ЕВРОФИНАНС МОСНАРБАНК
	Яндекс Банк
	Банк БЖФ
	БАНК МОСКВА-СИТИ
	ГУТА-БАНК
	Прио-Внешторгбанк
	Уралфинанс
	ЦентроКредит
	Снежинский
	Металлинвестбанк
	ПроБанк
	Цифра банк
	Первый Дортрансбанк
	ЦМРБанк
	Плайт
	Банк Оранжевый
	ИКБР ЯРИНТЕРБАНК
	Вайлдберриз
	Номер счета
	Т-Банк
	МТС Деньги
	ТрансМежбанк
	ТрансСБП

 	
