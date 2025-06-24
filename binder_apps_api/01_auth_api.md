# 📘 Binder API AuthController

## Module Base Path:  
`/api/v1/auth/{method}`

Методы:

## `register`

**POST** `/api/v1/auth/register`

### Описание:
Регистрация нового пользователя (вендора) и отправка письма для подтверждения почты.

### Тело запроса:
```json
{
  "email": "vendor@example.com",
  "password": "password123",
  "type": "frontend_vue",
  "app" : "app2"
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
    "email": "vendor@example.com"
  }
}
```

## `forgotPassword`

**POST** `/api/v1/auth/forgotPassword`

### Описание:
Запросить сброс пароля (отправляется письмо с ссылкой на страницу сброса пароля).

### Тело запроса:
```json
{
  "email": "user@example.com",
  "app" : "app2"
}
```

### Ответ:
- **200 OK**
```json
{
  "ok": true,
  "message": "Password reset link has been sent."
}
```

## `resetPassword`

**POST** `/api/v1/auth/resetPassword`

### Описание:
Сброс пароля по токену. Отправляется со страницы сброса пароля после того, как вендор установил новый пароль.

### Тело запроса:
```json
{
  "token": "reset_token",
  "password": "new_password"
}
```

### Ответ:
- **200 OK**
```json
{
  "ok": true,
  "message": "Password has been reset successfully."
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
		"token": "eyJ0...Yo",
		"expires_in": 604800
	}
}
```

