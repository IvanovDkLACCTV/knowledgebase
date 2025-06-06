---
title: "Объект Date в JavaScript"
source: "https://purpleschool.ru/knowledge-base/article/date"
author:
published:
created: 2025-03-21
description: "Разбираемся как работает объект Date в JavaScript"
tags:
  - "clippings"
---
![](https://purpleschool.ru/_next/static/media/time-icon.33f80bd8.svg) 17 марта 2025 г.Автор

Дмитрий Нечаев

Объект `Date` в JavaScript предназначен для работы с датой и временем. Он позволяет создавать новые даты, получать информацию о текущем времени, а также выполнять множество операций с датами, такие как установка, получение и изменение значений.

### Создание объекта Date

Создать новый объект `Date` можно несколькими способами:

1. **Без аргументов**: Это создаст объект, представляющий текущую дату и время.
```jsx
const currentDate = new Date();
console.log(currentDate); // Выведет текущую дату и время
```
1. **С использованием строки даты**: Можно передать строку в формате даты в конструктор `Date`.
```jsx
const specificDate = new Date('2022-05-25');
console.log(specificDate); // Выведет дату 25 мая 2022 года
```
1. **С использованием временной метки**: Можно передать количество миллисекунд с начала эпохи Unix (1 января 1970 года) в конструктор `Date`.
```jsx
const timestampDate = new Date(1621872000000);
console.log(timestampDate); // Выведет дату 25 мая 2021 года
```

### Получение информации о дате и времени

Для получения информации о дате и времени можно использовать различные методы объекта `Date`:

```jsx
const date = new Date();

const year = date.getFullYear(); // Получить год
const month = date.getMonth(); // Получить месяц (от 0 до 11)
const day = date.getDate(); // Получить день месяца (от 1 до 31)
const hours = date.getHours(); // Получить часы (от 0 до 23)
const minutes = date.getMinutes(); // Получить минуты (от 0 до 59)
const seconds = date.getSeconds(); // Получить секунды (от 0 до 59)
const milliseconds = date.getMilliseconds(); // Получить миллисекунды (от 0 до 999)
const dayOfWeek = date.getDay(); // Получить день недели (от 0 (воскресенье) до 6 (суббота))
```

### Установка даты и времени

Можно также устанавливать значения даты и времени с помощью соответствующих методов:

```jsx
const date = new Date();

date.setFullYear(2023); // Установить год
date.setMonth(11); // Установить месяц (от 0 до 11)
date.setDate(31); // Установить день месяца (от 1 до 31)
date.setHours(23); // Установить часы (от 0 до 23)
date.setMinutes(59); // Установить минуты (от 0 до 59)
date.setSeconds(59); // Установить секунды (от 0 до 59)
date.setMilliseconds(999); // Установить миллисекунды (от 0 до 999)
```

### Форматирование даты и времени

JavaScript предоставляет методы для форматирования даты и времени:

```jsx
const date = new Date();

const dateString = date.toDateString(); // Преобразовать в строку с датой (день недели, месяц, число, год)
const timeString = date.toTimeString(); // Преобразовать в строку с временем (часы, минуты, секунды)
const dateTimeString = date.toLocaleString(); // Преобразовать в строку с датой и временем в локальном формате
```

### Работа с датами и временем

Методы объекта `Date` также позволяют выполнять различные операции с датами:

```jsx
const date = new Date();

date.setDate(date.getDate() + 7); // Увеличить дату на 7 дней
date.setHours(date.getHours() + 1); // Увеличить время на 1 час
```

### Заключение

Объект `Date` предоставляет множество методов для работы с датой и временем в JavaScript. Он позволяет создавать новые даты, получать информацию о текущем времени, а также устанавливать и изменять значения даты и времени. С помощью методов форматирования и операций над датами можно эффективно работать с датами в приложениях.

### Карта развития разработчика

Получите полную карту развития разработчика по всем направлениям: frontend, backend, devops, mobile