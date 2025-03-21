
Декораторы в TypeScript позволяют добавлять метаданные и изменять поведение классов, методов, свойств и параметров. Иногда возникает необходимость передавать в декоратор дополнительные данные, которые известны только в момент применения декоратора. В таких случаях на помощь приходят фабрики декораторов. Фабрика декоратора — это функция, которая возвращает сам декоратор и позволяет передавать в него параметры.

### Фабрика декоратора класса

Декораторы классов могут принимать параметры через фабрики декораторов, что позволяет гибко изменять поведение класса в зависимости от переданных параметров.

### Пример фабрики декоратора класса

Создадим декоратор класса `ClassLogger`, который принимает параметр `message` и выводит его при создании экземпляра класса:

```typescript
function ClassLogger(message: string) {
  return function (constructor: Function) {
    console.log(`${message}: ${constructor.name} создан`);
  };
}

@ClassLogger('Логирование класса')
class Person {
  constructor(public name: string) {}
}

const person = new Person('Alice'); // Логирует "Логирование класса: Person создан"
```

В этом примере фабрика декоратора `ClassLogger` принимает строку `message`, которая выводится в консоль при создании экземпляра класса `Person`.

### Фабрика декоратора свойства

Фабрики декораторов свойств позволяют передавать дополнительные данные, которые могут использоваться для модификации поведения свойств.

### Пример фабрики декоратора свойства

Создадим декоратор свойства `PropertyLogger`, который будет логировать доступ к свойству с указанием имени свойства и переданного параметра `message`:

```typescript
function PropertyLogger(message: string) {
  return function (target: any, propertyKey: string) {
    let value = target[propertyKey];

    const getter = () => {
      console.log(`${message} - Получение значения ${propertyKey}: ${value}`);
      return value;
    };

    const setter = (newValue) => {
      console.log(`${message} - Установка значения ${propertyKey} на ${newValue}`);
      value = newValue;
    };

    Object.defineProperty(target, propertyKey, {
      get: getter,
      set: setter,
      enumerable: true,
      configurable: true
    });
  };
}

class User {
  @PropertyLogger('Логирование свойства')
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}

const user = new User('Alice');
console.log(user.name); // Логирует получение значения
user.name = 'Bob'; // Логирует установку нового значения
```

В этом примере фабрика декоратора `PropertyLogger` добавляет логирование для свойства `name` класса `User`, используя переданное сообщение `message`.

### Фабрика декоратора метода

Фабрики декораторов методов позволяют передавать параметры, которые могут использоваться для изменения поведения методов.

### Пример фабрики декоратора метода

Создадим декоратор метода `MethodLogger`, который будет логировать вызов метода с указанием имени метода и переданного параметра `message`:

```typescript
function MethodLogger(message: string) {
  return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    const originalMethod = descriptor.value;

    descriptor.value = function (...args: any[]) {
      console.log(`${message} - Вызов метода ${propertyKey} с аргументами: ${JSON.stringify(args)}`);
      const result = originalMethod.apply(this, args);
      console.log(`${message} - Результат: ${result}`);
      return result;
    };
  };
}

class Calculator {
  @MethodLogger('Логирование метода')
  add(a: number, b: number): number {
    return a + b;
  }
}

const calculator = new Calculator();
calculator.add(2, 3); // Логирует вызов метода и результат
```

В этом примере фабрика декоратора `MethodLogger` добавляет логирование для метода `add` класса `Calculator`, используя переданное сообщение `message`.

### Заключение

Фабрики декораторов в TypeScript предоставляют мощный инструмент для передачи параметров в декораторы и гибкой модификации поведения классов, свойств и методов. Использование фабрик декораторов позволяет создавать более универсальные и переиспользуемые декораторы, которые могут адаптироваться к различным условиям в зависимости от переданных параметров.
[[https://purpleschool.ru/knowledge-base/article/decorator-factories|Источник]]