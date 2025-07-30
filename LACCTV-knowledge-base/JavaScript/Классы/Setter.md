
# Сеттеры в JavaScript (`set`)

>[Ссылка на статью](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Functions/set)

Оператор `set` связывает свойство объекта с функцией, которая будет вызвана при попытке установить это свойство.

---

## 📌 Синтаксис

```js
{ set prop(val) { ... } }
{ set [expression](val) { ... } } // с ECMAScript 6
```

### Параметры

- **prop** — имя свойства, связанного с функцией.
    
- **val** — значение, которое передаётся сеттеру.
    
- **expression** — выражение (с ES6), вычисляющее имя свойства.
    

---

## 🧠 Описание

Сеттер позволяет выполнять функцию при установке значения свойства. Обычно используется в паре с геттером для создания **псевдо-свойства**.

> ⚠️ Невозможно одновременно иметь сеттер и собственное значение у одного свойства.

---

### Особенности

- Идентификатор может быть строкой или числом.
    
- Сеттер должен иметь **ровно один параметр**.
    
- Нельзя объявлять два `set` с одинаковым именем или совмещать `set` с обычным значением:
    
    ```js
    // ❌ Ошибки:
    { set x(v) {}, set x(v) {} }
    { x: 123, set x(v) {} }
    ```
    
- Сеттер можно удалить с помощью `delete`.
    

---

## 🔍 Примеры

### Определение сеттера в объекте

```js
const o = {
  log: [],
  set current(str) {
    this.log[this.log.length] = str;
  },
};

o.current = "hello";
o.current = "world";

console.log(o.log); // ["hello", "world"]
```

> 📌 Свойство `current` не определено как значение, поэтому чтение `o.current` вернёт `undefined`.

---

### Удаление сеттера

```js
delete o.current;
```

---

### `Object.defineProperty`

Добавление сеттера к существующему объекту:

```js
const o = { a: 0 };

Object.defineProperty(o, "b", {
  set: function (x) {
    this.a = x / 2;
  },
});

o.b = 10;
console.log(o.a); // 5
```

---

### Вычисляемое имя свойства

```js
const expr = "foo";

const obj = {
  baz: "bar",
  set [expr](v) {
    this.baz = v;
  },
};

console.log(obj.baz); // "bar"
obj.foo = "baz";
console.log(obj.baz); // "baz"
```

---

## 📚 Спецификация

- [ECMAScript® 2026 Language Specification — Method Definitions](https://tc39.es/ecma262/#sec-method-definitions)
    

---

