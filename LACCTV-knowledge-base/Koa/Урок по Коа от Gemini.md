Koa.js — это новый веб-фреймворк, разработанный командой, создавшей Express. Он стремится быть **меньшей, более выразительной и более надежной основой** для веб-приложений и API. Используя асинхронные функции (async functions), Koa позволяет отказаться от колбэков и значительно улучшить обработку ошибок. Koa не поставляется со встроенным middleware в своем ядре.

**Минимальное Koa-приложение (Hello World)**

Вот пример простейшего Koa-приложения, которое отвечает "Hello World" на любой запрос:

```javascript
const Koa = require('koa'); // Подключаем библиотеку Koa
const app = new Koa(); // Инициализируем новое Koa-приложение

// Middleware, который будет выполняться при каждом запросе
// ctx (Context) - это объект контекста запроса/ответа
app.use(async ctx => { // Добавляем middleware к приложению
  ctx.body = 'Hello World'; // Устанавливаем тело ответа
});

app.listen(3000); // Запускаем HTTP-сервер на порту 3000

// Можно добавить колбэк, который выполнится после запуска сервера
// app.listen(3000, () => { console.log('Server started'); });
```

Этот код подключает Koa, создает экземпляр приложения, добавляет middleware с помощью `app.use()`, который устанавливает тело ответа `ctx.body`, и запускает сервер, прослушивая порт 3000 с помощью `app.listen()`. `app.listen()` является синтаксическим сахаром для создания HTTP-сервера с использованием `http.createServer(app.callback()).listen(...)`. Метод `app.callback()` возвращает функцию, подходящую для `http.createServer()`.

**Middleware и Каскадирование**

Приложение Koa представляет собой объект, содержащий массив функций middleware, которые **компоновываются и выполняются в стековом порядке** при поступлении запроса. Koa отличается от некоторых других систем middleware (например, Connect) **каскадным выполнением**. Middleware в Koa "спускаются" (downstream), вызывая `await next()`, а затем управление "поднимается" обратно (upstream) после выполнения всех последующих middleware.

Пример с каскадным middleware для логирования и добавления заголовка времени ответа:

```javascript
const Koa = require('koa');
const app = new Koa();

// Middleware для логирования (выполняется "upstream")
app.use(async (ctx, next) => {
  await next(); // Ждем выполнения следующего middleware в стеке
  const rt = ctx.response.get('X-Response-Time'); // Получаем установленный заголовок
  console.log(`${ctx.method} ${ctx.url} - ${rt}`); // Выводим информацию в консоль
});

// Middleware для добавления заголовка времени ответа (выполняется "upstream")
app.use(async (ctx, next) => {
  const start = Date.now(); // Запоминаем время начала запроса
  await next(); // Ждем выполнения следующего middleware
  const ms = Date.now() - start; // Вычисляем время выполнения
  ctx.set('X-Response-Time', `${ms}ms`); // Устанавливаем заголовок X-Response-Time
});

// Middleware для ответа (выполняется первым в "downstream")
app.use(async ctx => {
  ctx.body = 'Hello World'; // Устанавливаем тело ответа
});

app.listen(3000);
```

В этом примере, когда приходит запрос, сначала выполняется первый middleware (логирование), он вызывает `await next()`. Затем выполняется второй middleware (время ответа), он тоже вызывает `await next()`. Затем выполняется третий middleware (ответ), он устанавливает `ctx.body`. После этого управление возвращается обратно: сначала завершается второй middleware, устанавливая заголовок `X-Response-Time`, а затем завершается первый middleware, выводя сообщение в консоль.

**Объект Context (ctx)**

Объект **Context (ctx)** инкапсулирует объекты `request` и `response` Node.js в единый объект. Он предоставляет множество полезных методов и аксессоров для разработки веб-приложений и API. **Контекст создается для каждого запроса** и передается как аргумент в middleware. Многие аксессоры контекста просто делегируют вызовы соответствующим свойствам объектов `ctx.request` или `ctx.response` для удобства.

