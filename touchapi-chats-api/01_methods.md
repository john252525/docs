# 📘 Touchapi Chats API


Методы:

## `test`

**GET** `/test/test`

### Описание:
Тестовый метод для проверки доступности API.


### Успешный ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Test success",
	"data": {
		"brand_slug": "app1",
		"email": "mail@mail.com",
		"user_id": 235
	}
}
```
Просто возвращает данные извлеченные из access token. Это значит, что токен принят и API для данного пользователя работает

---

## `register`

**GET** `auth/register`

### Описание:
Регистрация пользоватяля в чатах

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Authentication successful",
	"data": {
		"chats_url": "https://chat.touch-api.com/chat/?satkn=c0ba2e8c-6dbd-4052-b08f-991ccfc74e24",
		"email": "mail@mail.com",
		"user_id": 235
	}
}
```
`chats_url` - готовая ссылка чатов пользователя, которую можно открывать во фрейме
`email` и `user_id` - просто дополнительная информация по пользователю приложения, для которого была сформирована ссылка

## `add`

**POST** `/account/add`

### Описание:
Добавляет инстансе Touchapi, как аккаунт.
> Пока можно добавить лишь один аккаунт с одним и тем же 'source'. То есть 2 whatsapp не добавить!

### Тело запроса:
```json
{
	"login": "acclogin",
	"source": "whatsapp",
	"token": "4a66e4c3-9877-487b-9a2f-29bae782556e",
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Account linked successfully",
	"data": {
		"login": "acclogin",
		"source": "whatsapp",
		"token": "4a66e4c3-9877-487b-9a2f-29bae782556e",
		"user_id": 32
	}
}
```

## `delete`

**GET** `/user/delete`

### Описание:
Полностью удаляет пользователя чатов.
> Так как нет возможности по API удалить аккаунт (инстанс Touchapi), необходимо полностью удалять пользователя, пересоздавать его и привязывать нужные аккаунты заново


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "User deleted.",
	"data": {
		"user_id": 42
	}
}
```
