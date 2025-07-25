# 📘 Binder API TariffController Documentation

## Module Base Path
`/api/v1/tariffs/{method}`


## 'getAll' (default) 
### Доступ: `user`

**GET** `/api/v1/tariffs/` или `/api/v1/tariffs/getAll`

### Описание:
Получить все действующие тарифы.
Если для данного приложения нет тарифов в базе, будут использованы дефолтные - 'brand_slug' = 'default'

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": null,
	"data": [
		{
			"id": 3,
			"brand_slug": "app1",
			"code": "touchapi-whatsapp",
			"period": "1m",
			"name": "Whatsapp 1 Месяц",
			"price": 1050,
			"currency": "RUB",
			"dt_ins": "2025-07-23 20:04:17",
			"dt_upd": "2025-07-23 20:29:03",
			"enable": 1
		}
	]
}
```
В `data` - массив тарифов, где\
"brand_slug" - к какому бренду принадлежит тариф (может быть только либо текущий бренд, либо 'default')\
"code" - [type]-[source] или просто [type] (но в дальнейшем может быть и еще какая-то другая схема формирования кода)\
"period" - период действия - 1d, 5d, 7d - дни, 1m, 2m - месяцы, 1y, 2y - годы\
Уникальный индекс по этим 3 колонкам, у бренда не может быть 2 одинаковых тарифа с одним и тем же периодом действия. Но может быть 2 тарифа с одинаковым кодом, но с разным периодом действия.\
"name" - имя для отображения, если где-то будет использоваться\
"enable" - всегда 1, так как неактуальные тарифы незачем возвращать на фронт


## 'tariffs/getByCode`
### Доступ: `user`

**POST** `/api/v1/tariffs/getByCode`

### Описание:
Получить все действующие тарифы для определенного типа вендора.

### Тело запроса:
```json
{
	"code": "touchapi-whatsapp"
}
```

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": null,
	"data": [
		{
      //массив тарифов
		}
	]
}
```


## '/tariffs/3/getById`
### Доступ: `user`


**GET** `/api/v1/tariffs/3/getById`
* пока избыточно, позже переделаю на `/api/v1/tariffs/3`


### Описание:
Получить тариф по ID.


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": null,
	"data": [
		{
      //тариф
		}
	]
}
```

