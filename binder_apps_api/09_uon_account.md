# 📘 UonAccount API - Blocked Messenger Users Documentation

## Блокирование пользователей мессенджеров для отключения проброса сообщений в UON (пользователи, которые не являются клиентами, а сотрудниками компании)

## Module Base Path
`/uon-account/{method}`

### Авторизация
[Общая информация по API](/00_common.md)

## `blockMessengerUser`
**POST** `/uon-account/blockMessengerUser`

### Обязательные параметры:
`phone` и/или `thread`/`source`

### Тело запроса:
```json
{
    "uuid": "2e31b1d9-e359-41ef-9fef-3f768f45907a",
    "user_id": 170,
    "name": "Some name",
    "brand_slug": "whatsapi",
    "phone": "79009009090"
}
```
`uuid` - UUID вендора uon\
`name` - имя для отображения в списке заблокированных пользователей\

### Ответ:
- **200 OK**
```json
{
    "ok": true,
    "message": "User has been blocked",
    "data": {}
}
```

## `unblockMessengerUser`
**POST** `/uon-account/unblockMessengerUser`

### Обязательные параметры:
`phone` или `thread` (при `thread` требуется `source`)

### Тело запроса:
```json
{
    "uuid": "2e31b1d9-e359-41ef-9fef-3f768f45907a",
    "user_id": 170,
    "brand_slug": "whatsapi",
    "phone": "79009009090"
}
```

### Ответ:
- **200 OK**
```json
{
    "ok": true,
    "message": "User has been unblocked",
    "data": true
}
```

## `getBlockedMessengerUsers`
**POST** `/uon-account/getBlockedMessengerUsers`

### Тело запроса:
```json
{
    "uuid": "2e31b1d9-e359-41ef-9fef-3f768f45907a",
    "user_id": 170,
    "brand_slug": "whatsapi"
}
```

### Ответ:
- **200 OK**
```json
{
    "ok": true,
    "message": "Blocked users received",
    "data": [
        {
            "id": "1",
            "name": "Пользователь 1",
            "phone": "",
            "source": "telegram",
            "thread": "user_id-90029901",
            "enable": "1",
            "dt_ins": "2026-01-14 16:44:52",
            "dt_upd": "2026-01-14 13:45:10",
            "hook_id": "0"
        },
        {
            "id": "2",
            "name": "Пользователь 2",
            "phone": "79009009090",
            "source": "",
            "thread": "",
            "enable": "1",
            "dt_ins": "0000-00-00 00:00:00",
            "dt_upd": "2026-01-15 16:30:37",
            "hook_id": "0"
        }
    ]
}
```

## Настройки аккаунта UON

## `getSettings`
**GET** `/uon-account/getSettings`
**POST** `/uon-account/getSettings`

