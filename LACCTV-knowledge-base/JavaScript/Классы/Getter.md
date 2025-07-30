# Геттеры в JavaScript (`get`) 

>[Ссылка на статью](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Functions/get)

Синтаксис `get` связывает свойство объекта с функцией, которая будет вызываться при обращении к этому свойству.

## 📘 Интерактивный пример

```js
const obj = {
  log: ["a", "b", "c"],
  get latest() {
    return this.log[this.log.length - 1];
  },
};

console.log(obj.latest);
// Expected output: "c"
```

---

## 📌 Синтаксис

```js
{ get prop() { ... } }
{ get [expression]() { ... } } // начиная с ES6
```

### Параметры

- **prop** — имя свойства, привязываемого к функции.
    
- **expression** — выражение для вычисляемого имени свойства (поддерживается с ECMAScript 6).
    

---

## 🧠 Описание

Геттер позволяет обращаться к функции как к обычному свойству. Это удобно, когда:

- значение свойства зависит от состояния;
    
- не хочется вызывать метод напрямую (`obj.getValue()` → `obj.value`);
    
- нужно создать **псевдосвойство**.
    

> ⚠️ Нельзя одновременно использовать `get` и обычное значение для одного свойства. Также нельзя объявлять два `get` с одинаковым именем.

> ✅ Геттер можно удалить с помощью `delete`.

---

## 🔍 Примеры

### Определение геттера в объекте

```js
const obj = {
  log: ["example", "test"],
  get latest() {
    if (this.log.length === 0) return undefined;
    return this.log[this.log.length - 1];
  },
};

console.log(obj.latest); // "test"
```

Попытка изменить `obj.latest` не сработает — это только для чтения.

---

### Удаление геттера

```js
delete obj.latest;
```

---

### `Object.defineProperty`

```js
const o = { a: 0 };

Object.defineProperty(o, "b", {
  get: function () {
    return this.a + 1;
  },
});

console.log(o.b); // 1
```

---

### Вычисляемое имя свойства

```js
const expr = "foo";

const obj = {
  get [expr]() {
    return "bar";
  },
};

console.log(obj.foo); // "bar"
```

> ⚠️ Работает только в средах с поддержкой ES6+.

---

### Ленивый геттер / умный геттер

```js
get notifier() {
  delete this.notifier;
  return (this.notifier = document.getElementById("bookmarked-notification-anchor"));
}
```

Первый вызов геттера заменяет его обычным свойством и кэширует результат.

Полезно, когда:

- вычисление ресурсоёмкое;
    
- значение нужно не сразу (или вообще не нужно);
    
- значение используется многократно.
    

> 🧠 В Firefox см. `XPCOMUtils.defineLazyGetter()`.

---

## 🏗️ Геттеры и классы

### Разница между `get` и `Object.defineProperty`:

```js
class Example {
  get hello() {
    return "world";
  }
}

const obj = new Example();
console.log(obj.hello); // "world"

console.log(Object.getOwnPropertyDescriptor(obj, "hello"));
// undefined

console.log(Object.getOwnPropertyDescriptor(Object.getPrototypeOf(obj), "hello"));
// { configurable: true, enumerable: false, get: ƒ, set: undefined }
```

- `get` → определяет геттер в **прототипе**.
    
- `defineProperty` → определяет геттер в **экземпляре**.
    

---

## 📚 Спецификация

- [ECMAScript® 2026 Language Specification — Method Definitions](https://tc39.es/ecma262/#sec-method-definitions)
    

---

