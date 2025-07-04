## 🧩 Архитектура и стек

### 1. **Headless CMS (Payload)**
   
- **Payload CMS 3** — tight-интеграция с Next.js, можно «установить прямо в сайт» (в один репозиторий) и использовать Local API без HTTP ([reddit.com](https://www.reddit.com/r/nextjs/comments/1h0iekq?utm_source=chatgpt.com "What is the huge push by Payload CMS? Is it actually a highly recommended service or is it marketing?")).
    
- CMS отвечает за:
    
    - хранение Markdown/MDX-файлов,
        
    - интерфейс для non-dev авторов с ролями,
        
    - API для всех клиентов,
        
    - Webhooks — Telegram, Django, отчёты и т.п.
        

---

### 2. **Веб-приложение (Next.js + T3 Stack + Fumadocs)**

- **Next.js (App Router)** с Fumadocs/MDX-генерацией документации.
    
- **T3 Stack**: tRPC/Prisma для типобезопасной логики, NextAuth — авторизация.
    
- Потребляет контент из CMS (через REST/GraphQL или Local API), добавляет бизнес-функции.
    
- SEO, статические страницы, SSR и кастомная веб‑админка (если нужна).
    

---

### 3. **Мобильное приложение (Expo)**

- Expo (React Native + Web) с MDX/Markdown рендерером (`rn-mdx` или `react-native-markdown-display`).
    
- Интеграция с камерой и сканером (сканирование номеров для отчетов).
    
- Expo-пуши: CMS может отправлять пуши через плагин Strapi или ручной webhook/API ([libraries.io](https://libraries.io/npm/strapi-plugin-notification-expo?utm_source=chatgpt.com "strapi-plugin-notification-expo 1.0.0-beta.5 on npm - Libraries.io - security & maintenance data for open source software")).
    
- OTA-обновления контента через EAS (бесплатный план работает до 1K MAU).
    

---

### 4. **Backend-эко-система**

- **Django API** — отдельный сервис для учёта актов, доступный из CMS/Web/Expo через API или webhook.
    
- **Telegram-бот** — получает webhooks из CMS или Django, отправляет уведомления/отчёты пользователям.
    

---

### 5. **Интеграции и workflow**

- **GitHub → CMS**: Obsidian-страницы пушатся и синхронизируются (через CI или webhook).
    
- **CMS → Telegram/Django**: при публикации через webhook.
    
- **CMS → Expo**: через API и Expo push.
    
- **Next.js** и **Expo** — потребляют один API, повторно используют типы (особенно с Payload).
    

---

## 🛠 Преимущества стека

|Компонент|Цель|Преимущество|
|---|---|---|
|Headless CMS|Контент и авторство|UI для non-dev, роли, Webhook, API|
|Next.js + T3|Веб + документация|SSR, MDX, SEO, типобезопасная бизнес-логика|
|Expo|Mobile + Web|Один код, интеграция камеры, OTA|
|Django|Учёт актов|Отдельный сервис с бизнес-логикой|
|Telegram|Пользователи и отчёты|Информирование через выходные каналы|

---

## ✅ Почему это работает

- Контент один для всех платформ — благодаря централизованному API.
    
- Не нуждаются в дублировании логики авторизации/ролей — всё в CMS.
    
- Быстро разворачиваются платформы: веб, iOS, Android, Telegram.
    
- Сильная типобезопасность (Payload + tRPC + Prisma).
    
- Масштабируемый, гибкий стек — легко изменять и добавлять новые функции.
    

---
