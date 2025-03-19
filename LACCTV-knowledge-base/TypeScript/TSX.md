### JSX в контексте TypeScript и React Native

JSX — это синтаксическое расширение для JavaScript, которое позволяет писать HTML-подобный код в JavaScript. В React Native JSX используется для описания структуры пользовательского интерфейса. Важно понимать, что JSX — это не HTML, а синтаксический сахар для вызовов функций, таких как `React.createElement`.

---

### Настройка `tsconfig.json` для работы с JSX

Для работы с JSX в TypeScript нужно настроить `tsconfig.json`. Вот основные параметры:

```json
{
  "compilerOptions": {
    "jsx": "react", // Указывает, что TypeScript должен компилировать JSX в вызовы React.createElement
    "module": "esnext", // Используем современные модули
    "target": "es6", // Целевая версия JavaScript
    "strict": true, // Включает строгую проверку типов
    "esModuleInterop": true, // Упрощает работу с CommonJS модулями
    "skipLibCheck": true, // Пропускает проверку типов в библиотеках
    "forceConsistentCasingInFileNames": true // Обеспечивает согласованность в именах файлов
  }
}
```

- `"jsx": "react"` — указывает TypeScript, что JSX должен компилироваться в вызовы `React.createElement`.
- Если вы используете React 17+ с новым JSX-трансформером, можно указать `"jsx": "react-jsx"`.

---

### Установка React, `@types/react`, `react-native`

Для работы с React Native и TypeScript нужно установить следующие пакеты:

```bash
npm install react react-native
npm install --save-dev @types/react @types/react-native
```

- `react` и `react-native` — основные библиотеки для работы с React Native.
- `@types/react` и `@types/react-native` — типы TypeScript для React и React Native.

---

### Что значит запись `JSX.Element`?

`JSX.Element` — это тип, который представляет собой результат компиляции JSX. Это объект, который описывает виртуальный DOM-элемент.

Пример:

```typescript
const element: JSX.Element = <Text>Hello, World!</Text>;
```

Здесь `element` — это объект, который будет создан после компиляции JSX.

---

### Для чего используются фигурные скобки `{}` в JSX?

Фигурные скобки `{}` используются для вставки JavaScript-выражений в JSX. Например:

```typescript
const name = "Alice";
const element = <Text>Hello, {name}!</Text>;
```

Здесь `{name}` будет заменено на значение переменной `name`.

---

### Пример с кастомными тегами и свойствами

В JSX можно использовать кастомные компоненты и передавать им свойства (props). Например:

```typescript
interface GreetingProps {
  name: string;
  age: number;
}

function Greeting({ name, age }: GreetingProps): JSX.Element {
  return (
    <View>
      <Text>Hello, {name}!</Text>
      <Text>You are {age} years old.</Text>
    </View>
  );
}

const App = () => (
  <Greeting name="Alice" age={30} />
);
```

- `Greeting` — это кастомный компонент.
- `name` и `age` — это свойства (props), которые передаются в компонент.

---

### Почему JSX — это не HTML

JSX выглядит как HTML, но это не HTML. Это синтаксический сахар для вызовов `React.createElement`. Например:

```typescript
const element = <Text>Hello, World!</Text>;
```

После компиляции это превратится в:

```javascript
const element = React.createElement(Text, null, "Hello, World!");
```

---

### Пример с `React.createElement`

JSX:

```typescript
const element = <Text style={{ color: "red" }}>Hello, World!</Text>;
```

Эквивалентный код с `React.createElement`:

```javascript
const element = React.createElement(Text, { style: { color: "red" } }, "Hello, World!");
```

---

### Что будет после компиляции с помощью `tsc`

Исходный код:

```typescript
const App = () => (
  <View>
    <Text>Hello, World!</Text>
  </View>
);
```

После компиляции:

```javascript
const App = () => React.createElement(View, null, React.createElement(Text, null, "Hello, World!"));
```

---

### Как работает `React.render` (кратко)

`React.render` (или `ReactDOM.render` в вебе) принимает виртуальный DOM-элемент (созданный с помощью JSX или `React.createElement`) и монтирует его в реальный DOM (или в корневой элемент React Native).

Пример:

```typescript
import { AppRegistry } from 'react-native';
import App from './App';

AppRegistry.registerComponent('MyApp', () => App);
```

Здесь `AppRegistry` монтирует корневой компонент `App` в приложение React Native.

---

### Почему вместо треугольных скобок при касте типа надо использовать `as`

В TypeScript для приведения типов используется ключевое слово `as`, а не угловые скобки (`<>`), чтобы избежать конфликтов с синтаксисом JSX.

Пример:

```typescript
const value: any = "123";
const numberValue = value as number; // Приведение типа
```

Если бы мы использовали угловые скобки:

```typescript
const numberValue = <number>value; // Ошибка: конфликт с JSX
```

---

### Итог

- JSX — это синтаксический сахар для `React.createElement`.
- `JSX.Element` — это тип, представляющий результат компиляции JSX.
- Фигурные скобки `{}` используются для вставки JavaScript-выражений в JSX.
- Кастомные компоненты и свойства позволяют создавать гибкие UI.
- `React.createElement` — это низкоуровневый способ создания элементов.
- `as` используется для приведения типов в TypeScript.

> Советую ознакомиться с [[https://purpleschool.ru/knowledge-base/typescript|базой знаний по TypeScript от PurleSchool]]. 
> Данный раздел этого курса был вдохновлён именно этой базой знаний.