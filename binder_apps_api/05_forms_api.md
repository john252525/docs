# 📘 Binder API FormController Documentation

## Module Base Path
`/api/v1/forms/{method}`


## `getAddInstanceForm`

**GET** `/api/v1/forms/getAddInstanceForm`

### Описание:
Получить форму для добавления аккаунта.

### Ответ:
- **200 OK**
```json

{
"ok": true,
"message": null,
"data": [
    {
        "id": "1",
        "parent_id": "0",
        "name": "group",
        "value": "messenger",
        "type": "select"
    },
    ...
    ]
}
```

## `getAddInstanceForm2`

**GET** `/api/v1/forms/getAddInstanceForm`

### Описание:
Получить форму для добавления аккаунта версия 2.

### Ответ:
- **200 OK**
```json

{
"ok": true,
"message": null,
"data": {
    "type": "select",
    "required": true,
    "validate": false,
    "name": "group",
    "options": [
        {
            "value": "messenger",
            "children": {
                "type": "select",
                "required": true,
                "validate": false,
                "name": "source",
                "options": [
    ...
    }
}
```