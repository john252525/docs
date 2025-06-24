# 📘 Binder API AuthController

Базовый путь:  
`/api/v1/auth/{method}`

## Api key
Передается либо в заголовках (`X-Api-Key`), либо в параметрах - `key`


## Ошибки:
Все ошибки возвращаются в следующем формате:
```json
{
  "ok": false,
  "errors": ["..."] //Массив ошибок, может быть несколько
}
```

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
    "token": "jwt_token_here" // можно позже использовать токен для верификации запросов
  }
}
```
## `verifyToken`

**POST** `/api/v1/auth/verifyToken`

### Описание:
Проверка JWT токена на валидность.

Можно передавать как в заголовке, так и в теле запроса.

### Заголовок:
```
Authorization: Bearer your_jwt_token
```

### Или тело запроса:
```json
{
  "token": "your_jwt_token"
}
```

### Ответ:
- **200 OK**
```json
{
  "ok": true,
  "message": "Token verified",
  "data": {
    "vendor_id": 1,
    "email": "user@example.com",
    "exp": 9999999999
  }
}
```
