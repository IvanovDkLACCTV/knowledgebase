#### 📚 **1. Функции с типами и без них**

В **TypeScript** можно объявлять функции с явным указанием типов или без него:

✅ **Функция без явного указания типа (Type Inference):** TypeScript сам определяет типы на основе переданных аргументов и возвращаемого значения.
```typescript
function add(a, b) {
  return a + b; // Тип вывода: number | string (зависит от переданных значений)
}
```

✅ **Функция с явным указанием типов:**

```typescript
function add(a: number, b: number): number {
  return a + b;
}
```

✅ **Функция, принимающая `Union` тип:** Union (объединение) позволяет использовать несколько типов.

```typescript
function printId(id: number | string): void {
  console.log(`ID: ${id}`);
}

printId(42);       // OK
printId("abc123"); // OK
```

✅ **Функция, использующая `interface`:** Интерфейсы полезны для описания структуры объектов.
```typescript
interface User {
  id: number;
  name: string;
}

function greetUser(user: User): void {
  console.log(`Hello, ${user.name}!`);
}

greetUser({ id: 1, name: "Alice" }); // OK
```

#### 📊 **2. Типы vs Интерфейсы: Когда что использовать?**

|🔍 Характеристика|`type`|`interface`|
|---|---|---|
|**Для чего использовать**|Примитивы, объединение типов, функции|Объекты и классы, расширение структур|
|**Расширение (Extends)**|Использует `&` (intersection)|Использует `extends`|
|**Совместимость (Merging)**|Не поддерживает|Поддерживает (можно дополнять)|
|**Производительность**|Быстрее в сложных типах|Медленнее при глубоком наследовании|
|**Keyof (извлечение ключей)**|Работает корректно|Работает корректно|
|**Рекомендуется**|Сложные типы, функции|Объекты и классы|

##### 🔎 **Расширение интерфейсов (`extends`):**

Позволяет создать новый интерфейс на основе существующего.
```typescript
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

const myDog: Dog = {
  name: "Rex",
  breed: "Labrador",
};
```

##### ➕ **Пересечение типов (*&*):**

Объединяет несколько типов в один.
```typescript
type Animal = {
  name: string;
};

type Dog = Animal & {
  breed: string;
};

const myDog: Dog = {
  name: "Rex",
  breed: "Labrador",
};
```

##### 📌 **Дополнение интерфейсов (Declaration Merging):**

Интерфейсы можно расширять повторным объявлением.
```typescript
interface User {
  id: number;
}

interface User {
  name: string;
}

const user: User = {
  id: 1,
  name: "Alice",
}
```

> Типы же можно объявлять только один раз.

#### 🔄 **3. Каст типов (*as*):**

Используется для явного приведения типов.

✅ **Пример с `as`:**
```typescript
let value: unknown = "Hello, world!";
let str: string = value as string;
console.log(str.toUpperCase());
```
✅ **Каст к DOM-элементам:**
```typescript
const input = document.querySelector("input") as HTMLInputElement;
input.value = "Typed Input";
```

---
##### 🎨 **Пример с CSS-свойствами:**

Пример при работе с **Canvas**:
```typescript
const myCanvas = document.getElementById('canvas') as HTMLCanvasElement
```

Иногда при работе с CSS-стилями требуется каст к `CSSProperties`.
```typescript
import { CSSProperties } from "react";

const containerStyle: CSSProperties = {
  display: "flex",
  justifyContent: "center",
  padding: "20px",
};

function App() {
  return <div style={containerStyle}>Hello, TypeScript!</div>;
}
```

Если требуется указать нестандартное свойство:
```typescript
const customStyle = {
  "--main-color": "blue",
} as CSSProperties;
```

💡 **Итог:**

- Старайся использовать `interface` там, где это возможно.
- Используй `type` для примитивов, объединения и функций.
- `extends` расширяет интерфейсы, а `&` объединяет типы.
- `as` применяется для приведения к конкретному типу.