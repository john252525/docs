# 📘 Binder API AuthController

## Module Base Path:  
`/api/v1/auth/{method}`

Методы:

## `register`

**POST** `/api/v1/auth/register`

### Описание:
Регистрация нового пользователя и отправка письма для подтверждения почты.

### Тело запроса:
```json
{
  "email": "vendor@example.com",
  "password": "password123",
}
```

### Успешный ответ:
- **200 OK**
```json
{
  "ok": true,
  "message": "Registration successful. Email sent."
}
```

---

## `verifyEmail`

**POST** `/api/v1/auth/verifyEmail`

### Описание:
Подтверждение email по токену из письма.

### Тело запроса:
```json
{
  "token": "verification_token"
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Email verified successfully.",
	"data": {
		"email": "name@gmail.com"
	}
}
```

## `forgotPassword`

**POST** `/api/v1/auth/forgotPassword`

### Описание:
Запросить сброс пароля, если пользователь забыл пароль и не может войти в ЛК (отправляется письмо с ссылкой на страницу сброса пароля).

### Тело запроса:
```json
{
  "email": "user@example.com",
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Password reset link has been sent.",
	"data": {
		"email": "user@example.com"
	}
}
```

## `resetPassword`

**POST** `/api/v1/auth/resetPassword`

### Описание:
Сброс пароля по токену. Отправляется со страницы сброса пароля после того, как вендор установил новый пароль.

### Тело запроса для сброса по токену:
```json
{
  "token": "reset_token_из_письма",
  "new_password": "new_password"
}
```

### Тело запроса для сброса по действующему паролю:
```json
{
	"password": "действующий_пароль",
	"new_password": "новый_пароль"
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Password has been reset.",
	"data": {
		"user_id": 42
	}
}
```

## `login`

**POST** `/api/v1/auth/login`

### Описание:
Аутентификация пользователя.

### Тело запроса:
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Login successful.",
	"data": {
		"token": "eyJ0e...bSrD0",
		"expires_at": "2025-07-30 20:58:22",
		"refresh_token": "4ecf17cb2...e2c4bbd72",
		"refresh_expires_at": "2025-10-21 20:58:22"
	}
}
```
Все даты по UTC.


## `verifyToken`

**GET** `/api/v1/auth/verifyToken`

### Описание:
Проверка токена на актуальность.


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Token verified",
	"data": {
		"brand_slug": "brand",
		"user_id": 42,
		"email": "name@ygmail.com",
		"exp": 1753953050
	}
}
```


## `refreshToken`

**POST** `/api/v1/auth/refreshToken`

### Описание:
Замена токенов.

### Тело запроса:
```json
{
	"refresh_token": "e7aba....93a617",
  "email": "name@gmail.com"
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Token refreshed successfully.",
	"data": {
		"token": "eyJ0eXAiOi...hns_bJ4U",
		"expires_at": "2025-07-24 16:39:27",
		"refresh_token": "f5cbc6330...c86ce",
		"refresh_expires_at": "2025-10-15 16:39:27"
	}
}
```


