Свойство `animation-name` в CSS позволяет задать имя для анимации, чтобы можно было применить её к элементу. Без этого свойства невозможно связать анимацию, описанную с помощью `@keyframes`, с конкретным элементом. В этой статье мы подробно рассмотрим, как использовать `animation-name`, и приведем примеры для лучшего понимания.

## Основы animation-name

Свойство `animation-name` связывает элемент с анимацией, определенной с помощью правила `@keyframes`. Без задания имени анимации она не будет применена к элементу.

### Синтаксис animation-name

Синтаксис использования свойства `animation-name` простой:

```css
.element {
  animation-name: имя_анимации;
}
```

### Пример использования

Рассмотрим простой пример, где анимация изменяет прозрачность элемента:

```css
@keyframes fade {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.fade-element {
  animation-name: fade; /* Применение анимации с именем fade */
  animation-duration: 2s;
}
```

В этом примере элемент `.fade-element` будет плавно изменять прозрачность от 0 до 1 в течение 2 секунд.

## Задание нескольких анимаций

С помощью свойства `animation-name` можно задавать несколько анимаций для одного элемента. Имена анимаций перечисляются через запятую.

### Пример использования нескольких анимаций

```css
@keyframes move {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(100px);
  }
}

@keyframes fade {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.multi-animation-element {
  animation-name: move, fade; /* Применение нескольких анимаций */
  animation-duration: 2s, 3s; /* Соответствующая длительность для каждой анимации */
}
```

В этом примере элемент `.multi-animation-element` будет одновременно перемещаться и изменять прозрачность.

## Совместное использование с другими свойствами анимации

Свойство `animation-name` часто используется вместе с другими анимационными свойствами, такими как `animation-duration`, `animation-timing-function`, `animation-delay`, `animation-iteration-count`, и `animation-direction`.

### Пример с комплексной анимацией

Рассмотрим более сложный пример, где используется несколько анимационных свойств:

```css
@keyframes bounce {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-100px);
  }
  100% {
    transform: translateY(0);
  }
}

.bounce-element {
  animation-name: bounce; /* Применение анимации с именем bounce */
  animation-duration: 1s;
  animation-timing-function: ease-in-out;
  animation-delay: 0.5s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
```

Здесь элемент `.bounce-element` будет двигаться вверх и вниз бесконечно, чередуя направление анимации.

## Практические примеры использования animation-name

### Пример с вращающейся анимацией

Создадим анимацию, которая будет вращать элемент:

```css
@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.rotate-element {
  animation-name: rotate; /* Применение анимации с именем rotate */
  animation-duration: 4s;
  animation-iteration-count: infinite;
}
```

### Пример с изменением цвета

Создадим анимацию, которая будет изменять цвет элемента:

```css
@keyframes changeColor {
  from {
    background-color: red;
  }
  to {
    background-color: blue;
  }
}

.color-element {
  animation-name: changeColor; /* Применение анимации с именем changeColor */
  animation-duration: 3s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
}
```

## Советы и рекомендации

1. **Задание осмысленных имен**. Используйте осмысленные и понятные имена для анимаций, чтобы код был легче читать и поддерживать.
    
2. **Комбинирование с другими свойствами**. Используйте `animation-name` вместе с другими анимационными свойствами для создания более сложных и плавных анимаций.
    
3. **Тестирование в разных браузерах**. Убедитесь, что ваши анимации корректно работают в различных браузерах, так как поддержка CSS-анимаций может отличаться.
    

## Заключение

Свойство `animation-name` в CSS является ключевым инструментом для задания имени анимации, чтобы можно было применить её к элементу. Используя это свойство, вы можете легко связывать анимации, определенные с помощью `@keyframes`, с конкретными элементами и создавать динамичные и привлекательные веб-страницы. Следуя приведенным рекомендациям и примерам, вы сможете эффективно использовать `animation-name` в своих проектах, улучшая взаимодействие с пользователями и делая ваши веб-страницы более интересными и интерактивными.

[[https://purpleschool.ru/knowledge-base/article/animation-name|Источник]]