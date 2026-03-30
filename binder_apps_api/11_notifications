# 📘 Binder API Documentation: Notifications & Articles

## Module Base Path
- **Notifications:** `/api/v1/notifications/{method}`
- **Articles:** `/api/v1/articles/{method}`

---

# 🔔 Notifications

## `test`
### Доступ: `public`

**GET** `/api/v1/notifications/test`

### Описание:
Тестовый метод для проверки работоспособности модуля уведомлений.

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Notification module works"
}
```

---

## `getAll` (default)
### Доступ: `user`

**GET** `/api/v1/notifications/` или `/api/v1/notifications/getAll`

### Описание:
Получить список уведомлений пользователя с пагинацией.

### Параметры запроса (query):
| Параметр | Тип | Описание |
|----------|-----|----------|
| page | int | Номер страницы (по умолчанию 1) |
| per_page | int | Количество элементов на странице (по умолчанию 20) |
| full | bool | Если `true`, подгружает дополнительную информацию о связанной сущности (статью) |
| user_id | int | (только для admin) ID пользователя, чьи уведомления нужно получить |

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Notifications retrieved",
	"data": [
		{
			"id": 1,
			"user_id": 42,
			"type": "article",
			"item_id": 5,
			"title": "Новая статья опубликована",
			"body": "Опубликована статья 'Как работать с API'",
			"is_read": 0,
			"dt_ins": "2025-03-20 10:00:00",
			"entity": {
				"title": "Как работать с API",
				"description": "Подробное руководство по работе с API",
				"content": "<p>Содержание статьи...</p>"
			}
		}
	],
	"paginator": {
		"total_items": 15,
		"total_pages": 2,
		"current_page": 1,
		"per_page": 20
	}
}
```
- `entity` присутствует только при `full=true` и для типов уведомлений, поддерживающих обогащение (сейчас только `article`).  
- Для типа `message` поле `entity` равно `null` (до реализации MessageService).

---

## `getNotRead`
### Доступ: `user`

**GET** `/api/v1/notifications/getNotRead`

### Описание:
Получить все непрочитанные уведомления пользователя (без пагинации, максимум 1000 записей). Администратор может указать `user_id` для получения уведомлений другого пользователя.

### Параметры запроса (query):
| Параметр | Тип | Описание |
|----------|-----|----------|
| since_date | string | Дата в формате `Y-m-d H:i:s`. Если указана, возвращаются уведомления, созданные позже этой даты |
| full | bool | Если `true`, подгружает дополнительную информацию о связанной сущности |
| user_id | int | (только для admin) ID пользователя |

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Unread notifications retrieved",
	"data": [
		{
			"id": 2,
			"user_id": 42,
			"type": "article",
			"item_id": 6,
			"title": "Новое обновление",
			"body": "Вышло обновление 2.0",
			"is_read": 0,
			"dt_ins": "2025-03-21 09:00:00"
		}
	],
	"total": 1
}
```

---

## `getNotificationItem`
### Доступ: `user`

**GET** `/api/v1/notifications/getNotificationItem`

### Описание:
Получить конкретное уведомление по типу и идентификатору связанного элемента. Администратор может указать `user_id` для получения уведомления другого пользователя.

### Параметры запроса (query):
| Параметр | Тип | Обязательный | Описание |
|----------|-----|--------------|----------|
| type | string | Да | Тип уведомления (например, `article`, `message`) |
| item_id | int | Да | Идентификатор связанной сущности |
| full | bool | Нет | Если `true`, подгружает дополнительную информацию о связанной сущности |
| user_id | int | Нет | (только для admin) ID пользователя, которому принадлежит уведомление |

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Notification retrieved",
	"data": {
		"id": 1,
		"user_id": 42,
		"type": "article",
		"item_id": 5,
		"title": "Новая статья опубликована",
		"body": "Опубликована статья 'Как работать с API'",
		"is_read": 0,
		"dt_ins": "2025-03-20 10:00:00"
	}
}
```
При `full=true` в ответе добавляется поле `entity` (как в методе `getAll`).

---

## `markAsRead`
### Доступ: `user`

**POST** `/api/v1/notifications/markAsRead/{id}`

### Описание:
Отметить уведомление как прочитанное. Администратор может указать `user_id` для отметки уведомления другого пользователя.

### Параметры пути (URL):
| Параметр | Тип | Описание |
|----------|-----|----------|
| id | int | ID уведомления |

### Параметры запроса (query) (опционально):
| Параметр | Тип | Описание |
|----------|-----|----------|
| user_id | int | (только для admin) ID пользователя, которому принадлежит уведомление |

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Notification marked as read",
	"data": []
}
```

---

# 📄 Articles

## `test`
### Доступ: `public`

**GET** `/api/v1/articles/test`

### Описание:
Тестовый метод для проверки работоспособности модуля статей.

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Article module works"
}
```

---

## `getPublished` (default)
### Доступ: `user`

**GET** `/api/v1/articles/` или `/api/v1/articles/getPublished`

### Описание:
Получить список опубликованных статей с пагинацией. Доступен всем авторизованным пользователям.

