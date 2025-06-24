# 📘 Binder API VendorController Documentation

## Module Base Path
`/api/v1/vendor/{method}`


## `getAll`

**GET** `/api/v1/vendors/getAll`

### Описание:
Получить всех вендоров фронтенда - type - `frontend_vue`.

### Ответ:
- **200 OK**
```json
{
  "ok": true,
  "data": [
    {
      "id": 1,
      "uuid": "deaa8077-604d-4507-96f8-2ebaf27c531b",
      "type": "frontend_vue",
      ...
    },
    {
      "id": 2,
      "uuid": "bb6ed694-9eff-46bf-9b4b-d205d999631e",
      "type": "frontend_vue",
      ...
    }
  ]
}
```


## `getById`

**GET** `/api/v1/vendors/getById/{vendorId}`

### Описание:
Получить вендора по ID.

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"data": {
		"id": "1",
		"uuid": "8f1d7ab5-db5d-49cb-a304-4ec5dc40b547",
		"dt_ins": "2025-06-18 10:14:15",
		"type": "frontend_vue",
		"token": "{}",
		"login": "vendor_login",
		"source": "",
		"enable": "1"
	}
}
```

## `getByIds`

**POST** `/api/v1/vendors/getByIds`

### Описание:
Получить вендоров по массиву ID.

### Тело запроса:
```json
{
  "vendor_ids": [191, 192]
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"data": {
		"vendors": [
			{
				"id": "191",
				"uuid": "403ac2e1-7335-4e0c-ac3c-3be482abd712",
				"dt_ins": "2025-06-18 12:14:46",
				"type": "connect",
				"token": "",
				"login": "",
				"source": "",
				"enable": "1"
			},
			{
				"id": "192",
				"uuid": "254505cd-8c22-437d-be6e-dff153943b41",
				"dt_ins": "2025-06-18 10:14:46",
				"type": "touchapi",
				"token": "0a02fbc...",
				"login": "79909009999",
				"source": "telegram",
				"enable": "1"
			}
		]
	}
}
```

## `getRefId`

**GET** `/api/v1/vendors/getRefId/{vendorId}`

### Описание:
Получить реферальный ID вендора (пока это uuid).

### Ответ:
- **200 OK**
```json
{
  "ok": true,
  "data": {
    "ref_id": "deaa8077-604d-4507-96f8-2ebaf27c531b"
  }
}
```


## `addReferral`

**POST** `/api/v1/vendors/addReferral/{vendorId}`

### Описание:
Добавить реферала вендора.
`{vendorId}` - id реферрера
Перед добавлением реферала приглпшенный вендор должен уже существовать в базе!

### Тело запроса:
```json
{
  "email": "newvendor@example.com",
}
```
`email` - почта приглашенного вендора

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Referral added"
}
```

## `getAllReferrals`

**GET** `/api/v1/vendors/{vendor_id}/getAllReferrals`

### Описание:
Получение всех рефералов вендора


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"data": {
		"referral_ids": [
			"2884",
			"2885"
		]
	}
}
```
Массив `referral_ids` будет пустой, если рефералов нет


