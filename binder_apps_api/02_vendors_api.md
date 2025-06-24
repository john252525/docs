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