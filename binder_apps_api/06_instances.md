# 📘 Binder API InstanceController Documentation

## Module Base Path
`/api/v1/instances/{method}`

## `getInfoByToken`
### Доступ: `user`

**GET** `api/v1/instances/getInfoByToken

### Описание:
Получает аккаунты из различных источников

### Необязательные параметры
`group`:
- messenger - получить все аккаунты мессенджеров
- crm - получить все аккаунты CRM
- bulk - получить аккаунт Whatsapi

Для мессенджеров может быть указан `source` (whatsapp, telegram)\
Для CRM может быть указан `type` (amocrm, bitrix24, megaplan) и `with_tokens` (по умолчанию - false)


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Instances received",
	"data": {
		"instances": [
			{
				"id": 54,
				"uuid": "d08f76d0-73c7-4443-afaf-cd55673242",
				"dt_ins": "2025-07-15 14:03:45",
				"type": "bitrix24",
				"login": "e5ac70....2fad2410",
				"source": "b24-xxxxxx.bitrix24.ru",
				"enable": 1
			},
			{
				"id": 234,
				"uuid": "a92ccd53-a21a-4134-b6ba-97a74df016d4",
				"dt_ins": "2025-07-28 20:24:04",
				"type": "amocrm",
				"login": "account.amocrm.ru",
				"source": "",
				"enable": 1
			}
		]
	}
}
```
