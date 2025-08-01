[Ссылка на обучающее видео по REST API](https://youtu.be/6npSvyo9KAY?si=Rq093CXHstwBSbY8)
#### 1. **Что такое REST API?**
REST API (Representational State Transfer) — это интерфейс для взаимодействия между клиентом и сервером через HTTP-запросы. Он используется для создания, чтения, обновления и удаления данных (CRUD).

#### 2. **Модель зрелости Ричардсона**
Модель описывает 4 уровня зрелости REST API:
- **Уровень 0 (Болото)**: Все запросы отправляются на один URL, действия передаются в теле запроса. Не рекомендуется.
- **Уровень 1 (Ресурсы)**: Каждая сущность имеет свой URL, но методы HTTP не используются.
- **Уровень 2 (HTTP методы)**: Используются HTTP-методы (GET, POST, PUT, DELETE) для работы с ресурсами. Самый распространённый уровень.
- **Уровень 3 (Гипермедиа)**: В ответе возвращаются ссылки на доступные действия (например, ссылки для обновления или удаления ресурса).

#### 3. **Версионирование API**
Для поддержки обратной совместимости API версионируют через префикс в URL:
```plaintext
GET /v1/users  // Версия 1
GET /v2/users  // Версия 2 с другим форматом ответа
```

#### 4. **Модификаторы доступа**
Разделение API на публичные и приватные части:
```plaintext
GET /v1/users          // Публичный доступ
GET /v1/private/users  // Приватный доступ (требует авторизации)
GET /v1/admin/users    // Доступ только для администраторов
```

#### 5. **Проектирование API: CRUD и сущности**
Пример для сущности **User**:
```plaintext
// User
GET /users           // Получить всех пользователей
GET /users/{id}      // Получить пользователя по ID
GET /users/me        // Получить данные текущего пользователя
POST /users          // Создать пользователя
PUT /users/{id}      // Обновить пользователя
DELETE /users/{id}   // Удалить пользователя
```

Пример для сущности **Post**:
```plaintext
// Post
GET /posts           // Получить все посты
GET /posts/{id}      // Получить пост по ID
GET /posts/{alias}   // Получить пост по URL (алиасу)
POST /posts          // Создать пост
PUT /posts/{id}      // Обновить пост
DELETE /posts/{id}   // Удалить пост
```

Пример для сущности **Comment** (вложенной в Post):
```plaintext
// Comment
GET /posts/{id}/comments          // Получить комментарии поста
POST /posts/{id}/comments         // Создать комментарий
PUT /posts/{id}/comments/{id}     // Обновить комментарий
DELETE /posts/{id}/comments/{id}  // Удалить комментарий
```

#### 6. **Вложенные сущности**
Если сущности связаны (например, комментарии относятся к посту), их URL вкладывают друг в друга:
```plaintext
GET /users/{id}/posts     // Получить посты пользователя
GET /users/{id}/comments  // Получить комментарии пользователя
```

#### 7. **Примеры изображений**
1. **Структура API**:
   ![Пример структуры API](image.png)
   - Показаны основные endpoints для User, Post и Comment.

2. **Пример версионирования и модификаторов доступа**:
   ![Версионирование и доступ](image.png)
   - Примеры URL с версиями (`v1`, `v2`) и модификаторами (`private`, `admin`).

3. **CRUD для сущностей**:
   ![CRUD для User, Post, Comment](image.png)
   - Описаны базовые операции для каждой сущности.

#### 8. **Итоговые рекомендации**
- Используйте **уровень 2** модели Ричардсона (HTTP-методы).
- Версионируйте API для обратной совместимости.
- Разделяйте доступ через префиксы (`public`, `private`, `admin`).
- Соблюдайте единообразие в наименовании endpoints.
- Вкладывайте сущности, если они логически связаны (например, `posts/{id}/comments`).

