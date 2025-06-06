### **Storybook для React Native: Полное руководство**  
**Storybook** — это инструмент для **разработки, тестирования и документирования UI-компонентов** в изоляции. Он особенно полезен в больших проектах, где много переиспользуемых компонентов.

---

[Познакомьтесь с Storybook, посмотрев это видео](https://youtu.be/gdlTFPebzAU?si=bZutKwWUjtG8Odqu)

---

## **1. Зачем нужен Storybook?**  
- 🛠 **Разработка компонентов в изоляции** — без зависимости от основного приложения.  
- 📚 **Документирование** — демонстрация всех состояний компонента (с примерами кода).  
- 🎨 **Визуальное тестирование** — проверка внешнего вида при разных пропсах.  
- 🔄 **Совместная работа** — дизайнеры и разработчики могут видеть компоненты в Storybook без запуска всего приложения.  

---

## **2. Установка Storybook для React Native**  

### **Шаг 1: Инициализация проекта**  
Если у вас ещё нет проекта:  
```bash
npx react-native init MyApp
cd MyApp
```

### **Шаг 2: Установка Storybook**  
```bash
npx -p @storybook/cli sb init --type react_native
```
После этого в проекте появится папка `storybook` с базовой конфигурацией.

### **Шаг 3: Запуск Storybook**  
```bash
npm run storybook
```
Затем запустите приложение в отдельном терминале:  
```bash
npx react-native run-android  # или run-ios
```
Storybook откроется в браузере на `http://localhost:7007`, а компоненты будут отображаться в мобильном приложении.

---

## **3. Структура проекта**  
После инициализации:  
```
my-app/
├── storybook/
│   ├── index.js          # Главный файл Storybook
│   ├── stories/          # Папка с историями
│   │   └── Button.stories.js  # Пример истории
├── App.js
└── ...
```

---

## **4. Создание Stories (Историй)**  
**Story (История)** — это изолированное состояние компонента.  

### 📌 **Пример: Документирование кнопки**  
Допустим, у нас есть компонент `Button.js`:  
```jsx
import React from 'react';
import { TouchableOpacity, Text } from 'react-native';

const Button = ({ title, onPress, disabled = false }) => {
  return (
    <TouchableOpacity 
      onPress={onPress} 
      disabled={disabled}
      style={{ 
        padding: 10, 
        backgroundColor: disabled ? 'gray' : 'blue',
        borderRadius: 5,
      }}
    >
      <Text style={{ color: 'white' }}>{title}</Text>
    </TouchableOpacity>
  );
};

export default Button;
```

Создаём историю в `stories/Button.stories.js`:  
```jsx
import React from 'react';
import { storiesOf } from '@storybook/react-native';
import Button from '../../src/components/Button';

// Группируем истории по категориям
storiesOf('Components/Button', module)
  .add('Default', () => (
    <Button 
      title="Click me" 
      onPress={() => console.log('Pressed!')} 
    />
  ))
  .add('Disabled', () => (
    <Button 
      title="Disabled" 
      onPress={() => {}} 
      disabled={true} 
    />
  ));
```

---

## **5. Просмотр Stories**  
После запуска Storybook:  
- Откроется веб-интерфейс (`http://localhost:7007`).  
- В мобильном приложении будут отображаться компоненты.  


---

## **6. Дополнительные возможности**  

### **📌 Addons (Расширения)**  
Storybook поддерживает плагины:  
- **Knobs** — динамическое изменение пропсов прямо в интерфейсе.  
- **Actions** — логирование кликов и событий.  
- **Docs** — автоматическая генерация документации.  

Установка аддонов:  
```bash
npm install @storybook/addon-knobs @storybook/addon-actions @storybook/addon-docs
```

Пример с Knobs:  
```jsx
import { withKnobs, text, boolean } from '@storybook/addon-knobs';

storiesOf('Components/Button', module)
  .addDecorator(withKnobs)
  .add('Dynamic Props', () => (
    <Button 
      title={text('Title', 'Click me')} 
      disabled={boolean('Disabled', false)}
    />
  ));
```

---

## **7. Интеграция с TypeScript и JSDoc**  
Storybook отлично работает с TypeScript и JSDoc.  

### **Пример с TypeScript**  
```tsx
interface ButtonProps {
  title: string;
  onPress: () => void;
  disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({ title, onPress, disabled }) => { ... };
```

### **Пример с JSDoc**  
```jsx
/**
 * Кастомная кнопка.
 * @param {Object} props - Пропсы.
 * @param {string} props.title - Текст кнопки.
 * @param {() => void} props.onPress - Обработчик нажатия.
 * @param {boolean} [props.disabled=false] - Блокировка кнопки.
 */
const Button = ({ title, onPress, disabled = false }) => { ... };
```

---

## **8. Деплой Storybook**  
Можно выложить Storybook в сеть для доступа команды:  
- **Chromatic** (платный) — облачный хостинг от создателей Storybook.  
- **GitHub Pages** (бесплатно) — ручная настройка.  

Пример для GitHub Pages:  
```bash
npm run build-storybook
```
Загрузите содержимое папки `storybook-static` в GitHub Pages.

---

## **9. Плюсы и минусы Storybook**  

### **✅ Плюсы**  
- Ускоряет разработку UI.  
- Упрощает документирование компонентов.  
- Позволяет тестировать edge-кейсы (например, длинный текст в кнопке).  

### **❌ Минусы**  
- Требует времени на настройку.  
- Может замедлять сборку в больших проектах.  

---

## **10. Итог**  
1. **Storybook** — мощный инструмент для разработки UI в React Native.  
2. **Подходит для:**  
   - Командной работы (дизайнеры + разработчики).  
   - Документирования компонентов.  
   - Визуального тестирования.  
3. **Лучше всего комбинировать с:**  
   - JSDoc (описание пропсов).  
   - TypeScript (типизация).  


Ознакомьтесь с Storybook подробнее в [миникурсе по этой ссылке](https://youtu.be/uMKFBg1BZWs?si=X9iWtvV_VroADGPS) 🚀