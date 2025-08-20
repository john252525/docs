## Touchapi chats API

### Dev url: https://chats.developtech.ru

## Базовый путь:
`/{resource}/{method}`

## Авторизация пользователя
Через заголовок `Bearer Token`
Authorization: Bearer d83yhd8346...dsfds
> access token пользователя такой же, который используется для bapi88

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