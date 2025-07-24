# 📘 Binder API TariffController Documentation

## Module Base Path
`/api/v1/tariffs/{method}`


## 'getAll' (default) 
### Доступ: `user`

**GET** `/api/v1/tariffs/` или `/api/v1/tariffs/getAll`

















## `addReferral`
### Доступ: `public`

**POST** `/api/v1/vendors/addReferral`

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