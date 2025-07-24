# 📘 Binder API VendorController Documentation

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
Получение всех рефералов пользователя


### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Referrals received",
	"data": {
		"referral_ids": [
			47,
			45
		]
	}
}
```
При отсутствии рефералов вернктся успешный ответ, но массив `referral_ids` будет пустой


