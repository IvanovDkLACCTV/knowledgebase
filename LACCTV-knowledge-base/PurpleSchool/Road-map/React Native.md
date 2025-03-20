## React Native

### Компоненты и стили

- Стилизация
- Flex
- Работа с SVG
- Image
- Обработка событий
- Input
- ScrollView
- Fonts
- FlatList
- RefreshControl
- NativeWind
- Platform-specific стили

### Анимация

- Интерполяция
- Основы анимации
- Ограничения анимации
- Reanimated (Основы)
- Reanimated (useSharedValue, useAnimatedStyle, жесты)
- Расширенные возможности Reanimated: работа с жестами, сложные анимации.    
- Использование библиотеки **react-native-gesture-handler**.

### Отладка и lint

- Eslint
- Обработка ошибок
- Отладчик и Chrome
- React Dev Tools

### Expo Router

- Основы
- Layout
- Stack
- SafeArea и StatusBar
- SplashScreen
- Unmatched
- Route с параметрами
- Вложенные Layout
- Drawer
- Навигация

### Нативные возможности


- ImagePicker
- Sharing API
- Permissions
- Expo-notifications
- Работа с push уведомлениями
- Использование библиотеки **expo-camera**.
- Использование библиотеки **expo-location**
- Использование библиотеки **expo-sensors**
### Адаптив

- Dimensions
- ScreenOrientation
- KeyboardAvoidingView
- Поддержка планшетов
- Platform
- Использование **Dimensions** и **useWindowDimensions**
- Оптимизация производительности: использование **memo**, **useCallback**, **useMemo**

#### Локальное хранение данных

- AsyncStorage
- MMKV
- SQLite в React Native
- Работа с файлами (react-native-fs)

#### Работа с удалёнными базами данных

- Подключение к Firebase
- Работа с Firestore
- REST API
- GraphQL (Apollo Client)
- Подключение к PostgreSQL / MySQL через Backend

### Сборка

- Сборка через EAS
- Сборка через XCode
- Сборка через Android Studio
- Сборка без Expo
- Настройка окружения для сборки без Expo.
- Использование **EAS Build** для автоматизации сборки
- Публикация приложения в Google Play Store и App Store

### Локальное хранилище

#### **AsyncStorage**

- Основы AsyncStorage: методы `setItem`, `getItem`, `removeItem`, `clear`.
    
- Ограничения AsyncStorage: объем данных, типы данных (только строки).
    
- Примеры использования: хранение токенов, настроек пользователя, темы (dark/light mode).
    

#### **MMKV**

- Преимущества MMKV перед AsyncStorage: производительность, поддержка типов данных.
    
- Настройка и использование MMKV в React Native.
    
- Примеры: хранение больших объемов данных, кэширование.
    

#### **SQLite**

- Настройка SQLite в React Native (например, с использованием библиотеки **react-native-sqlite-storage**).
    
- CRUD операции в SQLite.
    
- Примеры: хранение структурированных данных, офлайн-режим.
    

#### **Работа с файлами**

- Использование библиотеки **react-native-fs** для работы с файловой системой.
    
- Чтение и запись файлов.
    
- Примеры: сохранение изображений, работа с логами.

### PWA и офлайн-режим

#### **Офлайн-режим**

- Стратегии кэширования данных в React Native.
    
- Использование Service Worker (если применимо).
    
- Примеры: офлайн-доступ к данным, кэширование API-запросов.
    

#### **Push-уведомления**

- Настройка push-уведомлений через **expo-notifications**.
    
- Интеграция с Firebase Cloud Messaging (FCM).
    
- Примеры: отправка уведомлений пользователям.