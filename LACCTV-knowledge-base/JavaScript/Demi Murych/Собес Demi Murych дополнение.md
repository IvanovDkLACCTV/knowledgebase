
---

### 1. Function Declaration vs Function Expression

- **Спецификация ECMA‑262 (последнее издание):** официальное описание конструкций `FunctionDeclaration` и `FunctionExpression` ([TC39](https://tc39.es/ecma262/multipage/ecmascript-language-functions-and-classes.html?utm_source=chatgpt.com "15 ECMAScript Language: Functions and Classes"))
    
- **MDN:** разница в поведении hoisting (подготовка функции до выполнения кода vs. только при достижении строки) ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function?utm_source=chatgpt.com "function expression - JavaScript - MDN Web Docs - Mozilla"), [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions?utm_source=chatgpt.com "Functions - JavaScript - MDN Web Docs"))
    

**Демо:**

```js
// Function Declaration — работает до объявления
hoisted(); // OK

function hoisted() {
  console.log('declaration');
}

// Function Expression — ошибка при вызове до объявления
try {
  notYet(); // TypeError
} catch (e) {
  console.log('expression not hoisted');
}

const notYet = function() {
  console.log('expression');
};
```

---

### 2. Arrow Functions (→ Functions Expression)

- **MDN — Arrow function expression:** нет собственного `this`, `arguments`, нельзя использовать с `new` или `yield` ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions?utm_source=chatgpt.com "Arrow function expressions - JavaScript - MDN Web Docs"))
    
- **Спецификация ECMA‑262 6th Edition (ES2015):** добавление Arrow functions как FunctionExpression без самостоятельного `this` и `prototype` ([en.wikipedia.org](https://en.wikipedia.org/wiki/ECMAScript_version_history?utm_source=chatgpt.com "ECMAScript version history"))
    

**Демо:**

```js
const arrow = (a, b) => a + b;
console.log(arrow(2,3)); // 5

// this и arguments
const obj = {
  x: 10,
  arrowFn: () => console.log(this),
  regularFn() { console.log(this); }
};
obj.arrowFn();    // this — внешнее, не obj
obj.regularFn();  // this === obj

// new на стрелочной — TypeError
try {
  new (() => {});
} catch(e) {
  console.log('Cannot use new with arrow');
}
```

---

### 3. `arguments` и стрелочные функции

- MDN описывает, что стрелочные функции не имеют собственного объекта `arguments`, и нужно использовать rest-параметры ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions?utm_source=chatgpt.com "Arrow function expressions - JavaScript - MDN Web Docs"))
    
