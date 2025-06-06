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