## Обязательный параметр
`uuid` - UUID вендора uon

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Settings received",
	"data": {
		"clients": {
			"set_default_manager": true
		},
		"requests": {
			"disable": false,
			"disable_creation": false,
			"set_default_manager": true
		},
		"actions": {
			"block": false,
			"block_incoming": false,
			"block_outgoing": false
		}
	}
}
```
- всегда возвращаются параметры по умолчанию, даже если у вендора их нет в базе данных.

## Описание
`clients` - настройки для сущености `client` (клиент) в uon\
`requests` - настройки для сущености `request` (обращение) в uon\
`actions` - настройки для сущености `request action` (касание) в uon

`set_default_manager` - устанавливать менеджера по умолчанию при создании новых клиентов и обращений (например, первого активного, если не определено настройками)

`requests.disable` - отключить поиск и создание обращений, никакие касания не добавляются в обращения, только в историю общения клиента\
`requests.disable_creation` - отключить создание обращений (если обращение есть, то касание будет добавлено в него)

`actions.block` - заблокировать создание касаний в U-ON (блокируются все сообщения, и входящие, и исходящие (из мессенджера), но можно отправлять исходящие из U-ON)\
`actions.block_incoming` - заблокировать создание касаний в U-ON для входящих (если пришло сообщение в подключенный мессенджер, в UON оно не пробрасывается)\
`actions.block_outgoing` - заблокировать создание касаний в U-ON для исходящих (если писать из мессенджера, то в U-ON такие сообщения пробрасываться не будут)


## `saveSettings`
**POST** `/uon-account/saveSettings`

## Обязательный параметр
`uuid` - UUID вендора uon (GET параметром или в теле)

### Тело запроса (обязательно):
```json
{
    "clients": {
        "set_default_manager": true
    },
    "requests": {
        "disable": false,
        "disable_creation": false,
        "set_default_manager": true
    },
    "actions": {
        "block": false,
        "block_incoming": false,
        "block_outgoing": false
    }
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Settings saved",
	"data": true
}
```


## getHistory
**GET** или **POST** `/uon-account/getHistory`

## Обязательные параметры:
`uuid` - UUID вендора U-ON\
`user_id` - ID пользователя (если не авторизован)

## Опциональные параметры:
`date_from` - начальная дата (формат YYYY-MM-DD или YYYY-MM-DD HH:MM:SS)\
`date_to` - конечная дата (формат YYYY-MM-DD или YYYY-MM-DD HH:MM:SS)\
`page` - номер страницы (по умолчанию: 1)\
`per_page` - количество записей на странице (по умолчанию: 50)\
`messenger` - фильтр по мессенджеру: whatsapp, telegram, max, vk\
`status` - фильтр по статусу: pending, success, fail\
`filter_by_vendor` - фильтровать только по текущему U-ON вендору (true/false, по умолчанию false), если параметр не установлен, будут выведены все сообщения (в том числе где uon_vendor_id = 0)

## Специфичные методы поиска (приоритетные):
`search_number` - поиск по номеру телефона (обязателен date_from)\
`request_id` - поиск по request_id\
`hook_id` - поиск по hook_id


### Минимальное тело запроса (либо GET параметры):
```json
{
    "uuid": "a7e08aef-967b-49d2-906c-e99d45833011",
    "user_id": 170,
    "date_from": "2024-01-01",
    "date_to": "2024-01-31"
}
```

```json
{
    "uuid": "a7e08aef-967b-49d2-906c-e99d45833011",
    "user_id": 170,
    "date_from": "2024-01-01",
    "date_to": "2024-01-31",
    "messenger": "whatsapp",
    "status": "success",
    "filter_by_vendor": true,
    "page": 1,
    "per_page": 50
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "History received",
	"data": {
		"messages": [
			{
				"id": "66",
				"user_id": "132",
				"uon_vendor_id": "5",
				"hook_id": "1856299",
				"task_id": "54376",
				"messenger": "telegram",
				"sent_from": "miytgmtum4wtknbxga",
				"sent_to": "user_id-5742728215",
				"number": "79366000000",
				"outgoing": "1",
				"from_messenger": "1",
				"manager_user_id": "0",
				"tourist_user_id": "24",
				"content": "вот",
				"request_id": "930",
				"action_id": "69623",
				"thread": "user_id-5742728215",
				"item": "160435",
				"status": "success",
				"fail_reason": "0",
				"meta": "{}",
				"dt_ins": "2026-02-01 19:34:18",
				"dt_upd": "2026-02-01 19:34:19",
				"dt_msg": "2026-02-01 19:34:18"
			},
            {
				"id": "1",
				"user_id": "132",
				"uon_vendor_id": "5",
				"hook_id": "1856211",
				"task_id": "54343",
				"messenger": "telegram",
				"sent_from": "miytgmtum4wtknbxga",
				"sent_to": "user_id-5742728215",
				"number": "79366000000",
				"outgoing": "1",
				"from_messenger": "1",
				"manager_user_id": "0",
				"tourist_user_id": "24",
				"content": "",
				"request_id": "930",
				"action_id": "69601",
				"thread": "user_id-5742726215",
				"item": "160413",
				"status": "success",
				"fail_reason": "0",
				"meta": "{}",
				"dt_ins": "2026-02-01 19:27:09",
				"dt_upd": "2026-02-01 19:27:11",
				"dt_msg": "2026-02-01 19:27:08"
			}
		],
		"pagination": {
			"current_page": 20,
			"per_page": 50,
			"total": 973,
			"total_pages": 20
		},
		"dictionaries": {
			"statuses": {
				"pending": "В ожидании",
				"success": "Успешно",
				"fail": "Ошибка",
				"": ""
			},
			"fail_reasons": {
				"unknown": "Неизвестная ошибка",
				"no_binds": "Канал с CRM не создан",
				"no_binds_after_filter": "Подходящий канал не найден",
				"no_subscription": "Нет подписки",
				"binds_disabled": "Канал с CRM отключен",
				"messenger_not_set": "Не выбран мессенджер",
				"privacy_settings": "Номер телефона закрыт",
				"blocked_by_settings": "Заблокировано настройками",
				"api_error": "Ошибка API",
				"limit_reached": "Лимит запросов исчерпан",
				"network_issue": "Сетевая проблема",
				"no_phone": "Номер телефона не найден"
			},
			"messengers": {
				"whatsapp": "WhatsApp",
				"telegram": "Telegram",
				"max": "MAX",
				"vk": "VK"
			}
		}
	}
}
```