### Параметры запроса (query):
| Параметр | Тип | Описание |
|----------|-----|----------|
| page | int | Номер страницы (по умолчанию 1) |
| per_page | int | Количество элементов на странице (по умолчанию 20) |
| since_date | string | Дата в формате `Y-m-d H:i:s`. Если указана, возвращаются статьи, опубликованные после этой даты |

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Published articles retrieved",
	"data": [
		{
			"id": 1,
			"title": "Как работать с API",
			"description": "Подробное руководство по работе с API",
			"content": "<p>Содержание статьи...</p>",
			"image": "https://example.com/image.jpg",
			"category": "news",
			"author_id": 42,
			"status": "published",
			"dt_ins": "2025-03-15 12:00:00",
			"dt_published": "2025-03-15 12:00:00"
		}
	],
	"paginator": {
		"total_items": 10,
		"total_pages": 1,
		"current_page": 1,
		"per_page": 20
	}
}
```

---

## `getAll`
### Доступ: `admin`

**GET** `/api/v1/articles/getAll`

### Описание:
Получить список статей (всех статусов) с возможностью фильтрации. Доступен только администраторам.

### Параметры запроса (query):
| Параметр | Тип | Описание |
|----------|-----|----------|
| page | int | Номер страницы (по умолчанию 1) |
| per_page | int | Количество элементов на странице (по умолчанию 20) |
| status | string | Фильтр по статусу (`draft`, `published`, `archived`) |
| author_id | int | Фильтр по ID автора |

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Articles retrieved",
	"data": [
		{
			"id": 1,
			"title": "Как работать с API",
			"description": "Подробное руководство",
			"content": "<p>Содержание...</p>",
			"image": "https://example.com/image.jpg",
			"category": "news",
			"author_id": 42,
			"status": "published",
			"dt_ins": "2025-03-15 12:00:00",
			"dt_published": "2025-03-15 12:00:00"
		},
		{
			"id": 2,
			"title": "Черновик",
			"description": "Статья в работе",
			"content": "<p>Незаконченная статья</p>",
			"status": "draft",
			"dt_ins": "2025-03-16 09:00:00"
		}
	],
	"paginator": {
		"total_items": 15,
		"total_pages": 1,
		"current_page": 1,
		"per_page": 20
	}
}
```

---

## `addArticle`
### Доступ: `admin`

**POST** `/api/v1/articles/addArticle`

### Описание:
Создать новую статью (черновик). Доступно только администраторам.

### Тело запроса (JSON):
```json
{
	"title": "Заголовок статьи",
	"description": "Краткое описание",
	"content": "<p>Полный текст статьи в HTML</p>",
	"image": "https://example.com/cover.jpg",
	"category": "news",
	"publish": false
}
```
| Поле | Тип | Обязательное | Описание |
|------|-----|--------------|----------|
| title | string | Да | Заголовок статьи |
| content | string | Да | HTML-содержимое статьи |
| description | string | Нет | Краткое описание (аннотация) |
| image | string | Нет | URL обложки |
| category | string | Нет | Категория (по умолчанию `news`) |
| publish | bool | Нет | Опубликовать сразу после создания (по умолчанию `false`) |

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Article added successfully",
	"data": {
		"id": 3
	}
}
```

---

## `editArticle`
### Доступ: `admin`

**PUT** `/api/v1/articles/editArticle/{id}`

### Описание:
Редактировать существующую статью. Доступно только администраторам или автору статьи.

### Параметры пути (URL):
| Параметр | Тип | Описание |
|----------|-----|----------|
| id | int | ID статьи |

### Тело запроса (JSON):
```json
{
	"title": "Новый заголовок",
	"description": "Обновлённое описание",
	"content": "<p>Новый текст статьи</p>",
	"image": "https://example.com/new_cover.jpg",
	"category": "tutorial",
	"publish": true,
	"status": "archived"
}
```
Все поля необязательны. Если передано `publish: true`, статья будет опубликована. Если `status: "archived"` – переведена в архив.

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Article updated successfully",
	"data": []
}
```

---

## `getById`
### Доступ: `admin`

**GET** `/api/v1/articles/getById/{id}`

### Описание:
Получить статью по ID. Доступно администраторам. (Обычным пользователям доступна только через `getPublished`.)

### Параметры пути (URL):
| Параметр | Тип | Описание |
|----------|-----|----------|
| id | int | ID статьи |

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Article retrieved",
	"data": {
		"id": 1,
		"title": "Как работать с API",
		"description": "Подробное руководство",
		"content": "<p>Содержание статьи...</p>",
		"image": "https://example.com/image.jpg",
		"category": "news",
		"author_id": 42,
		"status": "published",
		"dt_ins": "2025-03-15 12:00:00",
		"dt_published": "2025-03-15 12:00:00"
	}
}
```
- **404 Not Found** – если статья не найдена.
- **403 Forbidden** – если статья не опубликована и текущий пользователь не является её автором и не администратор.

---

## `getNotPublished`
### Доступ: `admin` (несмотря на указание `user` в конфигурации)

**GET** `/api/v1/articles/getNotPublished`

### Описание:
Получить список неопубликованных статей (статус `draft`). В текущей реализации метод доступен только администраторам, так как контроллер проверяет `isAdmin`.

### Параметры запроса (query):
| Параметр | Тип | Описание |
|----------|-----|----------|
| page | int | Номер страницы (по умолчанию 1) |
| per_page | int | Количество элементов на странице (по умолчанию 20) |

### Ответ:
- **200 OK**
```json
{
	"ok": true,
	"message": "Unpublished articles retrieved",
	"data": [
		{
			"id": 2,
			"title": "Черновик",
			"description": "Статья в работе",
			"content": "<p>Незаконченная статья</p>",
			"status": "draft",
			"dt_ins": "2025-03-16 09:00:00"
		}
	],
	"paginator": {
		"total_items": 3,
		"total_pages": 1,
		"current_page": 1,
		"per_page": 20
	}
}
```
> **Примечание:** Несмотря на указанный в конфигурации доступ `user`, в коде контроллера присутствует проверка `$this->isAdmin`. В текущей версии метод доступен только администраторам.