Примеры доступа к свойствам контекста:

```javascript
app.use(async ctx => {
  console.log(ctx.method); // Метод HTTP запроса (GET, POST и т.д.)
  console.log(ctx.url); // Полный URL запроса
  console.log(ctx.path); // Путь запроса (без строки запроса)
  console.log(ctx.status); // Статус ответа - по умолчанию 404
  console.log(ctx.body); // Тело ответа

  // Установка свойств ответа
  ctx.status = 200; // Устанавливаем статус ответа
  ctx.body = 'Response body'; // Устанавливаем тело ответа
  ctx.set('Content-Type', 'text/plain'); // Устанавливаем заголовок ответа
});
```

Объект `ctx.state` является рекомендуемым пространством имен для передачи информации через middleware и в представления фронтенда.

**Обработка JSON**

Вы можете передавать JSON напрямую, устанавливая `ctx.body` в JavaScript-объект или массив. Koa автоматически сериализует их в JSON. Тип контента (`Content-Type`) по умолчанию будет установлен как `application/json`.

Пример возврата JSON:

```javascript
app.use(async ctx => {
  // Установка объекта в ctx.body автоматически отправит его как JSON
  ctx.body = { msg: 'Hello World' };
  // Koa автоматически установит Content-Type: application/json
});
```

Для более красивого форматирования JSON в ответе можно использовать стороннюю библиотеку `koa-json`.

Пример использования `koa-json`:

```javascript
const Koa = require('koa');
const json = require('koa-json'); // Подключаем модуль для работы с JSON

const app = new Koa();

app.use(json()); // Включаем обработку JSON с помощью middleware

app.use(async ctx => {
  // Установка объекта по-прежнему работает, но koa-json может улучшить форматирование
  ctx.body = { msg: 'Hello World' };
});

app.listen(3010, () => {
  console.log('Server running on http://localhost:3010'); // Сообщение о запуске сервера
});
```

**Маршрутизация (с помощью `koa-router`)**

Koa не включает встроенную маршрутизацию. Для определения маршрутов обычно используются сторонние middleware, такие как `koa-router`.

Пример установки и использования `koa-router`:

Сначала установите его: `npm install koa-router`.

Затем используйте в коде:

```javascript
const Koa = require('koa');
const Router = require('koa-router'); // Подключаем koa-router

const app = new Koa();
const router = new Router(); // Инициализируем новый экземпляр Router

// Определение маршрута GET /test
router.get('/test', async ctx => { // Определяем GET-маршрут '/test'
  ctx.body = 'Привет, тест!'; // Устанавливаем тело ответа для этого маршрута
});

// Подключение middleware маршрутизатора к приложению Koa
app.use(router.routes()); // Добавляем middleware для обработки маршрутов
app.use(router.allowedMethods()); // Добавляем middleware для обработки разрешенных методов

app.listen(3000);
```

**Получение параметров URL**

С помощью `koa-router` вы можете получать параметры из URL, определенные в маршруте (например, `/test/:name`), через объект `ctx.params`.

Пример получения параметра из URL:

```javascript
const Koa = require('koa');
const Router = require('koa-router');

const app = new Koa();
const router = new Router();

// Определение маршрута с параметром ":name"
router.get('/hello/:name', async ctx => {
  const name = ctx.params.name; // Получаем значение параметра "name" из ctx.params
  ctx.body = `Привет, ${name}!`; // Используем параметр в ответе
});

app.use(router.routes());
app.use(router.allowedMethods());

app.listen(3000);
```

При обращении к `/hello/Harry`, ответ будет "Привет, Harry!".

**Добавление свойств в Context**

Вы можете добавлять дополнительные свойства или методы в объект `ctx` для использования во всем приложении, редактируя прототип `app.context`. Это может быть полезно для добавления ссылок на базу данных или других общих ресурсов.

