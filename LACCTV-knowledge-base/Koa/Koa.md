# [Конспект урока](https://youtu.be/z84uTk5zmak?si=_dmWI42ddRb11Rr0) по [Koa.js](https://koajs.com)

## Минимальный Koa-сервер

```javascript
const Koa = require("koa")
const log = console.log // Сокращение для console.log
const app = new Koa() // Инициализация приложения

// Middleware для обработки запросов
app.use(async (ctx) => (ctx.body = "Hello World"))

// Запуск сервера
app.listen(3010, () => {
  log("Server running...")
})
```

## Работа с JSON

### Без библиотек
```javascript
app.use(async (ctx) => (ctx.body = { msg: "Hello World" }))
```

### С библиотекой koa-json
```javascript
const json = require("koa-json")

app.use(json()) // Включаем обработку JSON

app.use(async (ctx) => (ctx.body = { msg: "Hello World" }))

app.listen(3010, () => {
  log("Server running on http://localhost:3010")
})
```

## Настройка шаблонов с koa-ejs

### Конфигурация
```javascript
const path = require("path")
const render = require("koa-ejs")

// Настройка шаблонизатора
render(app, {
  root: path.join(__dirname, "views"), // Папка с шаблонами
  layout: "layout",                   // Основной layout
  viewExt: "html",                    // Расширение файлов
  cache: false,                       // Отключение кеширования
  debug: false                        // Режим отладки
})
```

### Пример роута
```javascript
router.get("/", async (ctx) => {
  await ctx.render("index", { title: "Welcome to Koa" })
  log("GET request to /")
})
```

## Структура шаблонов

### `layout.html` (основной макет)
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/css/bootstrap.min.css" rel="stylesheet" />
  <title>Things app</title>
</head>
<body>
  <div class="container">
    <% include partials/_navbar %>
    <%- body %>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

### `index.html`
```html
<h1><%- title %></h1>
<ul class="list-group">
  <% things.forEach(thing => { %>
    <li class="list-group-item"><%= thing %></li>
  <% }) %>
</ul>
```

### `partials/_navbar.html`
```html
<nav class="navbar navbar-expand-lg bg-body-tertiary mb-4">
  <div class="container-fluid">
    <a class="navbar-brand" href="/">Things</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavDropdown">
      <ul class="navbar-nav ml-auto">
        <li class="nav-item">
          <a class="nav-link active" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/add">Add something</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

## Работа с данными

```javascript
// Временное хранилище (в реальном проекте используйте БД)
const thingsILove = ["Coding", "Coffee", "Music", "Nature", "Traveling"]

// Обработчик главной страницы
async function index(ctx) {
  await ctx.render("index", { 
    title: "Things I Love", 
    things: thingsILove 
  })
  log("GET request to /")
}
```

## Обработка форм

### `add.html`
```html
<h1 class="display-mb-4">Add a Thing</h1>
<form action="/add" method="POST">
  <div class="form-group">
    <input
      type="text"
      name="thing"
      class="form-control form-control-lg"
      placeholder="Enter a thing you love"
    />
    <input type="submit" value="Add" class="btn btn-dark btn-lg mt-3" />
    <a href="/" class="btn btn-danger btn-lg mt-3">Cancel</a>
  </div>
</form>
```

### Обработчик POST-запроса
```javascript
const bodyParser = require("koa-bodyparser")
app.use(bodyParser()) // Подключаем middleware для парсинга тела запроса

router.post("/add", addThing)

async function addThing(ctx) {
  const body = ctx.request.body
  thingsILove.push(body.thing) // Добавляем новый элемент
  ctx.redirect("/") // Перенаправляем на главную
}
```

## Расширение контекста

```javascript
// Добавляем свойства в контекст приложения
app.context.user = 'Guest'

// Пример использования
router.get("/test", (ctx) => (ctx.body = `Hi ${ctx.user}`))
```

## Обработка параметров маршрута

```javascript
router.get("/test2/:name", (ctx) => (ctx.body = `Hi ${ctx.params.name}`))
```
