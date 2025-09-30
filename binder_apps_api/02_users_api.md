# 📘 Binder API UserController Documentation

## Module Base Path
`/api/v1/users/{method}`


## `getRefId`
### Доступ: `user`

**GET** `/api/v1/users/getRefId`

### Описание:
Получить реферальный ID пользователя (короткий ID с закодированным ID пользователя).

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": null,
	"data": {
		"ref_id": "00002Ab3f91"
	}
}
```

## `addReferral`
### Доступ: `public`

**POST** `/api/v1/users/addReferral`

### Описание:
Добавить реферала.
Перед добавлением реферала приглпшенный пользователь должен уже существовать в базе!
То есть сначала вызывается метод register и если он успешно завершился, вызывается данный метод.

### Тело запроса:
```json
{
	"email": "test123123@mail.ru",
	"ref_id": "00002Ab3f91"
}
```
`ref_id` - токен с зашитым user id
`email` - почта приглашенного вендора, использующаяся при регистрации, предварительно с данным email делается регистрация

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Referral added",
	"data": {
		"parent_user_id": 42,
		"referred_user_id": 45
	}
}
```
`parent_user_id` - id родительского пользователя
`referred_user_id` - id приглашенного пользователя
возвращаются просто для информации или дополнительной проверки


## `getAllReferrals`
### Доступ: `user`

**GET** `/api/v1/users/getAllReferrals`

### Описание:
Получение всех рефералов пользователя и их количества


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Referrals received",
	"data": {
		"referrals": [
			{
				"email": "kravcov11@yandex.ru",
				"is_verified": "1",
				"dt_ins": "2025-09-15 19:08:32",
				"enable": "1"
			},
			{
				"email": "97394@powerscrews.com",
				"is_verified": "0",
				"dt_ins": "2025-09-16 06:30:58",
				"enable": "1"
			}
		],
		"referrals_count": 2
	}
}
```
`referrals` - массив пользователей, которые являются рефералами текушего пользователя\
	`email` - email пользователя, который является рефералом текущего пользователя\
	`is_verified` - подтверждена ли почта\
	`dt_ins` - дата регистрации\
	`enable` - статус пользователя\
> При отсутствии рефералов вернется успешный ответ, но массив `referrals` будет пустой и `referrals_count` будет равен 0
> Активность пользователя определять по совокупности `is_verified` и `enable`


## `getContact`
### Доступ: `user`

**GET** `/api/v1/users/getContact`

### Описание:
Получить получает контактную информацию, если она есть.

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "User contact",
	"data": {
		"phone": "79909009090",
		"contact_preferred_channels": [
			"call",
			"telegram"
		]
	}
}
```
`phone` - всегда возвращается в числовом виде, даже если при сохранении формат был иным



## `saveContact`
### Доступ: `user`

**POST** `/api/v1/users/saveContact`

### Описание:
Сохраняет контактный телефон и предпочитаемые каналы связи пользователя.

### Тело запроса:
```json
{
	"phone": "+7(892)6807892",
	"contact_preferred_channels": ["call"]
}
```
`phone` - телефон в любом формате (для сохранения будет приведет к числовому виду)
`contact_preferred_channels` - массив предпочитаемых каналов связи (без жестких критериев)

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "User contact saved",
	"data": {
		"phone_update_result": true,
		"preferred_channels_update_result": true
	}
}
```
