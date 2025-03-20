Массивы являются одной из самых часто используемых структур данных в программировании. В TypeScript массивы определяются с помощью квадратных скобок `[]` и являются строго типизированными, что обеспечивает дополнительные проверки типов и делает код более надежным.

### Определение массивов

В TypeScript массивы могут быть определены двумя способами:

1. Использование квадратных скобок `[]`.
2. Использование обобщенного типа `Array<type>`.

Оба подхода эквивалентны и могут быть использованы в зависимости от предпочтений разработчика.

### Пример использования квадратных скобок

```typescript
let numbers: number[] = [1, 2, 3, 4, 5];
let strings: string[] = ["hello", "world"];
```

### Пример использования обобщенного типа `Array<type>`

```typescript
let numbers: Array<number> = [1, 2, 3, 4, 5];
let strings: Array<string> = ["hello", "world"];
```

### Основные операции с массивами

Массивы в TypeScript поддерживают стандартные операции, такие как добавление, удаление, поиск и итерация элементов.

### Добавление элементов

Для добавления элементов в массив можно использовать методы `push` и `unshift`.

```typescript
let numbers: number[] = [1, 2, 3];

// Добавление элемента в конец массива
numbers.push(4);
console.log(numbers); // [1, 2, 3, 4]

// Добавление элемента в начало массива
numbers.unshift(0);
console.log(numbers); // [0, 1, 2, 3, 4]
```

### Удаление элементов

Для удаления элементов из массива можно использовать методы `pop`, `shift` и `splice`.

```typescript
let numbers: number[] = [1, 2, 3, 4, 5];

// Удаление элемента из конца массива
numbers.pop();
console.log(numbers); // [1, 2, 3, 4]

// Удаление элемента из начала массива
numbers.shift();
console.log(numbers); // [2, 3, 4]

// Удаление элементов по индексу
numbers.splice(1, 1); // Удаление одного элемента начиная с индекса 1
console.log(numbers); // [2, 4]
```

### Поиск элементов

Для поиска элементов в массиве можно использовать методы `indexOf` и `includes`.

```typescript
let numbers: number[] = [1, 2, 3, 4, 5];

// Поиск индекса элемента
let index = numbers.indexOf(3);
console.log(index); // 2

// Проверка наличия элемента
let contains = numbers.includes(4);
console.log(contains); // true
```

### Итерация по массиву

Для итерации по массиву можно использовать циклы `for`, `for...of`, а также методы `forEach`, `map`, `filter` и другие.

```typescript
let numbers: number[] = [1, 2, 3, 4, 5];

// Цикл for
for (let i = 0; i < numbers.length; i++) {
    console.log(numbers[i]);
}

// Цикл for...of
for (let num of numbers) {
    console.log(num);
}

// Метод forEach
numbers.forEach(num => console.log(num));

// Метод map
let squaredNumbers = numbers.map(num => num * 2);
console.log(squaredNumbers); // [2, 4, 6, 8, 10]
```

### Массивы сложных типов

Массивы в TypeScript могут содержать объекты, другие массивы и даже функции.

### Массивы объектов

```typescript
interface Person {
    name: string;
    age: number;
}

let people: Person[] = [
    { name: "Alice", age: 25 },
    { name: "Bob", age: 30 }
];

people.forEach(person => console.log(`${person.name} is ${person.age} years old`));
```

### Массивы массивов

```typescript
let matrix: number[][] = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

for (let row of matrix) {
    console.log(row);
}
```

### Массивы функций

```typescript
let operations: ((a: number, b: number) => number)[] = [
    (a, b) => a + b,
    (a, b) => a - b,
    (a, b) => a * b
];

let result1 = operations[0](2, 3); // 5
let result2 = operations[1](5, 3); // 2
let result3 = operations[2](4, 3); // 12

console.log(result1, result2, result3);
```

### Кортежи (Tuples)

TypeScript поддерживает специальные виды массивов, называемые кортежами, которые позволяют хранить элементы разного типа фиксированной длины.

### Пример использования кортежей

```typescript
let tuple: [string, number] = ["hello", 42];
console.log(tuple[0]); // hello
console.log(tuple[1]); // 42

// Ошибка: Нельзя добавить элементы в кортеж, если они не соответствуют объявленным типам
// tuple.push(true); // Ошибка
```

### Ограничения и особенности

TypeScript обеспечивает строгую типизацию массивов, что помогает избежать ошибок, связанных с некорректными операциями над массивами. Однако важно помнить, что TypeScript выполняет проверки типов только на этапе компиляции. В рантайме все массивы ведут себя так же, как и в JavaScript.

### Пример ограничения типов

```typescript
let numbers: number[] = [1, 2, 3];
// Ошибка компиляции: Невозможно присвоить значение типа 'string' переменной типа 'number[]'
// numbers.push("hello");
```

### Заключение

Массивы в TypeScript являются мощным инструментом для работы с упорядоченными наборами данных. Строгая типизация массивов позволяет избежать множества ошибок и делает код более предсказуемым. Использование массивов сложных типов, кортежей и методов работы с массивами позволяет создавать гибкие и мощные приложения. Благодаря встроенным возможностям TypeScript разработчики могут эффективно управлять данными и создавать надежные программные решения.

[[https://purpleschool.ru/knowledge-base/article/arrays|Источник]]