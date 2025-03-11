#### Базовые типы в TypeScript

**TypeScript** расширяет **JavaScript**, добавляя строгую типизацию. Вот основные типы:

| **Тип**        | **Описание**                                    | **Пример**                             |
|----------------|------------------------------------------------|----------------------------------------|
| `number`       | Числа (целые, дробные, `NaN`, `Infinity`)       | `let age: number = 25;`                |
| `string`       | Строки                                          | `let name: string = "Alice";`          |
| `boolean`      | Логический тип (`true`/`false`)                 | `let isAdmin: boolean = true;`         |
| `null`         | Отсутствие значения                             | `let empty: null = null;`              |
| `undefined`    | Неопределённое значение                         | `let u: undefined = undefined;`        |
| `any`          | Любое значение (отключает проверку типов)       | `let anything: any = 42;`              |
| `void`         | Отсутствие значения (например, в функциях)      | `function log(): void { console.log("Hi"); }` |
| `never`        | Значение, которое никогда не возвращается       | `function error(): never { throw new Error("Oops"); }` |
| `object`       | Объекты (любые сложные структуры)               | `let obj: object = { id: 1 };`         |
| `unknown`      | Неизвестный тип (более безопасная альтернатива `any`) | `let value: unknown = "text";`         |
#### Объявление переменной с типом и без:

```typescript
// С типом:
let username: string = "Alice";
let age: number = 30;

// Без указания типа (TypeScript сам выведет тип):
let isLoggedIn = true; // boolean

```

#### Ошибка при операциях с разными типами:

**TypeScript** предотвращает ошибки во время компиляции.

❌ Попытка сложить строку и число:

```typescript
let age: number = 30;
let name: string = "Alice";

// Ошибка: Операнд типа "number" нельзя использовать с "string"
console.log(age + name);

```

#### Типизация массивов:

```typescript
// Массив чисел:
let numbers: number[] = [1, 2, 3];

// Массив строк:
let names: string[] = ["Alice", "Bob"];

// Используя `Array<T>`:
let boolArray: Array<boolean> = [true, false];
```

#### Тип *any*:

`any` отключает проверку типов, и переменная может принимать любое значение.

```typescript
let data: any = 42;
data = "string";  // Нет ошибки
data = true;      // Нет ошибки
```

**Почему `any` — это плохо в продакшене?**

- Теряется защита типов.
- Ошибки могут проявиться только во время выполнения.
- Сложнее поддерживать и рефакторить код.

**Рекомендуется вместо `any` использовать:**

- `unknown` — если тип заранее неизвестен.
- `union types` — для нескольких допустимых типов.

#### Настройка *noImplicitAny* в *tsconfig.json*:

Включает проверку, чтобы все переменные и параметры имели явный тип.

```json
{
  "compilerOptions": {
    "noImplicitAny": true
  }
}

```
✅ **Преимущество:** TypeScript не позволит использовать `any` неявно.

#### Переприсваивание типов:

Тип переменной фиксируется при объявлении.

❌ Ошибка:
```typescipt
let age: number = 30;
age = "thirty"; // Ошибка: Нельзя присвоить тип "string"
```

✅ Решение — использовать `union`:
```typescript
let age: number | string = 30;
age = "thirty"; // ОК
```

#### Типизация функций:

Функция с явным указанием типов аргументов и возвращаемого значения:
```typescipt
function add(a: number, b: number): number {
  return a + b;
}
```

✅ Стрелочная функция:
```typescript
const multiply = (x: number, y: number): number => x * y;
```

#### Типизация *map* и *reduce*:

Примеры работы с массивами:

`map`:
```typescipt
const numbers: number[] = [1, 2, 3];
const squared: number[] = numbers.map((n: number) => n * n);
```

`reduce`:
```typescript
const sum: number = numbers.reduce((acc: number, curr: number) => acc + curr, 0);
```

#### Вопросительный знак **?** (Optional properties):

Используется для обозначения необязательных свойств или параметров.

Пример:
```typescipt
interface User {
  id: number;
  name?: string; // Необязательно
}

const user: User = { id: 1 };
```

✅ В функции:
```typescript
function greet(name?: string): void {
  console.log(`Hello, ${name ?? "Guest"}`);
}
```

#### Union и Safety Types:

Union позволяет переменной принимать несколько типов:
```typescipt
let value: string | number;
value = 10;       // ОК
value = "Hello";  // ОК
```

✅ В функциях:
```typescript
function printId(id: number | string): void {
  if (typeof id === "number") {
    console.log(`ID: ${id}`);
  } else {
    console.log(`String ID: ${id}`);
  }
}
```

✅ В массивах (гетерогенные массивы):
```typescript
let mixed: (number | string)[] = [1, "two", 3];
```

#### Тип *void*:

Используется для функций, которые **ничего не возвращают**.

Пример:
```typescipt
function logMessage(message: string): void {
  console.log(message);
}
```

❌ Нельзя:
```typescript
let result: void = logMessage("Test");
// Ошибка: Значение функции с типом void нельзя присвоить
```

#### *undefined* и *null*:

- **`undefined`** — переменная объявлена, но не инициализирована.
- **`null`** — переменная явно не имеет значения.

```typescipt
let u: undefined = undefined;
let n: null = null;
```

🔔 В TypeScript `undefined` и `null` являются подтипами всех типов, но с `strictNullChecks: true` они требуют явного указания.