

Литеральные типы позволяют задавать переменной **строго определённые значения**. В TypeScript можно использовать **строковые**, **числовые** и **логические** литеральные типы.

---

### 📊 **1. Строковые литеральные типы**

Ограничивают переменную конкретными строковыми значениями.

```typescript
type Direction = "left" | "right" | "up" | "down";

function move(direction: Direction) {
  console.log(`Moving ${direction}`);
}

move("left");  // ✅ OK
move("right"); // ✅ OK
move("back");  // ❌ Ошибка: значение не входит в Direction
```

> 📝 **Когда использовать?**  
> Когда значение переменной должно быть ограничено строго определёнными строками (например, направления, статусы, роли).

---

### 🔢 **2. Числовые литеральные типы**

Ограничивают переменную конкретными числовыми значениями.

```typescript
type StatusCode = 200 | 400 | 404 | 500;

function handleResponse(code: StatusCode) {
  console.log(`Status: ${code}`);
}

handleResponse(200); // ✅ OK
handleResponse(401); // ❌ Ошибка: не входит в StatusCode
```

> 📝 **Когда использовать?**  
> Если функция принимает фиксированные числовые коды (например, коды HTTP-статусов).

---

### 🔘 **3. Логические литеральные типы**

Можно ограничить переменную `true` или `false`.

```typescript
type Toggle = true | false;

function setDarkMode(mode: Toggle) {
  console.log(mode ? "Dark Mode ON" : "Dark Mode OFF");
}

setDarkMode(true);  // ✅ OK
setDarkMode(false); // ✅ OK
setDarkMode("yes"); // ❌ Ошибка
```

> 📝 **Когда использовать?**  
> Если функция принимает **строго true или false**, например, для включения или выключения функции.

---

### 🛠️ **4. Сочетание литеральных типов и `Union`**

Литеральные типы часто используют с **объединением типов** (`|`), чтобы создать гибкие и безопасные варианты.

```typescript
type ButtonSize = "small" | "medium" | "large";
type ButtonColor = "red" | "blue";

type Button = {
  size: ButtonSize;
  color: ButtonColor;
};

const myButton: Button = {
  size: "medium",
  color: "blue",
};
```

---

### 📋 **5. Литеральные типы и `as const`**

`as const` делает объект **неизменяемым** и автоматически выводит **литеральные типы**.

```typescript
const ROLES = {
  ADMIN: "admin",
  USER: "user",
} as const;

type Role = typeof ROLES[keyof typeof ROLES];

function setRole(role: Role) {
  console.log(`Role: ${role}`);
}

setRole("admin"); // ✅ OK
setRole("guest"); // ❌ Ошибка
```

---

### 🔎 **6. Применение с перечислениями (Enum vs Literal Types)**

Литеральные типы могут заменить `enum` в некоторых случаях, поскольку они компактнее и безопаснее.

✅ **С использованием `enum`:**

```typescript
enum Status {
  Success = "success",
  Error = "error",
}

function logStatus(status: Status) {
  console.log(status);
}

logStatus(Status.Success);
```

✅ **С использованием литеральных типов:**

```typescript
type Status = "success" | "error";

function logStatus(status: Status) {
  console.log(status);
}

logStatus("success"); // ✅ OK
```

> 📝 **Когда использовать литеральные типы вместо `enum`?**

- Когда не требуется автоматическое числовое значение.
- Когда код должен быть компактнее.

---

### 📚 **7. Литеральные типы и перегрузка функций**

Использование литеральных типов позволяет точно описать функции с разным поведением.

```typescript
type Shape = "circle" | "square";

function getArea(shape: "circle", radius: number): number;
function getArea(shape: "square", size: number): number;
function getArea(shape: Shape, value: number): number {
  return shape === "circle" ? Math.PI * value ** 2 : value * value;
}

console.log(getArea("circle", 10)); // ✅ OK
```

---

### 📦 **8. Литеральные типы и типизация CSS**

Литеральные типы полезны при работе с CSS, где нужны фиксированные значения.

```typescript
type Display = "block" | "inline" | "flex" | "grid";

const style: Record<string, Display> = {
  header: "flex",
  footer: "block",
};

console.log(style.header); // "flex"
```

---

### ✅ **Итоги:**

- **Строковые, числовые и логические литеральные типы** ограничивают переменную конкретными значениями.
- Используются для **строго фиксированных наборов значений** (например, `status`, `role`, `direction`).
- `as const` позволяет **автоматически** выводить литеральные типы.
- Удобны при работе с **перегрузками функций** и **CSS-свойствами**.