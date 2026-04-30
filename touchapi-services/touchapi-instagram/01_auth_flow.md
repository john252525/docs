## Touchapi Instagram instance auth

### Base url: `https://bapi88.[domain]/api/v1`

1. Получить ссылку для авторизации в Instagram

## `getAuthUrl`

**GET** `/instances/getAuthUrl`

### Описание:
Получение ссылки для авторизации через Instagram.

### Обязательные параметры:
`login`
`source`
`type`

### Успешный ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Auth url received",
	"data": {
		"auth_url": "https://....",
	}
}

2. Отобразить полученный `auth_url` пользователю в виде кнопки или ссылки, чтобы он мог по ней перейти в Instagram

3. После того, как пользовтель вернется в ЛК надо отобразить какое-то подтверждение, что он авторизовался в Instagram.

4. После подтверждения проверить статус через `getInfo`