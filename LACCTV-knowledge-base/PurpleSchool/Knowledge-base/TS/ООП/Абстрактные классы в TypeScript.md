Абстрактные классы в TypeScript представляют собой важный инструмент объектно-ориентированного программирования. Они определяются с использованием ключевого слова `abstract` и служат для создания базовых классов, которые не могут быть инстанцированы напрямую. Вместо этого абстрактные классы предоставляют общий интерфейс и могут содержать как реализованные методы, так и абстрактные методы, которые должны быть реализованы в классах-наследниках.

### Объявление абстрактного класса

Абстрактный класс объявляется с использованием ключевого слова `abstract` перед ключевым словом `class`. Такой класс может содержать абстрактные методы, которые не имеют реализации и должны быть реализованы в производных классах.

### Пример абстрактного класса

```typescript
abstract class Animal {
    abstract makeSound(): void; // Абстрактный метод

    move(): void {
        console.log("The animal moves.");
    }
}
```

В данном примере `Animal` — абстрактный класс, содержащий абстрактный метод `makeSound` и обычный метод `move`.

### Реализация абстрактных методов

Когда класс наследует абстрактный класс, он обязан реализовать все абстрактные методы родительского класса. Если этого не сделать, TypeScript выдаст ошибку.

### Пример реализации абстрактного метода

```typescript
class Dog extends Animal {
    makeSound(): void {
        console.log("Bark");
    }
}

let dog = new Dog();
dog.makeSound(); // "Bark"
dog.move(); // "The animal moves."
```

В этом примере класс `Dog` наследует абстрактный класс `Animal` и реализует метод `makeSound`.

### Создание абстрактного класса с полями и методами

Абстрактные классы могут содержать поля и методы с реализацией, которые будут наследоваться производными классами.

### Пример абстрактного класса с полями и методами

```typescript
abstract class Vehicle {
    protected brand: string;

    constructor(brand: string) {
        this.brand = brand;
    }

    abstract startEngine(): void; // Абстрактный метод

    drive(): void {
        console.log(`${this.brand} is driving.`);
    }
}

class Car extends Vehicle {
    constructor(brand: string) {
        super(brand);
    }

    startEngine(): void {
        console.log(`${this.brand} engine started.`);
    }
}

let car = new Car("Toyota");
car.startEngine(); // "Toyota engine started."
car.drive(); // "Toyota is driving."
```

В этом примере абстрактный класс `Vehicle` содержит поле `brand`, абстрактный метод `startEngine` и обычный метод `drive`. Класс `Car` наследует `Vehicle` и реализует абстрактный метод `startEngine`.

### Использование абстрактных классов для создания общих интерфейсов

Абстрактные классы полезны для создания общих интерфейсов, которые могут быть использованы несколькими классами. Это позволяет избежать дублирования кода и обеспечивает консистентность в реализации.

### Пример использования абстрактного класса для создания общего интерфейса

```typescript
abstract class Shape {
    abstract area(): number;

    describe(): void {
        console.log(`This shape has an area of ${this.area()} square units.`);
    }
}

class Rectangle extends Shape {
    private width: number;
    private height: number;

    constructor(width: number, height: number) {
        super();
        this.width = width;
        this.height = height;
    }

    area(): number {
        return this.width * this.height;
    }
}

class Circle extends Shape {
    private radius: number;

    constructor(radius: number) {
        super();
        this.radius = radius;
    }

    area(): number {
        return Math.PI * this.radius ** 2;
    }
}

let rectangle = new Rectangle(10, 20);
rectangle.describe(); // "This shape has an area of 200 square units."

let circle = new Circle(5);
circle.describe(); // "This shape has an area of 78.53981633974483 square units."
```

В этом примере абстрактный класс `Shape` определяет метод `area` и реализованный метод `describe`. Классы `Rectangle` и `Circle` наследуют `Shape` и реализуют метод `area`.

### Преимущества использования абстрактных классов

1. **Повторное использование кода**: Абстрактные классы позволяют создавать общие функции и свойства, которые могут быть повторно использованы в производных классах.
2. **Инкапсуляция логики**: Логика может быть инкапсулирована в абстрактных классах и использоваться в производных классах без необходимости дублирования кода.
3. **Обеспечение консистентности**: Производные классы обязаны реализовать абстрактные методы, что гарантирует наличие определенной функциональности.

### Заключение

Абстрактные классы в TypeScript являются мощным инструментом для создания базовых классов, которые задают структуру и функциональность, но не могут быть использованы напрямую. Они позволяют создавать обобщенные интерфейсы, повторно использовать код и обеспечивать консистентность в реализации производных классов. Это делает код более организованным, читаемым и легко поддерживаемым, что особенно важно в больших и сложных проектах.

[[https://purpleschool.ru/knowledge-base/article/abstract-classes-methods-and-fields|Источник]]