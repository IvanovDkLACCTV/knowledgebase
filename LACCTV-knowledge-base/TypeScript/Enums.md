### 📚 **1. Что такое `enum` в TypeScript и зачем он нужен?**

`enum` (перечисление) в TypeScript — это удобная структура, которая позволяет присваивать **именованные константы**. В отличие от **литеральных типов**, `enum` создаёт объект в JavaScript-коде, который доступен **во время выполнения (runtime)**.

---

## 📊 **Преимущества `enum` перед литеральными типами:**

|Особенность|`enum`|Литеральный тип (`type`)|
|---|---|---|
|✅ **Доступ в runtime**|Доступен как объект|Нет, удаляется после компиляции|
|✅ **Обратный маппинг**|Для числовых `enum` доступен|Нет|
|✅ **Расширяемость**|Можно объединять (гетерогенные `enum`)|Только объединение через `|
|✅ **Использование в объектах**|Можно использовать как ключи и значения|Только значения|
|✅ **Оптимизация кода**|Можно использовать `const enum`|Нет, всегда создаёт объект|

---

## 📌 **1. Числовые `enum`**

В числовых `enum` значения задаются автоматически, начиная с `0`, если не указать другое.

```typescript
enum Status {
  Pending,     // 0
  InProgress,  // 1
  Completed,   // 2
}

console.log(Status.Pending);    // ✅ 0
console.log(Status[1]);         // ✅ "InProgress"

// Начать с произвольного числа:
enum Role {
  User = 1,
  Admin,    // 2 (автоматически увеличивается)
  SuperAdmin, // 3
}

console.log(Role.Admin);         // ✅ 2
console.log(Role["SuperAdmin"]); // ✅ 3
```

---

## 📌 **2. Строковые `enum`**

Значения задаются явно, автоматического увеличения нет.

```typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}

console.log(Direction.Up);       // ✅ "UP"
console.log(Direction["Right"]); // ✅ "RIGHT"
```

---

## 📌 **3. Гетерогенные `enum`**

Комбинируют **числовые и строковые значения**, но так делать стоит осторожно — это усложняет код.

```typescript
enum Mix {
  NumberValue = 1,
  StringValue = "STRING",
}

console.log(Mix.NumberValue);   // ✅ 1
console.log(Mix.StringValue);   // ✅ "STRING"
```

---

## 📌 **4. Расчётные (вычисляемые) `enum`**

Можно использовать **выражения** и **функции** для значений.

```typescript
const getDynamicValue = () => new Date().getFullYear();

enum DynamicEnum {
  CurrentYear = getDynamicValue(), // Вызов функции
  NextYear = CurrentYear + 1,      // Выражение
}

console.log(DynamicEnum.CurrentYear); // ✅ Текущий год (например, 2025)
console.log(DynamicEnum.NextYear);    // ✅ Следующий год (2026)
```

---

## 📌 **5. Использование `enum` как объекта**

`enum` — это объект, его можно перебирать и использовать как структуру данных.

```typescript
enum Colors {
  Red = "red",
  Green = "green",
  Blue = "blue",
}

const palette: Record<Colors, string> = {
  [Colors.Red]: "#ff0000",
  [Colors.Green]: "#00ff00",
  [Colors.Blue]: "#0000ff",
};

console.log(palette[Colors.Red]); // ✅ "#ff0000"
```

---

## 📌 **6. Как получить строковое значение из `enum`**

Можно использовать **Object.values()** или **перебор `for...in`**.

```typescript
enum Fruits {
  Apple = "apple",
  Banana = "banana",
  Orange = "orange",
}

const fruitValues = Object.values(Fruits);
console.log(fruitValues); // ✅ ["apple", "banana", "orange"]
```

---
## 📌 **7. Обратный маппинг**

Обратный маппинг (`Reverse Mapping`) доступен **только для числовых `enum`**. Он позволяет получить имя `enum` по значению.

---

### 📌 **Пример обратного маппинга:**

```typescript
enum Status {
  Active = 1,
  Inactive,
  Pending,
}

console.log(Status.Active);  // ✅ 1
console.log(Status[1]);      // ✅ "Active"

