## Базовый путь:  
`/api/v1/{module}/{method}`

## Авторизация
Через заголовок `Bearer Token`
Authorization: Bearer d83yhd8346


## Формат ошибок
```json
{
  "ok": false,
  "errors": ["error_message"]
}

Ошибки в массиве, так как их может быть несколько.