- В спецификации `arguments` реализован как необычный объект (exotic), плохо оптимизируемый V8 — но форма не позволяет arrow взглянуть на него ([TC39](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification"), [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise?utm_source=chatgpt.com "Promise - JavaScript - MDN Web Docs"))
    

**Демо:**

```js
function regular() {
  console.log(arguments[0]);
}
regular(42); // 42

const arrow = () => {
  try {
    console.log(arguments);
  } catch (e) {
    console.log('no arguments in arrow');
  }
};
arrow(42);
```

---

### 4. Map и Set

- В спецификации ECMA‑262 раздел **24.1 Map Objects** описывает `Map` как коллекцию ключ/значение, `Set` аналогично уникальных значений ([TC39](https://tc39.es/ecma262/multipage/keyed-collections.html?utm_source=chatgpt.com "24 Keyed Collections"))
    

**Демо:**

```js
const m = new Map();
m.set('a',1);
m.set({},2);
console.log([...m.keys()]); // ['a', {}]

const s = new Set([1,2,2,3]);
console.log([...s]); // [1,2,3]
```

---

### 5. Promise (состояния и статические методы)

- **MDN по Promise:** описание состояний `pending`, `fulfilled`, `rejected`, а также поведения `resolve`, `then`, `catch`, `finally` ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise?utm_source=chatgpt.com "Promise - JavaScript - MDN Web Docs"))
    
- **StackOverflow / спецификация ECMAScript/A+:** Promise/A+ соответствует спецификации ECMAScript, ECMA‑262 имплементирует это полностью ([stackoverflow.com](https://stackoverflow.com/questions/53349615/whats-the-difference-between-promise-a-specification-and-ecma-specs-promise-s?utm_source=chatgpt.com "What's the difference between Promise/A+ specification ..."))
    

**Демо:**

```js
Promise.resolve(1).then(v => console.log('then', v));
Promise.reject('err').catch(e => console.log('catch', e));
Promise.all([Promise.resolve(2), 3]).then(vals =>
  console.log('all', vals)
);
```

---

### 6. Другие ключевые моменты (вопросы и ответы по спецификации)

|Тема|Кратко по спецификации|
|---|---|
|`this`, `call`, `apply`, `bind`|`this` — параметр normal function; `bind` создаёт новую функцию. ([TC39](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification"), [TC39](https://tc39.es/ecma262/multipage/ecmascript-language-functions-and-classes.html?utm_source=chatgpt.com "15 ECMAScript Language: Functions and Classes"))|
|Лексические окружения (Lexical Environment) — механизм замыканий и TDZ (`let`/`const`) описан в спецификации (Clause о идентификаторах и окружениях) ([262.ecma-international.org](https://262.ecma-international.org/5.1/?utm_source=chatgpt.com "ECMAScript Language Specification - ECMA-262 Edition 5.1"), [TC39](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification"))||
|`var` vs `let`/`const` — temporal dead zone, нет повторного объявления, `const` константная связь — всё в ECMA‑262 ([en.wikipedia.org](https://en.wikipedia.org/wiki/ECMAScript_version_history?utm_source=chatgpt.com "ECMAScript version history"), [TC39](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification"))||
|`structuredClone` — добавлен в ES2021/ES2022, спецификация содержит соответствующее описание технологии копирования ([en.wikipedia.org](https://en.wikipedia.org/wiki/ECMAScript_version_history?utm_source=chatgpt.com "ECMAScript version history"))||
|`Object.freeze` / `seal` / `preventExtensions` — описаны как встроенные стандартные методы ([262.ecma-international.org](https://262.ecma-international.org/5.1/?utm_source=chatgpt.com "ECMAScript Language Specification - ECMA-262 Edition 5.1"), [TC39](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification"))||

---

## 🌀 Event Loop, Task vs Microtask

- **Спецификация HTML5 / WHATWG** описывает Event Loop, **Task Queue** и **Microtask Queue (Jobs)** как части жизненного цикла страницы и JS‑окружения. Подробный алгоритм — в разделах спецификации HTML Standard ([html.spec.whatwg.org](https://html.spec.whatwg.org/multipage/webappapis.html?utm_source=chatgpt.com "Event loops - HTML Standard")).
    
- **ECMAScript (TC39)** вводит понятия _Task_ и _Job Queue_ именно для описания Promise и общего порядка выполнения асинхронных операций ([TC39](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification")).
    
- **MDN / веб‑документация** поясняет реальные очередности: после каждого macrotask выполняются все microtasks до отрисовки ([javascript.info](https://javascript.info/event-loop?utm_source=chatgpt.com "Event loop: microtasks and macrotasks")).
    

**Мини-демо:**

```js
console.log('sync');

setTimeout(() => console.log('macrotask'), 0);

Promise.resolve()
  .then(() => console.log('micro1'))
  .then(() => console.log('micro2'));

console.log('end');
// Вывод:
// sync
// end
// micro1
// micro2
// macrotask
```

---

## 🧠 Garbage Collection (GC) и WeakRef / FinalizationRegistry

- **ECMA‑262 спецификация** прямо говорит: **GC — не часть спецификации JavaScript**, это задача хост‑окружения (браузер, Node.js) ([262.ecma-international.org](https://262.ecma-international.org/?utm_source=chatgpt.com "ECMA-262, 16 th edition, June 2025 ECMAScript® 2025 ...")).
    
- В версиях ES2021+ официально определены объекты **WeakRef** и **FinalizationRegistry** для работы с слабой ссылочностью и регистрацией действий при сборке мусора **без сохранения ссылки на объект** ([TC39](https://tc39.es/ecma262/multipage/managing-memory.html?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification")).
    
- **MDN FinalizationRegistry** поясняет, что финализаторы вызываются «когда объект удалён сборщиком мусора», но время его вызова не гарантировано и может задерживаться ([MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/FinalizationRegistry?utm_source=chatgpt.com "FinalizationRegistry - JavaScript - MDN Web Docs")).
    

**Мини-демо:**

```js
let registry = new FinalizationRegistry(token => {
  console.log('object was collected:', token);
});

(function(){
  let obj = { a:1 };
  registry.register(obj, 'token‑A');
})(); // obj выходит из области видимости — доступен для GC

// GC произойдёт непредсказуемо; финализатор может вызвать логирование.
```

---

## 🌐 structuredClone — глубокое клонирование

- **ECMAScript спецификация** (начиная с ES2021/ES2022) описывает алгоритм `structuredClone`, встроенный метод для глубокого безопасного копирования сложных структур (объекты, массивы, TypedArray, Map, Set и др.) ([proposals.es](https://www.proposals.es/specifications?utm_source=chatgpt.com "ECMAScript Specifications")).
    

**Мини-демо:**

```js
const original = { a: 1, b: { c: 2 }, arr: [3,4] };
const copy = structuredClone(original);
copy.b.c = 42;
console.log(original.b.c); // 2 — оригинал не изменился
```

---

## 🔄 Взаимосвязь с темами собеседования:

|Тема|Спецификация|Мини-скрипт|
|---|---|---|
|Event Loop (Job vs Task)|WHATWG HTML, TC39|см. выше|
|Garbage Collection / WeakRef|ECMA‑262 Managing Memory (§26)|FinalizationRegistry выше|
|structuredClone|ECMA‑262 ES2021+|см. выше|
|Замыкания / лексические окружения|ECMA‑262 Lexical Environments (моё предыдущее сообщение включает упоминание)|пример с `closure` могу добавить при необходимости|

---

## 1. **Arrow Functions, `this`, `call`, `apply`, `bind`**

- **Спецификация ECMAScript (ES2026)** — глава про callable values, методы `.call()`, `.apply()`, `.bind()`; таблица, показывающая, какие виды функций можно вызывать как конструкторы и как они обрабатывают `this` ([exploringjs.com](https://exploringjs.com/js/downloads/exploring-js-book-preview.pdf?utm_source=chatgpt.com "Exploring JavaScript (ES2025 Edition)")).
    
- **Аргументы:**
    
    - `call(thisValue, …args)`, `apply(thisValue, argsArray)`, `bind(thisValue, …args)` — управление `this` и аргументами функции ([exploringjs.com](https://exploringjs.com/js/downloads/exploring-js-book-preview.pdf?utm_source=chatgpt.com "Exploring JavaScript (ES2025 Edition)")).
        
    - Для обычных функций `this` назначается из контекста вызова; стрелочные функции сохраняют `this` лексически, игнорируя `call/apply/bind` ([exploringjs.com](https://exploringjs.com/js/downloads/exploring-js-screen-preview.pdf?utm_source=chatgpt.com "Exploring JavaScript (ES2024 Edition)")).
        

**Демо:**

```js
function f(x) { return [this, x]; }
console.log(f.call({a:1}, 2)); // [{a:1}, 2]
const arrow = v => [this, v];
console.log(arrow.call({a:1}, 2)); // [lexical-this-контекст, 2]
```

---

## 2. **Lexical Environment и Замыкания**

- **ECMAScript спецификация** описывает цепочки лексических окружений (`Lexical Environment`), TDZ для `let`/`const` и механизм сохранения окружения функцией после её создания — фундамент замыкания.
    
- **Поведение `var` vs `let/const`:** `var` инициализируется `undefined` в начале блока, `let/const` — блокируются до момента связывания (TDZ). Повторное объявление запрещено у `let/const`. `const` создаёт неизменяемую связь по именованию, не по значению. ([tc39.es](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification"), [exploringjs.com](https://exploringjs.com/js/downloads/exploring-js-book-preview.pdf?utm_source=chatgpt.com "Exploring JavaScript (ES2025 Edition)"))
    

**Демо:**

```js
function outer() {
  let x = 1;
  return () => x;
}
const fn = outer();
console.log(fn()); // 1
```

---

## 3. **Event Loop: Task Queue и Microtask Queue**

- **WHATWG HTML Standard** описывает Event Loop, включая алгоритмы очередей заданий (`task queue`) и микрозаданий (`microtask queue`), включая `microtask checkpoint`, выполнение всех микрозадач после каждой задачи, условия выбора следующей задачи и лимит времени идл-режима ([html.spec.whatwg.org](https://html.spec.whatwg.org/multipage/webappapis.html?utm_source=chatgpt.com "Event loops - HTML Standard")).
    
- **JavaScript Job Queue (в ECMAScript)** определяет, что `Promise`-обработчики (`then`/`catch`/`finally`), а также `queueMicrotask` создают микрозадачи (`jobs`) ([jakearchibald.com](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/?utm_source=chatgpt.com "Tasks, microtasks, queues and schedules"), [developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide?utm_source=chatgpt.com "Using microtasks in JavaScript with queueMicrotask()"), [stackoverflow.com](https://stackoverflow.com/questions/25915634/difference-between-microtask-and-macrotask-within-an-event-loop-context?utm_source=chatgpt.com "Difference between microtask and macrotask within an ...")).
    

**Демо:**

```js
console.log('A');
setTimeout(() => console.log('B'), 0);
Promise.resolve().then(() => console.log('C')).then(() => console.log('D'));
console.log('E');
// Вывод: A E C D B
```

---

## 4. **WeakRef, FinalizationRegistry и Garbage Collection**

- **ECMAScript** отмечает, что сборщик мусора — не часть языка, это обязанность хост среды.
    
- Начиная с ES2021–ES2022 стандартизированы **WeakRef** и **FinalizationRegistry** — объекты слабой ссылочности и финализации, позволяющие регистрировать коллбэки после сборки мусора, без удержания сильных ссылок ([tc39.es](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification")).
    

**Демо:**

```js
const registry = new FinalizationRegistry(token => console.log('finalized', token));
(function(){
  const obj = { a:1 };
  registry.register(obj, 'tok1');
})(); 
// финализатор может сработать позже, когда obj будет удалён сборщиком
```

---

## 5. **Глубокое клонирование: `structuredClone`**

- **Спецификация ECMAScript ES2021+** описывает алгоритм `structuredClone`, актуальный способ создания глубоких копий многих структур (Map, Set, TypedArray, циклические ссылки) без сторонних библиотек ([tc39.es](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification")).
    

**Демо:**

```js
const a = { x: 1, nested: { y:2 }, arr: [3] };
const b = structuredClone(a);
b.nested.y = 99;
console.log(a.nested.y); // 2
```

---

## 6. **Map и Set**

- **ECMAScript 262**: раздел “Keyed Collections” описывает `Map` (из любых типов в качестве ключей) и `Set` (уникальные значения), сохранение порядка вставки ключей/значений и специализацию коллекций ([tc39.es](https://tc39.es/ecma262/?utm_source=chatgpt.com "ECMAScript® 2026 Language Specification")).
    

**Демо:**

```js
const m = new Map([['a',1], ['b',2]]);
m.set({}, 3);
for (const [k, v] of m) console.log(k, v);

const s = new Set([1,2,2,3]);
console.log(s.has(2), [...s]);
```

---

### Ссылки на статьи

---

### 🔹 Arrow Functions, `this`, `.call()`, `.apply()`, `.bind()`

- Раздел про Callable Values и методы Function в спецификации ECMAScript — поведение `call`, `apply`, `bind` и управление `this`: **ECMAScript §9.2.2 и §9.2.3** ([html.spec.whatwg.org](https://html.spec.whatwg.org/multipage/webappapis.html?utm_source=chatgpt.com "Event loops - HTML Standard"))  
    _(в тексте понятия `normal function`, `bound function`, `lexical this` описаны явно)_
    

---

### 🔹 Lexical Environment и Замыкания, `var` vs `let/const`, TDZ

- Описание цепочек лексических окружений (Lexical Environment), временной мёртвой зоны, замыканий и правил `let`, `const`, `var`: **ECMAScript Lexical Environments** ([html.spec.whatwg.org](https://html.spec.whatwg.org/multipage/webappapis.html?utm_source=chatgpt.com "Event loops - HTML Standard"))
    

---

### 🔹 Event Loop, Task Queue и Microtask Queue (Jobs)

- HTML Standard (WHATWG), раздел **"Event loops"**: архитектура event loop, distinction between task queues и microtask queue ([html.spec.whatwg.org](https://html.spec.whatwg.org/multipage/webappapis.html?utm_source=chatgpt.com "Event loops - HTML Standard"))
    
- Дополнительная информация о таймерах и микрозадачах: **Timers & Microtask Queue** (queueMicrotask, setTimeout) в HTML Spec §8.6–8.7 ([html.spec.whatwg.org](https://html.spec.whatwg.org/dev/timers-and-user-prompts.html?utm_source=chatgpt.com "8.6 Timers - HTML Standard, Edition for Web Developers"))
    

---

### 🔹 Garbage Collection, WeakRef и FinalizationRegistry

- Описание: сборщик мусора — не входит в ECMAScript; системные слабые ссылки и финализация: **ECMAScript Managing Memory и базовые WeakRef / FinalizationRegistry алгоритмы** ([html.spec.whatwg.org](https://html.spec.whatwg.org/multipage/webappapis.html?utm_source=chatgpt.com "Event loops - HTML Standard"))
    

---

### 🔹 `structuredClone`

- Алгоритм глубокого клонирования, появившийся в ES2021+ в разделе **"Performing structured cloning algorithm"** ECMAScript ([html.spec.whatwg.org](https://html.spec.whatwg.org/multipage/webappapis.html?utm_source=chatgpt.com "Event loops - HTML Standard"))
    

---

### 🔹 Map и Set — Keyed Collections

- Спецификация ECMAScript, раздел **"Keyed Collections"** описывает `Map` и `Set`, порядок итерации, типы ключей и поведение API ([html.spec.whatwg.org](https://html.spec.whatwg.org/multipage/webappapis.html?utm_source=chatgpt.com "Event loops - HTML Standard"))
    

---



