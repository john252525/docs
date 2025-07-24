## Базовый путь:  
`/api/v1/{resource}/` - метод, установленный по умолчанию
`/api/v1/{resource}/{method}` - выполнить метод
`/api/v1/{resource}/{id}/{method}` - выполнить метода для определенного ID ресурса

## Авторизация пользователя
Через заголовок `Bearer Token`
Authorization: Bearer d83yhd8346...dsfds

Токен выдается методом `auth/login`

## Авторизация admin (по ключу)
Через заголовок `X-Api-Key`
или
Через параметр `key`

## Формат успешных ответов

```json
{
  "ok": true,
  "message": "Success message",
  "data": {}
}
```

`message` - Общее сообщение или null
`data` - Возвращенные данные, если они предполагаются, могут быть пустыми

## Формат ошибок

```json
{
  "ok": false,
  "message": "Some error",
  "errors": ["error_message 1", "error_message 2"]
}
```

`message` - Общее сообщение об ошибке
`errors` - Массив конкретных ошибок, одна или больше