Ещё один пример особенности работы асинхронных функций в JavaScript.
Давайте разберем этот код пошагово:

```javascript:example.js
async function delay(ms) {
    return new Promise(r => setTimeout(r, ms));
}

async function short() {
    await delay(500);
    throw new Error('short() throwed');
}

async function long() {
    await delay(1000);
    return 'long() result';
}

async function start() {
    try {
        let promise1 = short();
        let promise2 = long();
        console.log(await promise2);
        console.log(await promise1);
        console.log('success');
    } catch (e) {
        console.error('CATCH ERROR');
    }
}

start().then(() => console.log('test done'));
```

**Вывод:**
```
long() result
CATCH ERROR
test done
```

**Объяснение:**

1. **Запуск промисов**: `promise1` и `promise2` запускаются одновременно (параллельно), но не ожидаются сразу
   - `promise1` (short) завершится через 500ms с ошибкой
   - `promise2` (long) завершится через 1000ms с результатом

2. **Первый await**: `await promise2` ждет завершения `long()` функции (1000ms)
   - К этому моменту `short()` уже завершилась с ошибкой (через 500ms), но ошибка еще не обработана
   - Выводится: `"long() result"`

3. **Второй await**: `await promise1` пытается получить результат от уже завершившегося промиса
   - Поскольку `promise1` завершился с ошибкой, выбрасывается исключение
   - Выполнение переходит в блок `catch`
   - Выводится: `"CATCH ERROR"`

4. **Завершение**: После обработки ошибки функция `start()` завершается успешно
   - Выводится: `"test done"`

**Ключевой момент**: Промисы запускаются параллельно, но await обрабатывает их результаты последовательно в том порядке, в котором написаны в коде.