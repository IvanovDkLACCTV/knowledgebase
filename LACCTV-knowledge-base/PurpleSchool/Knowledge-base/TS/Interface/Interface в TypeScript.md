## Введение

Интерфейсы представляют собой ключевой элемент языка, позволяя разработчикам определять структуры объектов, задавать типы данных и обеспечивать четкую спецификацию взаимодействия компонентов в приложении. В этой статье мы рассмотрим интерфейсы в **TypeScript** подробно, начиная с основ и заканчивая продвинутыми сценариями использования. Для начала давайте зададим тип User

## Интерфейсы объектов

```typescript
interface IUser {
  id: number;
  name: string;
  surname: string;
}
```

В этом примере мы описали тип пользователя. Теперь давайте реализуем его. Создадим объект User

```typescript
const Max: IUser = {
  id: 1,
  name: 'Max',
  surname: 'Smith',
};
```

Мы явно узазали, что объект имеет **user** тип **IUser**, это означает, что объект **user** обязан содержать поле id, name и surname

```typescript
const Mary: IUser = {
  id: 1,
  name: 'Mary',
};
// Property 'surname' is missing in type '{ id: number; name: string; }' but required in type 'IUser'
```

Мы можем использовать интерфейсы внутри других интерфейсов, как тип. Рассмотрим пример:

```typescript
interface IUser {
  id: number;
  name: string;
}
interface IPost {
  text: string;
  author: IUser;
}

const post: IPost = {
  text: 'Доброе утро, подписчики. Я наконец пофиксил баг)) 😵😡🤧',
  author: {
    id: 1,
    name: 'Вячеслав',
  },
};
```

Параметры методов и функций также могут представлять интерфейсы. Также можно возвращать объекты интерфейса:

```typescript
interface IUser {
  id: number;
  name: string;
  surname: string;
}

const Max: IUser = {
  id: 1,
  name: 'Max',
  surname: 'Smith',
};

function changeUserName(user: IUser, name: string): IUser {
  user.name = name;
  return user;
}
const changeUserSurname = (user: IUser, surname: string): IUser => {
  user.surname = surname;
  return user;
};

console.log(changeUserName(Max, 'Will')); // { id: 1, name: "Will", surname: "Smith" }
console.log(changeUserSurname(Max, 'Holland')); // { id: 1, name: "Max", surname: "Holland" }
```

## Необязательные свойства

Одной из удивительных особенностей интерфейсов в TypeScript является возможность определения необязательных свойств. Это позволяет нам описывать структуры объектов, где некоторые свойства могут отсутствовать, не нарушая статическую типизацию.

Давайте рассмотрим пример:

```typescript
interface IUser {
  id: number;
  name: string;
  surname?: string;
}

const Tom = {
  id: 1,
  name: 'Max',
};
// Тут нет ошибки, так как ключ surname в типе IUser необязателен
```

## Свойства только для чтения

`readonly` в интерфейсах предоставляет механизм для создания объектов с неизменяемыми свойствами. Это означает, что после установки значения свойства при создании объекта, оно не может быть изменено. Давайте рассмотрим, как использовать readonly на практике.

```typescript
interface IItem {
  readonly id: number;
  name: string;
  price: number;
}

const headphones: IItem = {
  id: 1,
  name: 'headphones',
  price: 299,
};

headphones.id = 2; // Cannot assign to 'id' because it is a read-only property.
```

## Расширение интерфейса

Расширение позволяет добавлять новые свойства или методы к уже существующему интерфейсу без изменения исходного кода. Давайте рассмотрим этот механизм на практике.

```typescript
interface IUser {
  name: string;
  age: number;
}

interface AdvancedUser extends IUser {
  email: string;
}

const Max: AdvancedUser = {
  name: 'Max',
  age: 18,
  email: 'maxPupkin@test.test',
};
```

В этом примере мы начинаем с исходного интерфейса **IUse**, который содержит базовые свойства. Затем мы создаем расширенный интерфейс **AdvancedUser**, добавляя новое свойства **email**

## Интерфейсы классов

В TypeScript мы можем использовать интерфейсы не только для описания структуры объектов, но и для определения формата классов. Это открывает дополнительные возможности для создания более строгих контрактов между классами и улучшения читаемости кода. Давайте рассмотрим, как работают интерфейсы классов. Определение Интерфейса Класса:

```typescript
// Интерфейс класса "Транспортное Средство"
interface Transportation {
  start(): void;
  stop(): void;
  getSpeed(): number;
}

// Реализация интерфейса в классе "Автомобиль"
class Car implements Transportation {
  private speed: number = 0;

  start() {
    console.log('Автомобиль начал движение.');
    this.speed = 10;
  }

  stop() {
    console.log('Автомобиль остановлен.');
    this.speed = 0;
  }

  getSpeed() {
    return this.speed;
  }
}

// Пример использования
let car = new Car();
car.start(); // Автомобиль начал движение.
console.log(`Текущая скорость: ${car.getSpeed()}`); // 10
car.stop(); // Автомобиль остановлен.
```

В этом примере у нас есть интерфейс **Transportation**, который описывает общие методы для транспортных средств. Затем мы создаем класс **Car**, который реализует этот интерфейс, предоставляя конкретную реализацию методов. Обратите внимание, что в классе должны быть определены все методы, указанные в интерфейсе.

### Расширение Интерфейса Класса

```typescript
// Интерфейс класса "Транспортное Средство"
interface Transportation {
  start(): void;
  stop(): void;
  getSpeed(): number;
}
// Расширение интерфейса для добавления нового метода
interface TransportationLighting extends Transportation {
  headlightsOn(): void;
}

// Расширенная реализация интерфейса в классе "Мотоцикл"
class Motorcycle implements TransportationLighting {
  private speed: number = 0;
  private enableHeadlamp: boolean = false;

  start() {
    console.log('Мотоцикл начал движение.');
    this.speed = 8;
  }

  stop() {
    console.log('Мотоцикл остановлен.');
    this.speed = 0;
  }

  getSpeed() {
    return this.speed;
  }

  headlightsOn() {
    console.log('Фары включены.');
    this.enableHeadlamp = true;
  }
}

// Пример использования
let motorcycle = new Motorcycle();
motorcycle.start(); // Мотоцикл начал движение.
motorcycle.headlightsOn(); // Фары включены.
console.log(`Текущая скорость: ${motorcycle.getSpeed()}`); //  10
motorcycle.stop(); // Мотоцикл остановлен.
```

В этом примере мы расширяем интерфейс, добавляя новый метод **headlightsOn** в интерфейс **TransportationLighting**. Затем мы создаем класс **Motorcycle**, который реализует этот расширенный интерфейс, предоставляя новый функционал. Таким образом, интерфейсы классов позволяют легко добавлять и изменять функциональность классов в соответствии с обновляющимися требованиями.

## Интерфейсы функций

В TypeScript мы можем использовать интерфейсы для описания формата функций. Это предоставляет четкие правила о том, как функция должна быть структурирована, что обеспечивает статическую типизацию при вызове функций. Давайте рассмотрим, как работают интерфейсы функций на примерах:

```typescript
interface sayHi {
  (name: string, timeOfDay: 'утро' | 'день' | 'вечер' | 'ночь'): string;
}

const greet: sayHi = function (name, timeOfDay) {
  return `Доброе ${timeOfDay}, ${name}!`;
};

console.log(greet('Алиса', 'утро')); // Доброе утро, Алиса!
```

## Интерфейсы массивов

В TypeScript мы можем использовать интерфейсы для описания структуры массивов, предоставляя явные правила по типам элементов и их порядку. Рассмотрим несколько примеров интерфейсов для массивов.

```typescript
interface ArrayOfStrings {
  [index: number]: string;
}

// Пример использования
const myColors: ArrayOfStrings = ['красный', 'зеленый', 'синий'];
console.log(myColors[0]); // красный
```

## Заключение

В этой статье мы глубоко погрузились в мир интерфейсов в TypeScript и их различные аспекты. Использование интерфейсов обогащает разработку, предоставляя мощные инструменты для описания структур данных, функций и классов.

Интерфейсы в TypeScript предоставляют не только читаемость кода, но и статическую типизацию, что является ключевым элементом для создания надежных и поддерживаемых приложений. Мы рассмотрели различные сценарии использования интерфейсов, начиная от описания объектов и массивов до расширения классов и определения формата функций.

Преимущества использования интерфейсов становятся особенно заметными в средних и крупных проектах, где строгая структура данных и четкие контракты между компонентами играют важную роль.

Запомните, что TypeScript дает возможность писать код, который более предсказуем, легче поддерживать и масштабировать. Внедрение интерфейсов в ваш код — это не только путь к улучшению его качества, но и шаг к созданию более структурированных и надежных приложений. Надеюсь, эта статья помогла вам лучше понять и использовать интерфейсы в TypeScript. Удачи в вашем кодинге! 🚀

[[https://purpleschool.ru/knowledge-base/article/interface|Источник]]