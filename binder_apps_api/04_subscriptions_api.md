# 📘 Binder API SubscriptionController Documentation

## Module Base Path
`/api/v1/subscriptions/{method}`


## 'getActiveSubscriptions' (default)
### Доступ: `user`

**GET** `/api/v1/subscriptions/` или `/api/v1/subscriptions/getActiveSubscriptions`

### Описание:
Получить все действующие подписки.

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Subscriptions received",
	"data": [
		{
			"id": 4,
			"transaction_id": 388473,
			"user_id": 42,
			"tariff_id": 3,
			"entity": "vendor",
			"entity_uuid": "uuid-2",
			"dt_from": "2025-07-24 00:00:00",
			"dt_to": "2026-08-24 00:00:00"
		},
		{
			"id": 8,
			"transaction_id": 388493,
			"user_id": 42,
			"tariff_id": 3,
			"entity": "vendor",
			"entity_uuid": "uuid-2",
			"dt_from": "2025-08-24 00:00:00",
			"dt_to": "2026-09-24 00:00:00"
		}
	]
}
```
В `data` - массив активных подписок, где:\
"transaction_id" - id транзакции в be-pay, который был передан при создании подписки\
"entity" - на какую сущность подписка (пока только `vendor`)\
"entity_uuid" - uuid сущности (в данном случае uuid вендора, то есть аккаунта touchapi или crm)\
"dt_from" - дата, с которой подписка действует
"dt_to" - дата, до которой подписка действует

> Если у пользователя оплачено уже несколько периодов и они еще не истекли, будут выведены все. В том числе и будущие. Это будут одинаковые подписки, но с разным `transaction_id`. Предполагается, что в рамках одной транзакции пользователь не может приобрести сразу несоколько одинаковых подписок, например, 3 по 1 месяцу. Он должен выбрать именно один тариф нужного вида и по нужному аккаунту (вендору), т.е. с периодом действия - 3 месяца, если такой есть.


## 'createSubscriptions`
### Доступ: `user`

**POST** `/api/v1/subscriptions/createSubscriptions`

### Описание:
Создать подписки. Хук необходимо кинуть при приобретении пользователем подписок на фронте.

### Тело запроса:
```json
{
	"transaction_id": 388493,
	"subscriptions": [
			{
			"tariff_id": 3,
			"entity": "vendor",
			"entity_uuid": "uuid-1344564-dffhfh9as"
			},
			{
			"tariff_id": 4,
			"entity": "vendor",
			"entity_uuid": "uuid-2344234-sdf6769as"
			}
	],
	"transaction_dt": "2025-07-24 00:00:00"
}
```
`transaction_id` - id транзакции в базе be-pay (покупка тарифа)
`subscriptions` - массив оплаченных подписок, то есть массив оплаченных аккаунтов (vendor), при текущем UI в массиве будет один элемент.
`transaction_dt` - дата транзакции (покупка тарифа)
> `transaction_dt` считается датой начала действия подписки, если по данному тарифу нет действующей подписки. Если действующая подписка есть, то датой начала будет считаться дата окончания последней действующей подписки.


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Subscriptions created (0 - subscription already was in db)",
	"data": {
		"subscription_ids_created": [
			8,
			9
		]
	}
}
```
`subscription_ids_created` - массив id созданных подписок



## 'getHistory`
### Доступ: `user`

**GET** `/api/v1/subscriptions/getHistory`
**POST** `/api/v1/subscriptions/getHistory`

### Описание:
Получить историю подписок.

для POST запроса
### Тело запроса:
```json
{
	"dt_from":"2023-08-24 00:00:00"
}
```

`dt_from` - дата, с которой надо получить все подписки пользователя (израсходованные и действующие)


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Subscriptions history received",
	"data": [
		{
			"id": 4,
			"transaction_id": 388473,
			"user_id": 42,
			"tariff_id": 3,
			"entity": "vendor",
			"entity_uuid": "uuid-2",
			"dt_from": "2025-07-24 00:00:00",
			"dt_to": "2024-08-24 00:00:00"
		},
		{
			"id": 8,
			"transaction_id": 388493,
			"user_id": 42,
			"tariff_id": 3,
			"entity": "vendor",
			"entity_uuid": "uuid-2",
			"dt_from": "2025-08-24 00:00:00",
			"dt_to": "2024-09-24 00:00:00"
		}
	]
}
```
в `data` массив всех подписок пользователя
