### Минимальный koa-server
```javascript
const Koa = require("koa")
const log = console.log //чтобы не писать console.log каждый раз
const app = new Koa() //подключение к фреймворку

app.use(async (ctx) => (ctx.body = "Hello World")) //middleware, который отвечает за обработку запросов

app.listen(3010, () => {
  log("Server running...")
}) //запуск сервера
```

Можно передать JSON прямо на view без библиотек
```javascript
app.use(async (ctx) => (ctx.body = { msg: "Hello World" })) //в таком виде от мы отдаем объект клиенту в формате JSON
```

А можно подключить специальную библиотеку
```javascript
const json = require("koa-json") //подключаем модуль для работы с JSON

const app = new Koa() //подключение к фреймворку

app.use(json()) //включаем обработку JSON

//middleware, который отвечает за обработку запросов

app.use(async (ctx) => (ctx.body = { msg: "Hello World" })) //в таком виде от мы отдаем объект клиенту в формате JSON

app.listen(3010, () => {

  log("Server running on http://localhost:3010")

}) //запуск сервера
```

Установим koa-ejs для рендера страницы
Добавим в наш код
```json
//импорты
const path = require("path") //подключаем модуль для работы с путями
const render = require("koa-ejs") //подключаем модуль для работы с шаблонами

//настройка
render(app, {
  root: path.join(__dirname, "views"), //указываем путь к папке с шаблонами
  layout: "layout", //указываем имя файла шаблона
  viewExt: "html", //указываем расширение файлов шаблонов
  cache: false, //отключаем кэширование шаблонов
  debug: false, //включаем режим отладки
})

//Index page
router.get("/", async (ctx) => {
  await ctx.render("index", { title: "Welcome to Koa" }) //рендерим шаблон index
  log("GET request to /") //логируем запрос
})
```
И создадим файл layout.html и index.html в папке views

layout.html (как App.jsx в React или layout.tsx в Next.js):
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
   href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/css/bootstrap.min.css"
     rel="stylesheet"
      integrity="sha384-4Q6Gf2aSP4eDXB8Miphtr37CMZZQ5oXLH2yaXMJ2w8e2ZtHTl7GptT4jmndRuHDT"
      crossorigin="anonymous"
    />
    <!-- Воспользуемся bootstrap -->
    <title>Things app</title>
  </head>
  <body>
    <div class="container">
    <!-- Синтаксис шаблонов EJS: -->
    <%- body %>
    </div>  
    <script
src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.6/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-j1CDi7MgGQ12Z7Qab0qlWQ/Qqz24Gc6BM0thvEMVjHnfYGF0rmFCozFSxQBxwHKO"
      crossorigin="anonymous"
    ></script>
    <!-- Воспользуемся bootstrap -->
  </body>

</html>
```

index.html
```html
<h1>Things I love</h1>
```

Теперь сделаем navbar. Скопируем с Bootstrap navbar в файл partials/_navbar.html

```html
<nav class="navbar navbar-expand-lg bg-body-tertiary mb-4">

  <div class="container-fluid">

    <a class="navbar-brand" href="/">Things</a>

    <button

      class="navbar-toggler"

      type="button"

      data-bs-toggle="collapse"

      data-bs-target="#navbarNavDropdown"

      aria-controls="navbarNavDropdown"

      aria-expanded="false"

      aria-label="Toggle navigation"

    >

      <span class="navbar-toggler-icon"></span>

    </button>

    <div class="collapse navbar-collapse" id="navbarNavDropdown">

      <ul class="navbar-nav ml-auto">

        <li class="nav-item">

          <a class="nav-link active" aria-current="page" href="#">Home</a>

        </li>

        <li class="nav-item">

          <a class="nav-link" href="/add">Add something</a>

        </li>

      </ul>

    </div>

  </div>

</nav>
```

После чего добавим этот элемент в наш основной layout
```html
<% include partials/_navbar %>
    <!-- Подключим navbar из partials/_navbar.ejs -->
```
