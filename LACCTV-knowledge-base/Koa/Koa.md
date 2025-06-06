### Минимум koa-server
```javascript
const Koa = require("koa")
const log = console.log //чтобы не писать console.log каждый раз
const app = new Koa() //подключение к фреймворку

app.use(async (ctx) => (ctx.body = "Hello World")) //middleware, который отвечает за обработку запросов

app.listen(3010, () => {
  log("Server running...")
}) //запуск сервера
```

