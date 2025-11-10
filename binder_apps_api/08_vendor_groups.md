# 📘 Binder API VendorGroupController Documentation

## Module Base Path
`/api/v1/groups/{method}`

## `default`
### Доступ: `user`

**GET** `api/v1/groups`

### Описание:
Получение групп с вендорами для каждой группы


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Vendor groups received",
	"data": {
		"vendor_groups": {
			"6d42d776-019a-7000-5c63a04f0444": {
				"id": "1",
				"uuid": "6d42d776-019a-7000-5c63a04f0444",
				"type": "cascade",
				"name": "Group 55d794d19292",
				"settings": "",
				"vendors": []
			},
			"6d4bb57f-019a-7000-e19867c154f4": {
				"id": "4",
				"uuid": "6d4bb57f-019a-7000-e19867c154f4",
				"type": "cascade",
				"name": "2",
				"settings": "{\"cascade\":[\"telegram\",\"whatsapp\",\"max\"]}",
				"vendors": {
					"0617e94b-abf4-401e-af22-03ea65cc8d25": {
						"id": "3",
						"uuid": "0617e94b-abf4-401e-af22-03ea65cc8d25",
						"token": "3d2a37e9-9192-4e5a-8c59-df13327748de",
						"login": "miytmndxmewtgztbmi",
						"source": "whatsapp"
					},
					"906effac-771b-48a7-9be0-3aa146857b6d": {
						"id": "4",
						"uuid": "906effac-771b-48a7-9be0-3aa146857b6d",
						"token": "3d2a37e9-9192-4e5a-8c59-df13327748de",
						"login": "miytmndxmewtoyzymm",
						"source": "whatsapp"
					}
				}
			}
		}
	}
}
```


## `add`
### Доступ: `user`

**POST** `api/v1/groups/add`

### Описание:
Добавление группы.

### Необязательные параметры
- type - тип группы (пока только `cascade`)
- name - имя группы
- settings - объект с настройками группы, для cascade - порядок отправки

### Тело запроса (необязательное):
```json
{
	"type": "cascade",
	"name": "Test name",
	"settings": {
		"cascade": [
			"whatsapp", "telegram"
		]
	}
}
```
> Без параметров будет создана группа с именем - "Group [последний сегмент uuid]"


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Vendor group created",
	"data": {
		"result": 1
	}
}
```


## `delete`
### Доступ: `user`

**POST** `api/v1/groups/delete`

### Описание:
Удаление группы.

### Обязательные параметры
- uuid - uuid группы

### Тело запроса (необязательное):
```json
{
	"uuid": "6d4bb57f-019a-7000-e19867c154f4",
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Vendor group deleted",
	"data": {
		"result": 1
	}
}
```



## `update`
### Доступ: `user`

**POST** `api/v1/groups/update`

### Описание:
Изменение группы.

### Обязательные параметры
- uuid - uuid группы

### Необязательные параметры
- name - имя группы
- settings - объект с настройками группы

### Тело запроса (необязательное):
```json
{
  	"uuid": "6d4bb57f-019a-7000-e19867c154f4",
	"name": "Имя группы",
	"settings": {
		"cascade": [
				"telegram",
				"whatsapp"
			]
	}
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Vendor group updated",
	"data": {
		"result": true
	}
}
```



## `addVendor`
### Доступ: `user`

**POST** `api/v1/groups/addVendor`

### Описание:
Добавление вендора в группу.

### Обязательные параметры
- group_uuid - uuid группы
- vendor_uuid - uuid вендора


### Тело запроса:
```json
{
  	"group_uuid": "6d4bb57f-019a-7000-e19867c154f4",
	"vendor_uuid": "906effac-771b-48a7-9be0-3aa146857b6d"
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Vendor added to group",
	"data": {
		"result": true
	}
}
```


## `deleteVendor`
### Доступ: `user`

**POST** `api/v1/groups/deleteVendor`

### Описание:
Удаление вендора из группы.

### Обязательные параметры
- group_uuid - uuid группы
- vendor_uuid - uuid вендора


### Тело запроса:
```json
{
  	"group_uuid": "6d4bb57f-019a-7000-e19867c154f4",
	"vendor_uuid": "906effac-771b-48a7-9be0-3aa146857b6d"
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Vendor deleted from group",
	"data": {
		"result": true
	}
}
```



