# 📘 Binder API InvoiceController Documentation

## Module Base Path
`/api/v1/invoices/{method}`

## `saveInn`
### Доступ: `user`

**GET** `api/v1/invoices/saveInn`

### Описание:
Сохраняет ИНН, введенный пользователем на фронтенде (Разместить поле для ввода в настройках)


### Тело запроса:
```json
{
	"inn": "50********471"
}
```
`inn` - добавить проверку по формату - только числа, минимально 10 знаков (для ЮЛ), максимально 12 (для ИП)


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Inn saved",
	"data": {
		"result": true
	}
}
```


## `getInn`
### Доступ: `user`

**GET** `api/v1/invoices/getInn`

### Описание:
Получает ИНН из базы, если он был предварительно сохранен.


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Inn received",
	"data": {
		"inn": "50******6474"
	}
}
```


## `generateInvoice`
### Доступ: `user`

**GET** `api/v1/invoices/generateInvoice`

### Описание:
Получает ссылку на сгенерированный счет. Цель: дать пользователям возможность оплатить с р/с компании.

### Параметры
`sum` - сумма пополнения (`api/v1/invoices/generateInvoice?sum=2500`)

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Invoice rendered",
	"data": {
		"invoice_link": "https://bapi88.apitter.com/files/invoices/20250922_50e1dkkf7j47g7hhs48596668bc8.pdf"
	}
}
```

> В истории предусотреть возможность скачать счет повторно, если вруг пользователь его потерял
> `invoice_link` - вывести в виде кнопки скачать или открыть, либо просто в виде ссылки



