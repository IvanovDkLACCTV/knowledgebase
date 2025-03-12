**Основные команды и их использование:**

![[Pasted image 20250312161038.png]]

Ниже представлены основные методы Socket.IO с примерами использования:

- **`io.on('connection', (socket) => { ... });`**: Устанавливает обработчик для нового подключения клиента.
```javascript
  const io = require('socket.io')(3000);

  io.on('connection', (socket) => {
    console.log('Новое подключение');
  });
```

**`socket.emit('event_name', data);`**: Отправляет событие с данными конкретному клиенту.
```javascript
  socket.emit('message', 'Привет, клиент!');
```

**`socket.on('event_name', (data) => { ... });`**: Устанавливает обработчик для получения определенного события от клиента.
```javascript
  socket.on('message', (msg) => {
    console.log('Сообщение от клиента:', msg);
  });
```

**`socket.broadcast.emit('event_name', data);`**: Отправляет событие всем клиентам, кроме текущего.
```javascript
  socket.broadcast.emit('message', 'Сообщение для всех, кроме отправителя');
```

**`socket.join('room_name');`**: Добавляет клиента в определенную комнату.
```javascript
  socket.join('комната1');
```

**`socket.leave('room_name');`**: Удаляет клиента из определенной комнаты.

```javascript
  socket.leave('комната1');
```

**`io.to('room_name').emit('event_name', data);`**: Отправляет событие всем клиентам в указанной комнате.
```javascript
  io.to('комната1').emit('message', 'Сообщение для всех в комнате1');
```
