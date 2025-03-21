
Пространства имен (namespaces) в TypeScript предназначены для организации больших программ. Они помогают структурировать код, разделяя его на логические блоки, которые можно сгруппировать в одном контексте. Это позволяет улучшить читаемость и управляемость кода, а также избежать конфликтов имен.

### Определение пространства имен

Пространства имен определяются с помощью ключевого слова `namespace`. Внутри пространства имен можно размещать классы, интерфейсы, функции, переменные и даже другие пространства имен.

### Пример определения пространства имен

```typescript
namespace MyNamespace {
    export class MyClass {
        greet() {
            console.log("Hello from MyClass");
        }
    }

    export function myFunction() {
        console.log("Hello from myFunction");
    }

    export const myVariable = "Hello from myVariable";
}
```

В этом примере пространство имен `MyNamespace` содержит класс `MyClass`, функцию `myFunction` и переменную `myVariable`. Все они экспортируются с помощью ключевого слова `export`, чтобы быть доступными за пределами пространства имен.

### Использование пространства имен

Для использования элементов пространства имен вне его, необходимо указать полное имя пространства имен.

### Пример использования пространства имен

```typescript
MyNamespace.myFunction(); // "Hello from myFunction"

let obj = new MyNamespace.MyClass();
obj.greet(); // "Hello from MyClass"

console.log(MyNamespace.myVariable); // "Hello from myVariable"
```

В этом примере мы обращаемся к элементам пространства имен `MyNamespace` через его полное имя.

### Вложенные пространства имен

Пространства имен могут быть вложенными, что позволяет более детально структурировать код.

### Пример вложенных пространств имен

```typescript
namespace OuterNamespace {
    export namespace InnerNamespace {
        export class InnerClass {
            sayHello() {
                console.log("Hello from InnerClass");
            }
        }
    }
}

let innerObj = new OuterNamespace.InnerNamespace.InnerClass();
innerObj.sayHello(); // "Hello from InnerClass"
```

В этом примере пространство имен `InnerNamespace` вложено в `OuterNamespace`, и класс `InnerClass` определяется внутри `InnerNamespace`.

### Импорт пространств имен

Для удобства можно импортировать элементы пространства имен в текущую область видимости с помощью ключевого слова `import`.

### Пример импорта пространства имен

```typescript
import MyNS = MyNamespace;

MyNS.myFunction(); // "Hello from myFunction"

let obj2 = new MyNS.MyClass();
obj2.greet(); // "Hello from MyClass"

console.log(MyNS.myVariable); // "Hello from myVariable"
```

В этом примере мы импортируем пространство имен `MyNamespace` под псевдонимом `MyNS`, что упрощает доступ к его элементам.

### Примеры использования пространств имен в реальных задачах

### Пример: Организация кода в библиотеке

```typescript
namespace Geometry {
    export namespace Shapes {
        export class Circle {
            constructor(public radius: number) {}

            getArea(): number {
                return Math.PI * this.radius * this.radius;
            }
        }

        export class Rectangle {
            constructor(public width: number, public height: number) {}

            getArea(): number {
                return this.width * this.height;
            }
        }
    }

    export namespace Utils {
        export function logShapeArea(shape: { getArea: () => number }) {
            console.log("Area:", shape.getArea());
        }
    }
}

let circle = new Geometry.Shapes.Circle(5);
let rectangle = new Geometry.Shapes.Rectangle(10, 20);

Geometry.Utils.logShapeArea(circle); // "Area: 78.53981633974483"
Geometry.Utils.logShapeArea(rectangle); // "Area: 200"
```

В этом примере пространство имен `Geometry` содержит вложенные пространства имен `Shapes` и `Utils`, которые организуют классы и функции, связанные с геометрическими фигурами.

### Заключение

Пространства имен в TypeScript предоставляют мощный инструмент для организации и структурирования кода в больших проектах. Они помогают группировать классы, интерфейсы, функции и другие пространства имен в логические блоки, что делает код более управляемым и читаемым. Пространства имен также помогают избегать конфликтов имен, обеспечивая более безопасную и чистую структуру кода. Использование пространств имен включает определение, вложение, импорт и экспорт, что позволяет гибко управлять видимостью и доступностью элементов в коде.
[[https://purpleschool.ru/knowledge-base/typescript/modules-and-namespaces|Источник]]