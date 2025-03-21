---
title: "Поверхностное и глубокое копирование в JavaScript"
source: "https://purpleschool.ru/knowledge-base/article/shallow-or-deep-clone"
author:
published:
created: 2025-03-21
description: "Разбираемся как работает поверхностное и глубокое копирование в JavaScript"
tags:
  - "clippings"
---
![](https://purpleschool.ru/_next/static/media/time-icon.33f80bd8.svg) 17 марта 2025 г.Автор

Дмитрий Нечаев

При работе с объектами и массивами в JavaScript часто возникает необходимость копировать их для изменения или передачи в функции без изменения оригинала. Однако копирование объектов и массивов может быть поверхностным или глубоким, и понимание разницы между этими подходами важно для правильной работы с данными.

### Поверхностное копирование

При поверхностном копировании создается новый объект или массив, и его свойства или элементы копируются из оригинала. Однако если свойства объекта или элементы массива сами являются объектами или массивами, они копируются по ссылке, а не по значению.

### Пример поверхностного копирования

```jsx
const original = {
  name: 'John',
  age: 30,
  hobbies: ['reading', 'swimming']
};

const shallowCopy = Object.assign({}, original);
shallowCopy.hobbies.push('cooking');

console.log(original); // { name: 'John', age: 30, hobbies: ['reading', 'swimming', 'cooking'] }
console.log(shallowCopy); // { name: 'John', age: 30, hobbies: ['reading', 'swimming', 'cooking'] }
```

В этом примере мы создали поверхностную копию объекта `original` с помощью `Object.assign()`. После добавления нового хобби в копию, изменение также отобразилось в оригинале, потому что свойство `hobbies` копировалось по ссылке.

### Глубокое копирование

Глубокое копирование создает полностью независимую копию объекта или массива, включая все вложенные объекты и массивы. Таким образом, изменения в копии не влияют на оригинал и наоборот.

### Пример глубокого копирования

```jsx
function deepCopy(obj) {
  if (typeof obj !== 'object' || obj === null) {
    return obj; // если не объект или null, вернуть сам объект
  }

  let copy = Array.isArray(obj) ? [] : {};

  for (let key in obj) {
    copy[key] = deepCopy(obj[key]); // рекурсивно копируем свойства объекта
  }

  return copy;
}

const original = {
  name: 'John',
  age: 30,
  hobbies: ['reading', 'swimming']
};

const deepClone = deepCopy(original);
deepClone.hobbies.push('cooking');

console.log(original); // { name: 'John', age: 30, hobbies: ['reading', 'swimming'] }
console.log(deepClone); // { name: 'John', age: 30, hobbies: ['reading', 'swimming', 'cooking'] }
```

В этом примере мы определили функцию `deepCopy()`, которая рекурсивно копирует все свойства объекта. Как результат, изменения в `deepClone` не влияют на `original`.

### Заключение

Понимание разницы между поверхностным и глубоким копированием важно при работе с объектами и массивами в JavaScript. Поверхностное копирование подходит для простых случаев, но при наличии вложенных структур необходимо использовать глубокое копирование, чтобы избежать неожиданных побочных эффектов.

### Карта развития разработчика

Получите полную карту развития разработчика по всем направлениям: frontend, backend, devops, mobile