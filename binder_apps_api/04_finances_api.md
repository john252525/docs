# 📘 Binder API VendorFinanceController Documentation

## Base Path
`/api/v1/vendor-finance/{method}`

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