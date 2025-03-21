
Модули в TypeScript позволяют структурировать код, улучшать его читаемость и управляемость. В этой статье мы рассмотрим основные аспекты работы с модулями: экспорт компонентов, импорт, использование псевдонимов, импорт всего модуля и экспорт по умолчанию.

### Экспорт компонентов модуля

Экспорт компонентов модуля позволяет делать их доступными для использования в других частях приложения. Для экспорта используется ключевое слово `export`.

### Пример экспорта компонентов

```typescript
// mathUtils.ts
export function add(a: number, b: number): number {
    return a + b;
}

export function subtract(a: number, b: number): number {
    return a - b;
}

export const PI = 3.14;
```

В этом примере функции `add` и `subtract`, а также константа `PI` экспортируются из модуля `mathUtils`.

### Импорт компонентов модуля

Для использования экспортированных компонентов из другого модуля, необходимо импортировать их с помощью ключевого слова `import`.

### Пример импорта компонентов

```typescript
// app.ts
import { add, subtract, PI } from './mathUtils';

console.log(`Addition: ${add(5, 3)}`); // "Addition: 8"
console.log(`Subtraction: ${subtract(5, 3)}`); // "Subtraction: 2"
console.log(`PI: ${PI}`); // "PI: 3.14"
```

В этом примере функции `add` и `subtract`, а также константа `PI` импортируются из модуля `mathUtils`.

### Псевдонимы

При импорте компонентов модуля можно использовать псевдонимы для избежания конфликтов имен или для удобства.

### Пример использования псевдонимов

```typescript
// anotherMathUtils.ts
export function multiply(a: number, b: number): number {
    return a * b;
}

export function divide(a: number, b: number): number {
    return a / b;
}
```

```typescript
// app.ts
import { add, subtract, PI } from './mathUtils';
import { multiply as mul, divide as div } from './anotherMathUtils';

console.log(`Multiplication: ${mul(5, 3)}`); // "Multiplication: 15"
console.log(`Division: ${div(6, 3)}`); // "Division: 2"
console.log(`Addition: ${add(5, 3)}`); // "Addition: 8"
console.log(`Subtraction: ${subtract(5, 3)}`); // "Subtraction: 2"
console.log(`PI: ${PI}`); // "PI: 3.14"
```

В этом примере функции `multiply` и `divide` импортируются с новыми именами `mul` и `div` соответственно.

### Импорт всего модуля

Можно импортировать все экспортированные компоненты модуля под одним именем, используя `* as`.

### Пример импорта всего модуля

```typescript
// app.ts
import * as MathUtils from './mathUtils';

console.log(`Addition: ${MathUtils.add(5, 3)}`); // "Addition: 8"
console.log(`Subtraction: ${MathUtils.subtract(5, 3)}`); // "Subtraction: 2"
console.log(`PI: ${MathUtils.PI}`); // "PI: 3.14"
```

В этом примере все экспортированные компоненты из модуля `mathUtils` импортируются под именем `MathUtils`.

### Экспорт по умолчанию

Экспорт по умолчанию (`default export`) позволяет экспортировать одну сущность из модуля как основной экспорт. Это упрощает импорт этой сущности.

### Пример экспорта по умолчанию

```typescript
// greeter.ts
export default class Greeter {
    constructor(private greeting: string) {}

    greet() {
        console.log(this.greeting);
    }
}
```

### Пример импорта экспорта по умолчанию

```typescript
// main.ts
import Greeter from './greeter';

let greeter = new Greeter("Hello, TypeScript!");
greeter.greet(); // "Hello, TypeScript!"
```

В этом примере класс `Greeter` экспортируется по умолчанию из модуля `greeter`, и при импорте не требуется использовать фигурные скобки.

### Комбинирование различных видов экспорта

В одном модуле можно комбинировать различные виды экспорта: именованный экспорт и экспорт по умолчанию.

### Пример комбинированного экспорта

```typescript
// utilities.ts
export function log(message: string) {
    console.log(message);
}

export default class Logger {
    logMessage(message: string) {
        log(`Logger: ${message}`);
    }
}
```

### Пример комбинированного импорта

```typescript
// app.ts
import Logger, { log } from './utilities';

log("Hello, world!"); // "Hello, world!"
let logger = new Logger();
logger.logMessage("Hello, TypeScript!"); // "Logger: Hello, TypeScript!"
```

В этом примере функция `log` экспортируется именованным экспортом, а класс `Logger` экспортируется по умолчанию.

### Заключение

Работа с модулями в TypeScript включает в себя экспорт и импорт компонентов, использование псевдонимов, импорт всего модуля и экспорт по умолчанию. Модули помогают организовать код, улучшить его читаемость и управляемость, а также способствуют многократному использованию компонентов. Правильное использование модулей делает разработку более эффективной и структурированной.
[[https://purpleschool.ru/knowledge-base/article/working-with-modules|Источник]]