Пример добавления ссылки на базу данных в контекст:

```javascript
const Koa = require('koa');
const app = new Koa();

// Допустим, у вас есть функция db(), возвращающая объект базы данных
// const db = () => ({ find: async (query) => `Finding: ${query}` });

// Добавляем свойство 'db' в прототип контекста
app.context.db = {
  find: async (query) => `Finding: ${query}` // Пример имитации метода find
};

app.use(async ctx => {
  // Теперь вы можете получить доступ к ctx.db в любом middleware
  const result = await ctx.db.find('something');
  ctx.body = `Database query result: ${result}`;
});

app.listen(3000);
```

В Koa v3 появилась возможность использовать `app.currentContext` с AsyncLocalStorage для доступа к контексту текущего запроса извне middleware, что полезно для передачи деталей запроса (например, ID запроса или пользователя) во внутренние сервисы.

**Обработка ошибок**

По умолчанию Koa выводит все ошибки в stderr, если только `app.silent` не равен `true`. Koa также не выводит ошибки, если `err.status` равно 404 или `err.expose` равно `true`. Для централизованного логирования или другой пользовательской обработки ошибок вы можете добавить слушатель события `"error"` на экземпляр приложения.

Пример обработки ошибок:

```javascript
const Koa = require('koa');
const app = new Koa();

// Добавляем слушатель события 'error'
app.on('error', (err, ctx) => { // Колбэк получает ошибку и опционально контекст
  console.error('Server error:', err); // Логируем ошибку
  // Если возможно ответить клиенту, Koa отправит 500 Internal Server Error
  // Если нет (например, данные уже были записаны в сокет), только логируется
});

app.use(async ctx => {
  // Пример, как вызвать ошибку, которая будет поймана слушателем 'error'
  // throw new Error('Something went wrong!');

  // Или использовать ctx.throw для удобства, который также эмитирует 'error' и устанавливает статус
  // ctx.throw(500, 'Внутренняя ошибка сервера');
  ctx.body = 'Hello Koa Error Handling!';
});

app.listen(3000);
```

В случае ошибки во время цикла запрос/ответ, когда еще возможно ответить клиенту (т.е. данные не были записаны в сокет), Koa автоматически отвечает с статусом 500 "Internal Server Error".

**Объекты Request и Response**

Объекты **`ctx.request`** и **`ctx.response`** в Koa являются абстракциями над нативными объектами `request` и `response` Node.js. Они предоставляют дополнительную функциональность, полезную для повседневной разработки HTTP-серверов. Многие свойства доступны прямо на `ctx` как удобные алиасы, делегирующие вызовы соответствующим объектам `request` или `response`.

Примеры использования объектов Request и Response:

```javascript
app.use(async ctx => {
  // Доступ к объекту Koa Request
  console.log(ctx.request.method); // Метод запроса
  console.log(ctx.request.url); // URL запроса
  console.log(ctx.request.query); // Распарсенная строка запроса
  console.log(ctx.request.ip); // IP адрес клиента
  console.log(ctx.request.is('json')); // Проверка типа контента запроса

  // Доступ к объекту Koa Response
  ctx.response.status = 201; // Установка статуса ответа
  ctx.response.body = { success: true }; // Установка тела ответа
  ctx.response.type = 'application/json'; // Установка типа контента ответа
  ctx.response.set('X-Custom-Header', 'value'); // Установка заголовка ответа
  ctx.response.redirect('/somewhere-else'); // Перенаправление
});
```

Важно отметить, что Koa не рекомендует и **не поддерживает** прямое использование нативных объектов `ctx.req` и `ctx.res` Node.js для управления ответом (например, `res.statusCode`, `res.writeHead()`, `res.write()`, `res.end()`), поскольку это может нарушить функциональность middleware и самой Koa. Для обхода встроенной обработки ответа Koa можно явно установить `ctx.respond = false`, но это считается "хаком".
