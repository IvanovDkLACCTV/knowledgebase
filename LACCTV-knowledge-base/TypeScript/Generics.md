(Due to technical issues, the search service is temporarily unavailable.)

### Дженерики в TypeScript

Дженерики (Generics) в TypeScript позволяют создавать компоненты, которые могут работать с различными типами данных, сохраняя при этом типобезопасность. Они позволяют писать более универсальный и переиспользуемый код.

#### Пример дублирования функций без дженериков

Предположим, у нас есть две функции, которые делают одно и то же, но для разных типов данных:

```typescript
function identityNumber(arg: number): number {
    return arg;
}

function identityString(arg: string): string {
    return arg;
}

console.log(identityNumber(42)); // 42
console.log(identityString("hello")); // hello
```

Здесь мы видим, что функции `identityNumber` и `identityString` делают одно и то же, но для разных типов данных. Это приводит к дублированию кода.

#### Решение проблемы с помощью дженериков

Дженерики позволяют нам написать одну функцию, которая будет работать с любым типом данных:

```typescript
function identity<T>(arg: T): T {
    return arg;
}

console.log(identity<number>(42)); // 42
console.log(identity<string>("hello")); // hello
```

Здесь `T` — это тип-параметр, который будет заменен на конкретный тип при вызове функции. Теперь функция `identity` может работать с любым типом данных.

#### Как дженерики выглядят после компиляции в JS

После компиляции TypeScript в JavaScript дженерики исчезают, так как JavaScript не поддерживает типы. Код выше будет скомпилирован в:

```javascript
function identity(arg) {
    return arg;
}

console.log(identity(42)); // 42
console.log(identity("hello")); // hello
```

Как видно, дженерики удаляются, и остается обычная JavaScript-функция.

### Type Guards в TypeScript

Type Guards — это механизм, который позволяет TypeScript сузить тип переменной внутри блока кода. Это полезно, когда у вас есть переменная, которая может быть нескольких типов, и вам нужно выполнить определенные действия в зависимости от ее типа.

Пример:

```typescript
function isString(value: any): value is string {
    return typeof value === 'string';
}

function printValue(value: string | number) {
    if (isString(value)) {
        console.log(`String: ${value}`);
    } else {
        console.log(`Number: ${value}`);
    }
}

printValue("hello"); // String: hello
printValue(42); // Number: 42
```

Здесь `isString` — это type guard, который проверяет, является ли значение строкой. Внутри блока `if` TypeScript знает, что `value` имеет тип `string`.

### Использование дженериков в интерфейсах

Дженерики можно использовать в интерфейсах для создания универсальных структур данных:

```typescript
interface Box<T> {
    value: T;
}

let numberBox: Box<number> = { value: 42 };
let stringBox: Box<string> = { value: "hello" };

console.log(numberBox.value); // 42
console.log(stringBox.value); // hello
```

Здесь интерфейс `Box` принимает тип-параметр `T`, который используется для определения типа свойства `value`.

### Использование дженериков в классах

Дженерики также можно использовать в классах:

```typescript
class Container<T> {
    private _value: T;

    constructor(value: T) {
        this._value = value;
    }

    get value(): T {
        return this._value;
    }

    set value(value: T) {
        this._value = value;
    }
}

let numberContainer = new Container<number>(42);
console.log(numberContainer.value); // 42

let stringContainer = new Container<string>("hello");
console.log(stringContainer.value); // hello
```

Здесь класс `Container` принимает тип-параметр `T`, который используется для определения типа свойства `_value`.

### Использование ключевого слова `extends` с дженериками

Ключевое слово `extends` позволяет ограничить типы, которые могут быть переданы в дженерик. Например, можно указать, что тип должен быть подтипом определенного класса или интерфейса:

```typescript
interface HasLength {
    length: number;
}

function logLength<T extends HasLength>(arg: T): void {
    console.log(arg.length);
}

logLength("hello"); // 5
logLength([1, 2, 3]); // 3
logLength({ length: 42 }); // 42
```

Здесь `T` должен быть типом, который имеет свойство `length`. Это позволяет нам вызывать `logLength` только с теми аргументами, которые имеют свойство `length`.

### Заключение

Дженерики в TypeScript — это мощный инструмент для создания универсальных и переиспользуемых компонентов. Они позволяют избежать дублирования кода и сохранить типобезопасность. Type Guards помогают сужать типы в условиях, а ключевое слово `extends` позволяет накладывать ограничения на типы, передаваемые в дженерики.