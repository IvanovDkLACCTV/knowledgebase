Статические поля и методы в TypeScript позволяют создавать свойства и функции, которые принадлежат самому классу, а не его экземплярам. Они определяются с помощью ключевого слова `static` и могут быть вызваны без создания экземпляра класса. Это удобно для определения утилитарных функций, констант и других элементов, которые логически принадлежат всему классу, а не отдельным объектам.

### Определение и использование статических полей и методов

### Пример статического поля

```typescript
class MathUtils {
    static PI: number = 3.14;

    static calculateCircumference(radius: number): number {
        return 2 * MathUtils.PI * radius;
    }
}

// Обращение к статическому полю
console.log(MathUtils.PI); // 3.14

// Обращение к статическому методу
console.log(MathUtils.calculateCircumference(10)); // 62.8
```

В этом примере `PI` и `calculateCircumference` являются статическими. Они принадлежат классу `MathUtils` и могут быть вызваны напрямую через имя класса.

### Преимущества использования статических полей и методов

1. **Общий доступ**: Статические поля и методы предоставляют общий доступ к данным и функциям без необходимости создания экземпляра класса.
2. **Константы и утилиты**: Часто используются для определения констант и утилитарных функций.
3. **Сохранение состояния**: Могут использоваться для хранения состояния, общего для всех экземпляров класса.

### Пример с сохранением состояния

```typescript
class Counter {
    private static count: number = 0;

    public static increment(): void {
        Counter.count++;
    }

    public static getCount(): number {
        return Counter.count;
    }
}

// Увеличиваем счетчик
Counter.increment();
Counter.increment();

// Получаем текущее значение счетчика
console.log(Counter.getCount()); // 2
```

В этом примере `Counter` содержит статическое поле `count`, которое отслеживает общее количество вызовов метода `increment`. Статический метод `getCount` возвращает текущее значение счетчика.

### Статические блоки

В TypeScript также поддерживаются статические блоки, которые позволяют выполнять инициализацию статических полей при загрузке класса.

### Пример использования статических блоков

```typescript
class Configuration {
    static readonly VERSION: string;
    static readonly API_URL: string;

    static {
        Configuration.VERSION = "1.0.0";
        Configuration.API_URL = "<https://api.example.com>";
    }
}

console.log(Configuration.VERSION); // "1.0.0"
console.log(Configuration.API_URL); // "<https://api.example.com>"
```

В этом примере статический блок используется для инициализации констант `VERSION` и `API_URL` при загрузке класса `Configuration`.

### Ограничения статических полей и методов

1. **Отсутствие доступа к экземплярам**: Статические методы не имеют доступа к свойствам и методам экземпляров класса.
2. **Отсутствие `this`**: В статических методах нельзя использовать `this` для обращения к полям и методам экземпляра.

### Пример ограничения

```typescript
class InstanceCounter {
    private static count: number = 0;

    constructor() {
        InstanceCounter.count++;
    }

    public static getCount(): number {
        return InstanceCounter.count;
    }

    public getInstanceCount(): number {
        // Ошибка: Статический метод не имеет доступа к this
        // return this.count;
        return InstanceCounter.count;
    }
}

let instance1 = new InstanceCounter();
let instance2 = new InstanceCounter();

console.log(InstanceCounter.getCount()); // 2
```

В этом примере статический метод `getCount` не может использовать `this`, так как он относится к классу, а не к его экземплярам.

### Заключение

Статические поля и методы в TypeScript предоставляют мощный инструмент для организации кода, позволяя определять свойства и функции, которые логически принадлежат классу, а не его экземплярам. Они часто используются для создания утилитарных функций, констант и для сохранения состояния, общего для всех объектов класса. При правильном использовании статические поля и методы помогают улучшить читаемость и поддерживаемость кода.

[[https://purpleschool.ru/knowledge-base/article/static-fields-and-methods|Источник]]