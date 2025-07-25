# 📘 Binder API FormController Documentation

## Module Base Path
`/api/v1/forms/{method}`

## `getForm`
### Доступ: `public`

**GET** `api/v1/forms/getForm`

### Описание:
Получить форму. Сейчас по умолчанию используется имя формы `addAccount`, в дальнейшем, если потребуется, можно отправлять параметр `form` с именем формы, которую надо получить.
Если формы для данного приложения не создано, будет использована форма `default` (настройки форм хранятся в /brands/{brand_slug}/forms/{form_name}Form.php)


### Тело запроса (сейчас не обязательно, так как форма по сути одна):
```json
{
	"form": "addAccount",
	"locale": "ru",
}
```
> Перед тем, как запрашиать другие локали, следует убедиться, что файлы настроек для них существуют. Если параметр не передан, то по дефолту `ru`.


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Form structure",
	"data": [
		{
			"parent_id": null,
			"id": 1,
			"element": "label",
			"for": "group",
			"text_content": "Выберите вид аккаунта"
		},
		{
			"parent_id": null,
			"id": 2,
			"element": "select",
			"name": "group"
		},
		{
			"parent_id": 2,
			"id": 3,
			"element": "option",
			"value": "messenger",
			"text_content": "Messendger"
		}
        ...
    ]
}
```
`id` - id элемента (порядковые номера для ссылок на элемент, как родительский)
`parent_id` - id родительского элемента
`element` - DOM элемент, который необходимо создать, значение полностью совпадает с тегом элемента в HTML
`text_content` - Текст контент в прямом понятии этого слова в HTML, то есть текстовый контент элемента. То есть это тот текст, который будет отображаться пользователю.
`validate` - надо ли валидировать значение
> Все остальные параметры соответсвуют атрибутам DOM элемента данного вида


Пример:
```json
{
    [
        {
            "parent_id": null,
            "id": 1,
            "element": "label",
            "for": "group",
            "text_content": "Выберите вид аккаунта"
        },
        {
            "parent_id": null,
            "id": 2,
            "element": "select",
            "name": "group"
        },
        {
            "parent_id": 2,
            "id": 3,
            "element": "option",
            "value": "messenger",
            "text_content": "Messendger"
        },
        {
            "parent_id": 2,
            "id": 4,
            "element": "option",
            "value": "crm",
            "text_content": "CRM"
        }
    ]
}
```

Результат на чистом HTML
```html
<label for="group">Выберите вид аккаунта</label>
<select name="group">
  <option value="messenger">Messendger</option>
  <option value="crm">CRM</option>
</select>
```





## Старые методы (больше не используются)

## `getAddInstanceForm`
### Доступ: `public`

**GET** `/api/v1/forms/getAddInstanceForm`

### Описание:
Получить форму для добавления аккаунта.

### Ответ:
- **200 OK**
```json

{
"ok": true,
"message": null,
"data": [
    {
        "id": "1",
        "parent_id": "0",
        "name": "group",
        "value": "messenger",
        "type": "select"
    },
    ...
    ]
}
```

## `getAddInstanceForm2`
### Доступ: `public`

**GET** `/api/v1/forms/getAddInstanceForm`

### Описание:
Получить форму для добавления аккаунта версия 2.

### Ответ:
- **200 OK**
```json

{
"ok": true,
"message": null,
"data": {
    "type": "select",
    "required": true,
    "validate": false,
    "name": "group",
    "options": [
        {
            "value": "messenger",
            "children": {
                "type": "select",
                "required": true,
                "validate": false,
                "name": "source",
                "options": [
    ...
    }
}
```