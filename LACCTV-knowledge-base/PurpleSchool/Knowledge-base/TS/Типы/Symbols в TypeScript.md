
## Введение

В ECMAScript 2015 введен тип `symbol` (символ) — примитивный тип данных, такой же, как `number` и `string`.

Значения типа `symbol` создаются с помощью вызова конструктора `Symbol`.

```typescript
let sym1 = Symbol();

let sym2 = Symbol("key"); // Необязательный строковый ключ
```

Символы неизменяемы и уникальны.

```typescript
let sym2 = Symbol("key");
let sym3 = Symbol("key");

sym2 === sym3; // false, символы уникальны
```

Подобно строкам, символы можно использовать как ключи для свойств объекта.

```typescript
const sym = Symbol();

let obj = {
    [sym]: "value"
};

console.log(obj[sym]); // "value"
```

Символы можно использовать вместе с вычисляемыми свойствами, чтобы объявлять свойства объектов и члены классов:

```typescript
const getClassNameSymbol = Symbol();

class C {
    [getClassNameSymbol](){
       return "C";
    }
}

let c = new C();
let className = c[getClassNameSymbol](); // "C"
```

## Заранее определенные символы

Кроме символов, определяемых пользователем, существуют заранее определенные встроенные символы. Встроенные символы нужны для отражения внутреннего поведения языка.

Список заранее определенных символов:

### `Symbol.asyncIterator`

Метод, возвращающий асинхронный итератор для объекта, совместимый с циклом `for await...of`.

### `Symbol.hasInstance`

Метод, который определяет, распознает ли объект конструктора переданный объект как экземпляр этого конструктора. Вызывается оператором `instanceof`.

### `Symbol.isConcatSpreadable`

Логическое значение, означающее, должен ли объект раскладываться на элементы массива при использовании с `Array.prototype.concat`.

### `Symbol.iterator`

Метод, который возвращает итератор по умолчанию для объекта. Вызывается конструкцией `for-of`.

### `Symbol.match`

Метод для регулярных выражений, который сопоставляет регулярное выражение со строкой. Вызывается методом `String.prototype.match`.

### `Symbol.replace`

Метод для регулярных выражений, который заменяет совпавшие подстроки в строке. Вызывается методом `String.prototype.replace`.

### `Symbol.search`

Метод для регулярных выражений, который возвращает позицию в строке, где находится совпадение с регулярным выражением. Вызывается методом `String.prototype.search`.

### `Symbol.species`

Свойство, содержащее функцию, которая служит в качестве конструктора для унаследованных объектов.

### `Symbol.split`

Метод для регулярных выражений, который разбивает строку по позициям совпадений с регулярным выражением. Вызывается методом `String.prototype.split`.

### `Symbol.toPrimitive`

Метод, который превращает объект в соответствующее примитивное значение. Вызывается абстрактной операцией `ToPrimitive`.

### `Symbol.toStringTag`

Строковое значение, которое используется для создания строкового значения по умолчанию, описывающего объект. Вызывается встроенным методом `Object.prototype.toString`.

### `Symbol.unscopables`

Объект, имена собственных свойств которого — это имена свойств, привязки к которым не включаются в окружение, создаваемое конструкцией `with` для соответствующих объектов.
[[https://purpleschool.ru/knowledge-base/typescript/types|Источник]]