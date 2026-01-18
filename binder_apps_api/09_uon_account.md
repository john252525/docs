# 📘 UonAccount API - Blocked Messenger Users Documentation

## Блокирование пользователей мессенджеров для отключения проброса сообщений в UON (пользователи, которые не являются клиентами, а сотрудниками компании)

## Module Base Path
`/uon-account/{method}`

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