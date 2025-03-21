Анимации в CSS позволяют оживить веб-страницы и добавить динамики элементам интерфейса. Одним из основных инструментов для создания сложных анимаций является директива `@keyframes`, которая позволяет задавать ключевые кадры анимации. В этой статье мы подробно рассмотрим, как использовать `@keyframes`, и приведём примеры её применения.

## Основы директивы `@keyframes`

Директива `@keyframes` позволяет определить анимацию, описав ключевые кадры и состояния, через которые проходит анимируемый элемент. Ключевые кадры задаются с помощью процентов или ключевых слов `from` и `to`, которые обозначают начало и конец анимации соответственно.

### Синтаксис директивы `@keyframes`

```css
@keyframes animation-name {
    from {
        /* начальное состояние */
    }
    to {
        /* конечное состояние */
    }
}
```

Или с использованием процентов:

```css
@keyframes animation-name {
    0% {
        /* начальное состояние */
    }
    100% {
        /* конечное состояние */
    }
}
```

### Пример базовой анимации

```css
@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}

.element {
    animation: fadeIn 2s ease-in-out;
}
```

В этом примере анимация `fadeIn` делает элемент плавно видимым в течение 2 секунд.

## Указание ключевых кадров

Ключевые кадры можно задавать с помощью процентов для создания более сложных анимаций.

### Пример анимации с несколькими ключевыми кадрами

```css
@keyframes bounce {
    0% {
        transform: translateY(0);
    }
    50% {
        transform: translateY(-50px);
    }
    100% {
        transform: translateY(0);
    }
}

.element {
    animation: bounce 1s infinite;
}
```

В этом примере анимация `bounce` заставляет элемент прыгать, используя три ключевых кадра: начальное положение, верхнюю точку и возвращение к исходному положению.

## Настройки анимации

Для управления анимацией используются различные свойства:

- `animation-name` — имя анимации, определённое в `@keyframes`.
- `animation-duration` — продолжительность анимации.
- `animation-timing-function` — функция временного распределения.
- `animation-delay` — задержка перед началом анимации.
- `animation-iteration-count` — количество повторений анимации.
- `animation-direction` — направление анимации.
- `animation-fill-mode` — поведение анимации до начала и после завершения.
- `animation-play-state` — состояние анимации (воспроизведение или пауза).

### Пример настройки анимации

```css
@keyframes slideIn {
    from {
        transform: translateX(-100%);
    }
    to {
        transform: translateX(0);
    }
}

.element {
    animation-name: slideIn;
    animation-duration: 3s;
    animation-timing-function: ease-in-out;
    animation-delay: 1s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
    animation-fill-mode: forwards;
    animation-play-state: running;
}
```

В этом примере элемент будет заезжать слева, анимация начнётся через 1 секунду, будет длиться 3 секунды, повторяться бесконечно, чередовать направления и сохранять конечное состояние.

## Использование сокращённого синтаксиса

Свойства анимации можно задавать в сокращённой записи.

### Пример сокращённого синтаксиса

```css
@keyframes rotate {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

.element {
    animation: rotate 5s linear infinite;
}
```

В этом примере анимация `rotate` вращает элемент на 360 градусов за 5 секунд бесконечно с линейной функцией времени.

## Сложные примеры анимаций

### Пример 1: Анимация вращения и изменения размера

```css
@keyframes rotateAndScale {
    0% {
        transform: rotate(0deg) scale(1);
    }
    50% {
        transform: rotate(180deg) scale(1.5);
    }
    100% {
        transform: rotate(360deg) scale(1);
    }
}

.element {
    animation: rotateAndScale 4s ease-in-out infinite;
}
```

В этом примере элемент будет вращаться и увеличиваться в размере, затем возвращаться к исходному состоянию.

### Пример 2: Анимация изменения цвета и перемещения

```css
@keyframes colorMove {
    0% {
        background-color: red;
        transform: translateX(0);
    }
    50% {
        background-color: blue;
        transform: translateX(100px);
    }
    100% {
        background-color: red;
        transform: translateX(0);
    }
}

.element {
    animation: colorMove 3s ease-in-out infinite;
}
```

В этом примере элемент будет перемещаться по горизонтали и изменять цвет фона.

## Заключение

Директива `@keyframes` в CSS предоставляет мощные возможности для создания сложных анимаций, позволяя задавать ключевые кадры и состояния. С её помощью можно оживить веб-страницы, добавив динамические и визуально привлекательные эффекты. Освоив использование `@keyframes`, вы сможете создавать профессиональные и креативные анимации для ваших веб-проектов.

[[https://purpleschool.ru/knowledge-base/article/keyframes|Источник]]