console.log(Status.Pending); // ✅ 3
console.log(Status[3]);      // ✅ "Pending"
```

👉 **Как это работает:** TypeScript создаёт **двунаправленный объект**, где есть и прямое, и обратное соответствие.

---

### 📜 **Как выглядит обратный маппинг в JavaScript:**

```javascript
"use strict";
var Status;
(function (Status) {
    Status[Status["Active"] = 1] = "Active";
    Status[Status["Inactive"] = 2] = "Inactive";
    Status[Status["Pending"] = 3] = "Pending";
})(Status || (Status = {}));

console.log(Status.Active); // 1
console.log(Status[1]);     // "Active"
```

---

### ❌ **Почему не работает с строковыми `enum`?**

Строковые `enum` не поддерживают обратный маппинг, потому что строки не могут быть ключами и значениями одновременно.

```typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
}

console.log(Direction.Up);      // ✅ "UP"
console.log(Direction["UP"]);   // ❌ undefined (нет обратного маппинга)
```

👉 В JavaScript это преобразуется в простой объект:

```javascript
"use strict";
var Direction = {
  Up: "UP",
  Down: "DOWN"
};
```

---

### 📌 **Пример использования обратного маппинга:**

Можно проверить, существует ли значение в `enum`:

```typescript
enum ErrorCode {
  NotFound = 404,
  ServerError = 500,
}

function getErrorName(code: number): string {
  return ErrorCode[code] || "Unknown Error";
}

console.log(getErrorName(404)); // ✅ "NotFound"
console.log(getErrorName(400)); // ✅ "Unknown Error"
```

> 👉 Используй **обратный маппинг** для числовых `enum`, если нужно получать **имя по значению**.
---



## 🧰 **2. Как `enum` работает в runtime и `const enum`**

### 🔍 **Как работает обычный `enum`:**

TypeScript **генерирует объект** в JavaScript:

```typescript
enum Status {
  Active = 1,
  Inactive,
}
```

✅ В JavaScript:

```javascript
"use strict";
var Status;
(function (Status) {
    Status[Status["Active"] = 1] = "Active";
    Status[Status["Inactive"] = 2] = "Inactive";
})(Status || (Status = {}));
```

---

### 📌 **Что такое `const enum` и зачем он нужен?**

`const enum` **не создаёт объект** в JavaScript — он **инлайнится** (подставляется напрямую).

```typescript
const enum Status {
  Active = 1,
  Inactive = 2,
}

console.log(Status.Active); // ✅ 1 (просто число)
```

✅ В JavaScript:

```javascript
"use strict";
console.log(1); // Вместо объекта
```

✅ **Когда использовать `const enum`?**

- Когда важна **производительность** (уменьшает размер кода).
- Если **не нужен доступ в runtime** (например, для CSS-классов или API-кодов).

---

## 🔥 **3. Пример с `never` и `switch-case`**

Используем `never`, чтобы убедиться, что все варианты `enum` обработаны:

```typescript
enum PaymentStatus {
  Pending = "pending",
  Completed = "completed",
  Failed = "failed",
}

function handlePayment(status: PaymentStatus): void {
  switch (status) {
    case PaymentStatus.Pending:
      console.log("Ожидание оплаты...");
      break;
    case PaymentStatus.Completed:
      console.log("Оплата успешна!");
      break;
    case PaymentStatus.Failed:
      console.log("Ошибка оплаты.");
      break;
    default:
      // Защита от неучтённых случаев
      const _exhaustiveCheck: never = status;
      throw new Error(`Неизвестный статус: ${status}`);
  }
}

handlePayment(PaymentStatus.Pending); // ✅ "Ожидание оплаты..."
// handlePayment("unknown"); // ❌ Ошибка на этапе компиляции
```

---

## 📌 **Краткое сравнение: Enum vs Literal Types**

|Характеристика|`enum`|Литеральный тип (`type`)|
|---|---|---|
|✅ **В runtime**|Доступен как объект|Нет (удаляется после компиляции)|
|✅ **Обратный маппинг**|Только для числовых `enum`|Нет|
|✅ **Производительность**|`const enum` не создаёт объект|Всегда инлайнится (быстрее)|
|✅ **Использование в switch**|Удобно для исчерпывающих проверок|Аналогично|
|✅ **Типобезопасность**|Высокая с `never`-проверкой|Высокая|
|✅ **Гибкость**|Можно комбинировать типы|Только объединение через `|

👉 Используй:

- **`enum`**, если нужен **runtime** (например, статусы, коды ошибок).
- **`const enum`**, если важна **производительность**.
- **Литеральные типы**, если нужен **строгий контроль** на уровне компиляции.