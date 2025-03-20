TypeScript является строго типизированным языком, что позволяет разработчикам точно указывать типы переменных, параметров и возвращаемых значений функций. Иногда возникает необходимость указать компилятору, что определенная переменная должна рассматриваться как конкретный тип. Для этого используется механизм преобразования типов, или type assertion. Type assertion позволяет разработчикам явно указывать тип переменной, помогая компилятору и улучшая читаемость кода.

### Основы преобразования к типу

Преобразование к типу в TypeScript не изменяет фактический тип значения, а лишь сообщает компилятору, как его следует интерпретировать. Это может быть полезно при работе с кодом, где типы могут быть неопределенными или неочевидными.

### Синтаксис преобразования типов

В TypeScript существует два основных синтаксиса для преобразования типов:

1. Угловые скобки (Angle-bracket syntax)
2. Ключевое слово `as`

Оба подхода выполняют одну и ту же функцию, но ключевое слово `as` считается более современным и предпочтительным, особенно при использовании в проектах с JSX, где угловые скобки могут вызвать конфликты.

```typescript
// Использование угловых скобок
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;

// Использование ключевого слова `as`
let someValue2: any = "this is a string";
let strLength2: number = (someValue2 as string).length;
```

### Примеры использования преобразования типов

### Преобразование объектов

Часто бывает необходимо преобразовать один объект в другой тип, особенно если мы точно знаем структуру данных.

```typescript
interface Employee {
    name: string;
    code: number;
}

let employee = <Employee>{};
employee.name = "John";
employee.code = 123;

console.log(employee);
```

### Работа с DOM элементами

Type assertion часто используется при работе с DOM, где тип элемента может быть неизвестен.

```typescript
let inputElement = document.getElementById("inputId") as HTMLInputElement;
inputElement.value = "Hello, TypeScript!";
```

### Преобразование типов при работе с API

При работе с данными, полученными от API, часто приходится преобразовывать их к определенным типам, чтобы избежать ошибок и сделать код более предсказуемым.

```typescript
interface User {
    id: number;
    name: string;
    email: string;
}

let response: any = {
    id: 1,
    name: "Alice",
    email: "alice@example.com"
};

let user: User = response as User;
console.log(user.name); // Alice
```

### Преобразование сложных типов

Type assertion может быть использовано для преобразования сложных типов, таких как объединение типов (Union Types) и пересечение типов (Intersection Types).

### Преобразование объединенных типов

```typescript
type Cat = { name: string; meow: () => void };
type Dog = { name: string; bark: () => void };

function makeNoise(animal: Cat | Dog) {
    if ((<Cat>animal).meow) {
        (<Cat>animal).meow();
    } else {
        (<Dog>animal).bark();
    }
}

let myCat: Cat = { name: "Whiskers", meow: () => console.log("Meow") };
let myDog: Dog = { name: "Rex", bark: () => console.log("Bark") };

makeNoise(myCat); // Meow
makeNoise(myDog); // Bark
```

### Преобразование пересекающихся типов

```typescript
type Person = { name: string };
type Employee = Person & { employeeId: number };

let person: Person = { name: "John" };
let employee = person as Employee;
employee.employeeId = 1234;

console.log(employee); // { name: "John", employeeId: 1234 }
```

### Ограничения преобразования типов

Type assertion не выполняет реальное преобразование типа в рантайме и не проводит проверку типов. Это лишь способ указать компилятору, как следует интерпретировать переменную. Поэтому важно использовать его осторожно и убедиться, что преобразования действительно валидны.

```typescript
let someValue: any = "this is a string";
let numValue: number = someValue as number; // Ошибка в рантайме
```

### Заключение

Type assertion в TypeScript является мощным инструментом, который позволяет разработчикам явным образом указывать типы переменных, улучшая проверку типов и делая код более безопасным и понятным. Он особенно полезен при работе с динамическими данными, такими как данные от API или DOM элементы. Однако следует использовать его с осторожностью, чтобы избежать потенциальных ошибок в рантайме.


[[https://purpleschool.ru/knowledge-base/article/type-assertion|Источник]]