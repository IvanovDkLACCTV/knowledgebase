**Основные команды и их использование:**

![[Pasted image 20250312161038.png]]
#### **Основные методы и события**

1. **`io.emit(event, data)`**  
    Отправляет событие `event` с данными `data` **всем подключенным клиентам**.
    
2. **`socket.emit(event, data)`**  
    Отправляет событие `event` с данными `data` **только текущему клиенту** (от сервера к клиенту или наоборот).
    
3. **`io.on(event, callback)`**  
    Обрабатывает события на уровне сервера (например, новое подключение).  
    Пример: `io.on('connection', (socket) => { ... })`.
    
4. **`socket.on(event, callback)`**  
    Обрабатывает события от **конкретного клиента**.  
    Пример: `socket.on('message', (data) => { ... })`.
    
5. **`io.to(room)`**  
    Фильтр для отправки сообщений клиентам в определенной **комнате**.  
    Пример: `io.to('room1').emit('event', data)`.
    
6. **`socket.join(room)`**  
    Подключает клиента к комнате `room`.  
    Пример: `socket.join('room1')`.
    
7. **`socket.leave(room)`**  
    Отключает клиента от комнаты `room`.  
    Пример: `socket.leave('room1')`.
    
8. **`.broadcast`**
    
    - `socket.broadcast.emit(event, data)` — отправляет событие **всем, кроме текущего клиента**.
        
    - `socket.broadcast.to('room').emit(event, data)` — отправляет событие всем в комнате `room`, кроме текущего клиента.

---
#### **Работа с JSON**

- **Отправить JSON на клиент** (сервер → клиент):
```javascript
// Сервер
socket.emit('event', { key: 'value' }); // Socket.IO автоматически сериализует объект в JSON.
```
- **Получить JSON с клиента** (клиент → сервер):
```javascript
// Сервер
socket.on('event', (data) => {
  console.log(data); // Объект автоматически парсится из JSON.
});
```
- **Отправить JSON на сервер** (клиент → сервер):
```javascript
// Клиент
socket.emit('event', { key: 'value' });
```
- **Получить JSON с сервера** (сервер → клиент):
```javascript
// Клиент
socket.on('event', (data) => {
  console.log(data); // Автоматический парсинг.
});
```
---
#### **Создание сервера**

```javascript
const http = require('http');
const { Server } = require('socket.io');

const server = http.createServer();
const io = new Server(server);

io.on('connection', (socket) => {
  console.log('Клиент подключен');
  
  socket.on('disconnect', () => {
    console.log('Клиент отключен');
  });
});

server.listen(3000, () => {
  console.log('Сервер запущен на порту 3000');
});
```
---
#### **Создание клиента**
```html
<script src="/socket.io/socket.io.js"></script>
<script>
  const socket = io('http://localhost:3000'); // Подключение к серверу
  
  socket.on('connect', () => {
    console.log('Подключено к серверу');
  });
</script>
```
---

#### **Комнаты (Rooms)**
```javascript
// Сервер: подключение клиента к комнате
socket.join('room1');

// Отправить сообщение всем в комнате 'room1'
io.to('room1').emit('room-message', 'Привет, комната!');

// Покинуть комнату
socket.leave('room1');
```
---
#### State Recovery
Это опция для восстановления состояния соединения после неожиданного разрыва (например, при потере интернета). Она позволяет:

- Сохранить буфер отправленных сообщений.
    
- Восстановить идентификатор сессии (`sessionID`) и данные аутентификации (`auth`).
    
- Продолжить работу с того же места после переподключения.

#### **Как включить?**

**На сервере** (при создании экземпляра `Server`):
```javascript
const io = new Server(httpServer, {
  connectionStateRecovery: {
    maxDisconnectionDuration: 2 * 60 * 1000, // Макс. время восстановления (2 мин)
    skipMiddlewares: true, // Пропустить middleware при восстановлении
  }
});
```
**На клиенте** (при подключении):
```javascript
const socket = io({
  reconnection: true, // Включить повторное подключение
  reconnectionAttempts: 5, // Макс. попыток
  connectionStateRecovery: {}, // Включить восстановление состояния
});
```
----
#### **Ключевые параметры**

- **`maxDisconnectionDuration`**  
    Время (в мс), в течение которого сервер хранит данные сессии после разрыва.  
    _По умолчанию: 2 минуты._
    
- **`skipMiddlewares`**  
    Если `true`, middleware (например, аутентификация) не выполняется при восстановлении сессии.  
    _По умолчанию: `false`.

#### **Как работает?**

1. При первом подключении сервер генерирует уникальный **`sessionID`** и отправляет его клиенту.
    
2. Клиент сохраняет `sessionID` и `auth`-данные (например, токен) в `localStorage`.
    
3. При разрыве соединения клиент пытается переподключиться, отправляя `sessionID`.
    
4. Если сервер находит сессию в своем хранилище, состояние восстанавливается.

#### **Пример использования**

**Сервер:**
```javascript
io.on("connection", (socket) => {
  console.log("Сессия:", socket.sessionID); // Уникальный ID сессии
  console.log("Данные аутентификации:", socket.auth); // { token: "..." }

  socket.on("message", (data) => {
    // Сообщение будет сохранено в буфере, если соединение прервется
    socket.emit("response", "Данные получены");
  });
});
```
**Клиент:**
```javascript
socket.auth = { token: "secret" }; // Данные для восстановления
socket.connect();

// События восстановления
socket.on("reconnect_attempt", (attempt) => {
  console.log(`Попытка ${attempt}...`);
});

socket.on("reconnect", (attempt) => {
  console.log("Соединение восстановлено!");
});
```
---

#### **Кластеры**

Для работы с кластерами в Node.js используйте адаптер (например, Redis):

1. Установите пакет: `npm install @socket.io/cluster-adapter`.
    
2. Настройте сервер:
```javascript
import { createAdapter, setupPrimary } from '@socket.io/cluster-adapter';
const { Server } = require('socket.io');

const io = new Server(server, {
	connectionStateRecovery: {},
	adapter: createAdapter()
});
```
---
#### **Закрытие соединения**

- **Сервер**:
```javascript
socket.disconnect(); // Отключить конкретного клиента.
```
- **Клиент**:
```javascript
socket.close(); // Закрыть соединение.
```

---
#### **Пример передачи данных**

**Сервер**:
```javascript
io.on('connection', (socket) => {
  socket.emit('server-msg', { message: 'Добро пожаловать!' });
  
  socket.on('client-msg', (data) => {
    console.log('Получено от клиента:', data);
  });
});
```

**Клиент**:
```javascript
socket.on('server-msg', (data) => {
  console.log('Сервер говорит:', data);
});

socket.emit('client-msg', { text: 'Привет, сервер!' });
```