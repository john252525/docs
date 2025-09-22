# 📘 Binder API TariffController Documentation

## Module Base Path
`/api/v1/tariffs/{method}`


## 'getAll' (default) 
### Доступ: `user`

**GET** `/api/v1/tariffs/` или `/api/v1/tariffs/getAll`

### Описание:
Получить все действующие тарифы.
Если для данного приложения нет тарифов в базе, будут использованы дефолтные - 'brand_slug' = 'default'

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": null,
	"data": [
		{
			"id": 3,
			"brand_slug": "app1",
			"code": "touchapi-whatsapp",
			"period": "1m",
			"name": "Whatsapp 1 Месяц",
			"price": 1050,
			"currency": "RUB",
			"dt_ins": "2025-07-23 20:04:17",
			"dt_upd": "2025-07-23 20:29:03",
			"enable": 1
		}
	]
}
```
В `data` - массив тарифов, где\
"brand_slug" - к какому бренду принадлежит тариф (может быть только либо текущий бренд, либо 'default')\
"code" - [type]-[source] или просто [type] (но в дальнейшем может быть и еще какая-то другая схема формирования кода)\
"period" - период действия - 1d, 5d, 7d - дни, 1m, 2m - месяцы, 1y, 2y - годы\
Уникальный индекс по этим 3 колонкам, у бренда не может быть 2 одинаковых тарифа с одним и тем же периодом действия. Но может быть 2 тарифа с одинаковым кодом, но с разным периодом действия.\
"name" - имя для отображения, если где-то будет использоваться\
"enable" - всегда 1, так как неактуальные тарифы незачем возвращать на фронт


## 'tariffs/getByCode`
### Доступ: `user`

**POST** `/api/v1/tariffs/getByCode`

### Описание:
Получить все действующие тарифы для определенного типа вендора.

### Тело запроса:
```json
{
	"code": "touchapi-whatsapp"
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": null,
	"data": [
		{
      //массив тарифов
		}
	]
}
```


## 'tariffs/getByCodeWithMods`
### Доступ: `user`

**POST** `/api/v1/tariffs/getByCodeWithMods`

### Описание:
Получить все действующие тарифы для определенного типа вендора с модификаторами, бонусами и ценой со скидками.

### Тело запроса:
```json
{
	"code": "touchapi-whatsapp"
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": null,
	"data": [
		{
      //массив тарифов
	  	{
			"id": 6,
			"code": "standard",
			"period": "1m",
			"limits": {
				"dialogs": 100,
				"messages": -1,
				"write_first": true,
				"group_chats": true
			},
			"name": "Standard 1 Month",
			"price": 1500,
			"final_price": 800,
			"currency": "RUB",
			"mods": [
				{
					"id": 1,
					"brand_slug": "brand",
					"code": "discount_next_channel_1_500",
					"promo_code": "",
					"description": "Discount for every next channel paid",
					"type": "discount",
					"accumulative_limit": 1,
					"amount": 500,
					"amount_unit": "currency",
					"data": [],
					"is_applied": false
				},
				{
					"id": 5,
					"brand_slug": "brand",
					"code": "bonus_subscription_bulk",
					"promo_code": "",
					"description": "Bulk subscription bonus",
					"type": "bonus",
					"accumulative_limit": 0,
					"amount": 1,
					"amount_unit": "subscription",
					"data": [
						{
							"code": "whatsapi-bulk"
						}
					],
					"is_applied": true
				},
				{
					"id": 6,
					"brand_slug": "brand",
					"code": "discount_next_channel_1_700",
					"promo_code": "",
					"description": "Discount for every next channel paid",
					"type": "discount",
					"accumulative_limit": 1,
					"amount": 700,
					"amount_unit": "currency",
					"data": [],
					"is_applied": false
				},
				{
					"id": 7,
					"brand_slug": "brand",
					"code": "discount_next_channel_1_200",
					"promo_code": "",
					"description": "Discount for every next channel paid",
					"type": "discount",
					"accumulative_limit": 1,
					"amount": 200,
					"amount_unit": "currency",
					"data": [],
					"is_applied": false
				}
			],
			"bonuses": [
				{
					"mod_id": 5,
					"tariff_code": "whatsapi-bulk",
					"tariff_period": "1m",
					"multiplier": 1
				}
			]
		},
		}
	]
}
```
Новые поля:
`limits` - установленные лимиты по тарифу (можно их выводить в тариф, кроме групповых чатов, так как у нас это не реализовано)
> -1 - значит безлимит, ограничение не установлено
`final_price` - цена после примененных скидок для текущего пользователя (цена по которой пользователь может приобрести подписку на данный момент)
`mods` - все доступные модификаоры по тарифу. Для информации можно выводить пользователю описание бонусов - `type` - `bonus`
`bonuses` - массив бонусов, которые будут применены, если покупка произойдет в данный момент (сейчас это только подписки в подарок). В бонусе указан код тарифа и период, на основании которого будет создана бесплатная подписка. Если подходящего тарифа нет, будет указан тариф с периодом `1m` и `multiplier`
> Если `multiplier` = 0, это значит, что бонус применен не будет (не найден тариф, который можно использовать)
> Информацию по бонусам надо отправлять при покупке подписки (см. `subscriptions/createSubscriptions`)

## '/tariffs/3/getById`
### Доступ: `user`


**GET** `/api/v1/tariffs/3/getById`
* пока избыточно, позже переделаю на `/api/v1/tariffs/3`


### Описание:
Получить тариф по ID.


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": null,
	"data": [
		{
      //тариф
		}
	]
}
```

