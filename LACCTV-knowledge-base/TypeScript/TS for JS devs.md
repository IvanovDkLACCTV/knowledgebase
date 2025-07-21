[5 TypeScript Tips You'll Actually Use (Best Practices)✨ – YouTube](https://www.youtube.com/watch?v=V8rl6-Sv3-g&utm_source=chatgpt.com)

Вот краткий конспект:

**1. Простой вывод типов через `as const` и `typeof`:**  
Использование `as const` помогает зафиксировать значение как литерал, а `typeof` позволяет вывести тип без дублирования. Упрощает работу с константами, оберегая от нежелательных изменений.

**2. Извлечение и повторное использование типов из функций:**  
Вместо вручную определять типы, используйте `ReturnType<typeof fn>` и `Parameters<typeof fn>`, чтобы автоматически получать типы возврата и параметров функций.

**3. Улучшенные типы для `map(), reduce()` и `.filter()`:**  
Пример с `reduce()` показывает, как задать тип аккумулятора вместо `any` для мощного контроля над данными на каждом шаге.

**4. `keyof typeof` — безопасный доступ к объектам:**  
Позволяет типобезопасно получить доступ к значениям объекта, избегая runtime‑ошибок.

**5. Условные типы (`extends ? :`) для более точного типобезопасного кода:**  
Пример с фильтрацией массива показал использование условных типов для уточнения результата: если массив строк — массив строк, иначе — массив чисел.

---

[TypeScript for JavaScript Developers in 15 min – YouTube](https://www.youtube.com/watch?v=JUORwadOU7s&utm_source=chatgpt.com)

Основные идеи:

**1. Типизация вместо комментариев и логики проверок:**  
TS помогает выявлять ошибки на этапе сборки, устраняя необходимость в runtime-проверках.

**2. `interface` и `type`:**

- `interface` хорош для описания объектов и расширения (extends).
    
- `type` удобнее для объединений (`union`), пересечений (`intersection`) и примитивов.
    

**3. Аннотации функций и переменных:**  
Выделение параметров и возвращаемых значений делает API яснее и позволяет избежать неожиданных `undefined` и `null`.

**4. Опциональные свойства и строгая проверка `null`:**  
Использование `?` и включение строгого режима (`strictNullChecks`) повышает надежность кода.

**5. Алгоритмы работы с типами (`Enum`, `Union`, `Literal Types`):**  
Примеры:

- `enum` — для групп связанных констант.
    
- `union` и `literal` — для строгих наборов значений.
    

**6. Интерфейсы для функций:**  
Можно описывать сигнатуру функции как интерфейс: для унификации и переиспользования.

**7. Generic-функции и ограничения (`extends`):**  
Пример: `function identity<T>(arg: T): T`.  
Добавление `extends` (например, `T extends string`) позволяет накладывать ограничения и обеспечивать безопасность.

**8. Примеры использования:**  
Показывается, как внедрять TS в существующий JS-проект: постепенная миграция с помощью `allowJs`, начни с аннотаций `.js`, постепенно переходя на `.ts`.

---

### 🧠 Резюме

|Что|Преимущество|
|---|---|
|Литеральные типы, `keyof` и вывод `typeof`|Повышают точность и безопасность|
|Автоматическое извлечение типов|Упрощает повторное использование|
|Интерфейсы, типы, generic-ы|Делают код гибким, читаемым и расширяемым|
|Строгая null-проверка|Уменьшает runtime‑ошибки|
|Пошаговая миграция|Позволяет внедрить TS без глобального рефакторинга|


---

## ✅ Видео 1: _5 TypeScript Tips You’ll Actually Use_

1. **Литеральные типы через `as const` + `typeof`**
    
    ```ts
    const COLORS = ['red', 'green', 'blue'] as const;
    type Color = typeof COLORS[number]; // 'red' | 'green' | 'blue'
    ```
    
    Это корректно: `as const` делает значения именно литеральными, а `typeof` позволяет автоматически выводить типы ([mayashavin.com](https://mayashavin.com/articles/types-from-constants-typescript?utm_source=chatgpt.com "Using keyof and typeof for types efficiently in TypeScript - Maya Shavin")).
    
2. **`ReturnType` и `Parameters`**
    
    ```ts
    function sum(a: number, b: number) { return a + b; }
    type SumReturn = ReturnType<typeof sum>; // number
    type SumParams = Parameters<typeof sum>; // [number, number]
    ```
    
    Совершенно точно — встроенные утилиты TS вытягивают формы функций ([mayashavin.com](https://mayashavin.com/articles/types-from-constants-typescript?utm_source=chatgpt.com "Using keyof and typeof for types efficiently in TypeScript - Maya Shavin"), [TypeScript](https://www.typescriptlang.org/docs/handbook/2/generics.html?utm_source=chatgpt.com "Generics - TypeScript: Documentation")).
    
3. **Уточнённый тип аккумулятора в `reduce()`**
    
    ```ts
    const nums = [1, 2, 3];
    const total = nums.reduce((acc: number, cur: number) => acc + cur, 0);
    ```
    
    Согласуется со спецификацией — точная типизация `accumulator` убирает `any`.
    
4. **`keyof typeof` для безопасных ключей**
    
    ```ts
    const config = { host: '', port: 8080 } as const;
    function get<C>(obj: C, key: keyof C) {
      return obj[key];
    }
    ```
    
    Это точное применение TS-идеи типов ключей ([mayashavin.com](https://mayashavin.com/articles/types-from-constants-typescript?utm_source=chatgpt.com "Using keyof and typeof for types efficiently in TypeScript - Maya Shavin"), [TypeScript](https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html?utm_source=chatgpt.com "Documentation - Template Literal Types - TypeScript")).
    
5. **Условные типы `T extends U ? X : Y`**  
    Из примера:
    
    ```ts
    type Filtered<T> = T extends string ? string[] : number[];
    ```
    
    Всё корректно согласно шаблонам TS conditional types ([TypeScript](https://www.typescriptlang.org/docs/handbook/unions-and-intersections.html?utm_source=chatgpt.com "Handbook - Unions and Intersection Types - TypeScript"), [Stack Overflow](https://stackoverflow.com/questions/58434389/typescript-deep-keyof-of-a-nested-object?utm_source=chatgpt.com "Typescript: deep keyof of a nested object - Stack Overflow")).
    

---

## ✅ Видео 2: _TypeScript for JavaScript Developers in 15 min_

1. **Типизация вместо комментариев и runtime-проверок** — общий принцип TS, соответствует как TS, так и ES2026.
    
2. **`interface` vs `type`**
    
    - `interface Person { name: string }`
        
    - `type Status = 'loading' | 'success'`  
        Совместимо с описаниями в официальной документации ([JavaScript in Plain English](https://javascript.plainenglish.io/5-very-useful-tricks-for-thetypescript-typeof-operator-404c0d30cd5?utm_source=chatgpt.com "5 Very Useful Tricks for TypeScript Typeof Operator")).
        
3. **Аннотация параметров и возвращаемых значений**
    
    ```ts
    function greet(name: string): string { return `Hi, ${name}`; }
    ```
    
    Это рекомендуемый подход ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html?utm_source=chatgpt.com "Documentation - More on Functions - TypeScript"), [exploringjs.com](https://exploringjs.com/ts/book/ch_typescript-essentials.html?utm_source=chatgpt.com "4 The basics of TypeScript - Exploring JS")).
    
4. **Строгий `null` и `?`**  
    Возможность предотвращения `undefined`/`null` ошибок подтверждается строгим режимом TypeScript ([exploringjs.com](https://exploringjs.com/ts/book/ch_typescript-essentials.html?utm_source=chatgpt.com "4 The basics of TypeScript - Exploring JS"), [Stack Overflow](https://stackoverflow.com/questions/64527150/in-typescript-how-to-select-a-type-from-a-union-using-a-literal-type-property?utm_source=chatgpt.com "In Typescript, how to select a type from a union, using a literal type ...")).
    
5. **`enum`, `union`, `literal types`**
    
    ```ts
    enum Role { Admin, User }
    type Mode = 'light' | 'dark';
    ```
    
    Полностью поддерживается базовым синтаксисом ([Total TypeScript](https://www.totaltypescript.com/books/total-typescript-essentials/unions-literals-and-narrowing?utm_source=chatgpt.com "Unions, Literals, and Narrowing - Total TypeScript"), [TypeScript](https://www.typescriptlang.org/docs/handbook/2/generics.html?utm_source=chatgpt.com "Generics - TypeScript: Documentation")).
    
6. **Типизация функций через интерфейсы**
    
    ```ts
    interface Greeter { (name: string): void }
    ```
    
    Упоминается в официальной секции по функциям ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/functions.html?utm_source=chatgpt.com "Documentation - More on Functions - TypeScript")).
    
7. **Обобщённые (Generic) функции**
    
    ```ts
    function identity<T>(x: T): T { return x; }
    ```
    
    Это классический пример, точно отражённый в документации ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/generics.html?utm_source=chatgpt.com "Generics - TypeScript: Documentation")).
    
8. **Пошаговая миграция с `allowJs`** — стандартный подход при внедрении TS в JS-проект.
    

---

## 🔍 Проверка соответствия спецификациям

- **TypeScript**: все приёмы — `as const`, `keyof`, generics и т. д. — встроены в TS-дефиниции (всп. docs и примеры выше).
    
- **ES2026/HTML5/WebAPI**: видео затрагивают только типизацию TypeScript, не меняя реализацию JS/WebAPI — никаких конфликтов нет.
    

---

## 💡 Дополнительные примеры

### Тип "паттерн матчинга" с `Extract`

```ts
type Action = { type: 'add'; value: number } | { type: 'remove'; id: string };
type Handlers = { [P in Action['type']]: Extract<Action, {type: P}> };

const handlers: { add: (a: Handlers['add']) => void; remove: (a: Handlers['remove']) => void } = {
  add: a => console.log(a.value),
  remove: a => console.log(a.id),
};
```

Согласуется с примерами юзеров на StackOverflow ([Stack Overflow](https://stackoverflow.com/questions/64527150/in-typescript-how-to-select-a-type-from-a-union-using-a-literal-type-property?utm_source=chatgpt.com "In Typescript, how to select a type from a union, using a literal type ...")).

### Generic identity

```ts
function identity<T>(arg: T): T { return arg; }
const result = identity(42); // тип число
```

Именно так описано в TS-руководстве ([TypeScript](https://www.typescriptlang.org/docs/handbook/2/generics.html?utm_source=chatgpt.com "Generics - TypeScript: Documentation")).

---

## ✅ Итог

- Примеры из видео **полностью соответствуют** спецификациям TypeScript.
    
- Типизация чисто TypeScript не конфликтует с ES2026, HTML5 или Web API.
    
- Примеры кода — правильны и рекомендованы.
    

