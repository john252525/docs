# 📘 Binder API TariffController Documentation

## Base Path
`/api/v1/tariffs/{method}`

## Authentication
- API Key required via:
  - Header: `X-Api-Key`
  - Query parameter: `key`

## Error Format
```json
{
  "ok": false,
  "errors": ["error_message"]
}

POST /add
{
  "name": "premium",
  "price": 13.99,
  "duration": 15,
  "access": [
    "amocrm",
    "whatsapp",
  ]
}