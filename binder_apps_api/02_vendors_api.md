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
Получить реферальный ID вендора - JWT токен с закодированным uuid вендора в payload.

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"data": {
		"ref_id": "eyJ0eX...1NiJ9.WyIx...UiXQ.LP3r...p_TI"
	}
}
```


## `addReferral`

**POST** `/api/v1/vendors/addReferral`

### Описание:
Добавить реферала вендора.
Перед добавлением реферала приглпшенный вендор должен уже существовать в базе!
То есть сначала вызывается метод register и если он успешно завершился, вызывается данный метод.

### Тело запроса:
```json
{
	"ref_id": "ey...JI1NiJ9.Wy...iXQ.LP3r9ECdyp8....Hp_TI",
  	"email": "newvendor@example.com"
}
```
`ref_id` - JWT токен, служащий как `ref_id`, в payload закодирован `uuid` вендора, токен безсрочный (на фронте ничего извлекать не надо, просто передать токен на бекенд)
`email` - почта приглашенного вендора, использующаяся при регистрации

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Referral added",
	"data": {
		"parent_uuid": "1d2d78...85e",
		"referral_uuid": "fgh....ddfg"
	}
}
```
`parent_uuid` - uuid родительского вендора 
`referral_uuid` - uuid вендора - реферала
возвращаются просто для информации


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


