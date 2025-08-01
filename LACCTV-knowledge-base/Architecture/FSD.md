## Ссылки на источники:

1. [Ссылка на видео 1](https://youtu.be/C9gGjOx5BLQ?si=jYE28djBzn8-_9hV)
2. [Ссылка на видео 2](https://youtu.be/GQO73xCzTCA?si=HxWuQB3xM2B8V_Uw)
3. [Ссылка на видео 3](https://www.youtube.com/watch?v=H_rJ0zB8rqc)
4. [Ссылка на документацию FSD ru](https://feature-sliced.design/ru/docs)
5. [Ссылка на документацию FSD eng](https://feature-sliced.github.io/documentation/docs)
6. [Ссылка на репозиторий FSD](https://github.com/feature-sliced)

**Feature-Sliced Design (FSD)** – это **архитектурная методология** для структурирования фронтенд-приложений. По своей сути, это **набор правил и соглашений** по организации кода, разработанный для того, чтобы сделать проекты более понятными, стабильными и масштабируемыми в условиях меняющихся бизнес-требований. FSD упрощает поддержку кода, снижает порог входа для новых разработчиков и способствует повышению качества кодовой базы. Методология **не зависит от конкретного фреймворка** и применима к React, Vue, Angular, Svelte и другим.

FSD организует код на трех основных уровнях абстракции: **слои (layers)**, **слайсы (slices)** и **сегменты (segments)**.

### Основные концепции FSD

FSD вводит три основных уровня организации кода:

- **Слои (Layers)**
- **Слайсы (Slices)**
- **Сегменты (Segments)**

#### Слои (Layers)

Слои — это верхний уровень организации проекта, представляющий собой стандартный, строго регламентированный набор основных элементов. Важным правилом является **однонаправленность зависимостей**: слои могут импортировать код только из слоёв, расположенных ниже, но не наоборот. В текущей версии FSD (2.1) существует шесть основных слоёв:

- **App (Приложение)**
    - **Назначение**: Корневой уровень приложения. Содержит глобальные настройки, инициализацию, роутинг, базовые стили, точки входа (например, `main.tsx`).
    - **Особенности**: Не содержит слайсов, но может иметь сегменты (например, `routes`, `store`, `styles`, `entry-point`).
    - **Пример**: Файлы для настройки маршрутизации, глобальные провайдеры контекста, аналитика (Яндекс.Метрика, Google Analytics).
- **Pages (Страницы)**
    - **Назначение**: Декомпозиция приложения на отдельные страницы. Каждая страница — это полноценный модуль, часто состоящий из виджетов.
    - **Особенности**: Содержат слайсы, каждый из которых соответствует отдельной странице или большой ее части (например, страница профиля пользователя).
    - **Пример**: Страница товара, страница корзины, страница поиска.
- **Widgets (Виджеты)**
    - **Назначение**: Большие, самодостаточные, изолированные куски функциональности или интерфейса, ориентированные на пользовательские сценарии.
    - **Особенности**: Страницы часто агрегируют несколько виджетов. Виджеты могут быть как переиспользуемыми, так и использоваться только в одном месте.
    - **Пример**: Виджет поиска, виджет карточки товара.
- **Features (Фичи)**
    - **Назначение**: Повторно используемые реализации функций продукта или пользовательских сценариев (use cases).
    - **Особенности**: Часто отвечают на вопрос "что сделать?" (например, лайкнуть пост, добавить товар в корзину). Этот слой часто вызывает путаницу у новых разработчиков.
    - **Пример**: Счетчик изменения количества товаров в корзине, авторизация, регистрация, логаут.
- **Entities (Сущности)**
    - **Назначение**: Бизнес-сущности, с которыми работает проект.
    - **Особенности**: Отвечают на вопрос "что это?" (например, пользователь, продукт, комментарий, пост). Содержат описание модели, интерфейса, API и логики взаимодействия с данными.
    - **Пример**: Аватар пользователя, отображение поста, описание API и сторов для работы с пользователем.
- **Shared (Общий код)**
    - **Назначение**: Переиспользуемый код, который не содержит никакой бизнес-логики и является оторванным от специфики проекта.
    - **Особенности**: Самый нижний слой. Не содержит слайсов, но имеет сегменты.
    - **Пример**: Универсальные UI-компоненты (кнопки, инпуты, лейблы, селекты), базовые утилиты, общие хелперы.

Иерархия слоёв: App -> Pages -> Widgets -> Features -> Entities -> Shared. Слои верхнего уровня могут импортировать код из слоёв нижнего уровня (например, Pages может использовать Widgets, но Widgets не может использовать Pages).

#### Слайсы (Slices)

Слайсы находятся внутри конкретных слоёв (за исключением `App` и `Shared`).

- **Назначение**: Группировка кода по его назначению продукта, бизнеса или приложения. Это доменные области, определенные бизнесом.
- **Особенности**: Название слайса соответствует названию доменной области (например, `post`, `user`, `cart`, `payment`). Число слайсов неограничено и зависит от размера и сложности приложения.
- **Правило Public API**: Каждый слайс должен явно определять свой публичный API (через `index.ts` файл), контролируя, что из него может быть экспортировано для использования другими модулями. Это предотвращает глубокий импорт и нежелательные зависимости.
- **Высокая сцепленность и низкая связанность**: Правильное разделение на слайсы означает, что части кода внутри слайса (сцепленность) образуют логически единое, атомарное целое, но при этом слайс имеет минимальную зависимость (связанность) с другими слайсами.

#### Сегменты (Segments)

Сегменты находятся внутри слайсов (или непосредственно внутри `App` и `Shared`, где нет слайсов).

- **Назначение**: Дальнейшая группировка кода внутри слайса по его техническому назначению.
- **Стандартные сегменты**:
    - **UI**: UI-компоненты, относящиеся к данной доменной области (например, UI страницы пользователя).
    - **API**: Взаимодействие с бэкендом (точки API, функции для получения данных).
    - **Model**: Схемы данных, интерфейсы, хранилища, бизнес-логика конкретного слайса.
    - **Lib (Библиотека)**: Библиотечный код, нужный другим модулям этого слайса.
    - **Config (Конфигурация)**: Файлы конфигурации, фича-флаги.
- **Правило Public API**: Подобно слайсам, сегменты также должны явно определять свой публичный API, чтобы контролировать, какие части могут быть использованы извне.

### Как работать с FSD и её преимущества

- **Масштабируемость и простота поддержки**: FSD обеспечивает четкую структуру и иерархию, которая сохраняется при росте проекта, упрощая его поддержку и развитие.
- **Удобство для новых разработчиков**: Благодаря единой концепции структурирования, новым членам команды легче ориентироваться в проекте, понимать его логику, находить и модифицировать компоненты.
- **Близость к бизнес-логике**: FSD отталкивается от доменной области и бизнес-сущностей, что делает архитектуру более понятной с точки зрения бизнеса.
- **Контролируемое переиспользование**: Методология помогает управлять переиспользованием логики и компонентов, предотвращая "мусорные" компоненты.

### Проблемы и их решения в FSD

Несмотря на преимущества, при работе с FSD могут возникать следующие проблемы:

1. **Кросс-импорты слайсов (Cross-imports)**
    - **Проблема**: FSD строго запрещает импорт кода из другого слайса в рамках текущего слоя. Это направлено на достижение низкой связанности и независимости модулей, но в реальных проектах сущности часто естественным образом взаимодействуют.
    - **Решение**:
        - **Паттерн инверсии зависимостей (Dependency Inversion)**: Использование контейнеров, глобальных сторов или контекста (в React) для прокидывания зависимостей вместо прямых импортов.
        - **Паттерн Render Props/Render Slots**: Передача компонентов в пропсах для рендеринга, что убирает прямую связь между компонентами. Однако это может усложнять компоненты и приводить к избыточным абстракциям.
        - **Новая фича `@/X` (публичный API для смежных слайсов)**: Позволяет легализовать кросс-импорты в явно связанных модулях. Для этого создается отдельный `index` файл (публичный API) для смежного слайса, который экспортирует только нужные модули.
2. **Размазывание кода по слоям (Code Scattering/Premature Decomposition)**
    - **Проблема**: Попытка избежать кросс-импортов и стремление использовать все шесть слоёв приводит к избыточному дроблению модулей и размазыванию кода по всей кодовой базе (так называемый "слайсовый ад").
    - **Решение**:
        - **Стратегия Local First**: Держать код максимально близко к месту его использования и не выносить его выше, пока в этом нет реальной необходимости.
        - **Подход Rich Domain Model для сущностей**: Делать сущности "умными" и полноценными модулями, которые знают, как получать, хранить и отображать данные, инкапсулируя локальные фичи и сценарии внутри себя.
3. **Субъективное понимание слоёв (What Goes Where?)**
    - **Проблема**: У разных разработчиков может быть свое субъективное понимание того, что является сущностью, фичей, виджетом и т.д., что приводит к разным подходам в одном и том же проекте.
    - **Решение**:
        - **Определение типа клиента (толстый/тонкий)**: FSD изначально разрабатывался для "толстых" клиентов (где много бизнес-логики на фронте). Для "тонких" клиентов (где большая часть логики на бэкенде) рекомендуется упрощенная версия FSD.
        - **Упрощенная версия FSD для тонких клиентов**: Исключает слои `entities` и `features` и фокусируется на подходе **Pages-first**. Все модули сначала собираются вокруг слоя `pages`, держатся там максимально локально, пока не понадобится их переиспользование где-то еще.
4. **Работа с инфраструктурой (Infrastructure Concerns)**
    - **Проблема**: В FSD нет явного слоя для инфраструктурных сервисов (например, аналитики, API-провайдеров, менеджеров тостов). Их часто размещают в `shared`, что приводит к размазыванию кода по сегментам этого слоя.
    - **Решение**: Выделение отдельного подслоя `shared/services` для таких модулей, что позволяет им быть изолированными друг от друга.
5. **Расширение методологии (Extending FSD)**
    - **Проблема**: Базовых слоёв FSD может не хватать для сложных проектов или из-за специфики предметной области.
    - **Решение**: FSD можно и нужно расширять, вводя дополнительные кастомные слои (например, абстрактные виджеты, фабрики для сущностей, слой для навигации/модальных окон) или даже верхнеуровневый слой `domains` для декомпозиции проекта на бизнес-домены (что хорошо подходит для монорепозиториев).

### Практическое применение и инструменты

- **Примеры**: На официальном сайте FSD и в сообществе есть примеры проектов.
- **Линтер Steiger**: Это архитектурный линтер для FSD, который помогает поддерживать структуру проекта согласно спецификации методологии. Он умеет работать с новыми фичами FSD, предотвращать преждевременную декомпозицию и проверять соблюдение правил, таких как кросс-импорты через публичный API.

В целом, FSD — это мощная архитектурная методология, которая, несмотря на некоторые проблемы (особенно с документацией и адаптацией для разных типов клиентов), активно развивается и позволяет создавать поддерживаемые и масштабируемые фронтенд-приложения.


---

### **Шпаргалка по элементам Feature-Sliced Design (FSD)**



### **1. Слои (Layers)**

**Слои** – это **стандартный набор регламентированных частей** проекта, которые структурируют его основные элементы. Ключевое правило слоев – **однонаправленные зависимости**: код может импортировать только из слоев, расположенных ниже (снизу вверх), но не наоборот.

В текущей версии FSD выделяется **шесть основных слоев**:

- **App (Приложение)**:
    - **Назначение**: **Корневой слой**, основа всего приложения. Содержит все, что необходимо для запуска проекта: **роутинг**, глобальные стили, инициализация сторов, точки входа (Entry Point), а также общие сервисы, такие как системы аналитики (Яндекс.Метрика, Google Analytics).
    - **Особенности**: **Не содержит слайсов**, но может иметь внутренние сегменты (например, `routes`, `store`, `styles`, `entry-point`).
- **Pages (Страницы)**:
    - **Назначение**: Представляют **полноценные страницы** приложения (например, `страница_товара`, `страница_корзины`, `профиль_пользователя`). Могут быть как частями многостраничных, так и основой одностраничных приложений.
    - **Особенности**: **Формируются из виджетов**. Могут содержать слайсы.
- **Widgets (Виджеты)**:
    - **Назначение**: **Крупные, самодостаточные и изолированные** блоки функциональности или интерфейса, ориентированные на конкретные пользовательские сценарии. Страница, как правило, состоит из набора виджетов. Виджеты агрегируют компоненты более низких уровней.
    - **Особенности**: Не обязательно являются переиспользуемыми во многих местах. Могут содержать слайсы.
- **Features (Фичи)**:
    - **Назначение**: **Переиспользуемые реализации продуктовых фич** или **пользовательских сценариев (юзкейсов)**. Отвечают на вопрос **"что сделать?"** (например, `лайкнуть_пост`, `оставить_комментарий`, `изменить_профиль`). Часто включают логику, связанную с действиями (например, счетчик изменения количества товаров).
    - **Особенности**: Это один из слоев, вызывающих наибольшую путаницу, поскольку понятие "фичи" в FSD отличается от общепринятого в продуктовой разработке. Могут содержать слайсы.
- **Entities (Сущности)**:
    - **Назначение**: **Бизнес-сущности** (объекты предметной области), с которыми работает проект (например, `пользователь`, `продукт`, `пост`, `комментарий`, `корзина`). Отвечают на вопрос **"что это?"**. Содержат описание моделей данных, интерфейсов, API-взаимодействий, сторов, контрактов, а также их UI-представления.
    - **Особенности**: Могут содержать слайсы.
- **Shared (Общее)**:
    - **Назначение**: Переиспользуемый код, который **не содержит никакой бизнес-логики** и не имеет специфики проекта или доменной области. Примеры: универсальные UI-компоненты (кнопки, инпуты, лейблы, чекбоксы), общие утилиты, вспомогательные функции, базовые API-клиенты.
    - **Особенности**: **Не содержит слайсов**, но может содержать сегменты. Инфраструктурные сервисы, не связанные с бизнес-логикой, часто размещаются в `shared` или в специальном подслое `shared/services`.

**Устаревший слой**: Ранее существовал слой **Processes**, который располагался между App и Pages и группировал страницы, относящиеся к одному процессу (например, авторизация, оформление заказа). Однако из-за переусложнения и частого вырождения он был исключен из текущей документации FSD.

**Подходы к реализации FSD**:

- **Для "толстого клиента"**: Если большая часть бизнес-логики и работы с данными сосредоточена на фронтенде, FSD рекомендуется проектировать, начиная с бизнес-сущностей (Entities-first).
- **Для "тонкого клиента"**: Если основная бизнес-логика находится на бэкенде, а фронтенд преимущественно запрашивает и отображает данные, рекомендуется использовать упрощенную версию FSD. В этом случае проектирование начинается вокруг слоя страниц (Pages-first), а слои Entities и Features могут быть исключены на начальном этапе. Весь код и локальные фичи сначала располагаются на уровне страниц, и только при явной необходимости выносятся в общие слои или переиспользуемые модули.

---

### **2. Слайсы (Slices)**

**Слайсы** – это второй уровень детализации. Они находятся **внутри слоев** (кроме App и Shared) и представляют собой **доменные области** или модули, на которые делится кодовая база. Название слайса **соответствует его названию в бизнес-логике** (например, `post`, `user`, `cart`, `payment`). Число слайсов неограничено и зависит от сложности приложения.

**Правильное деление на слайсы** основывается на двух критериях:

- **Высокая сцепленность (High Cohesion)**: Части кода, которые логически образуют единое целое, должны быть сгруппированы в один слайс.
- **Низкая связанность (Low Coupling)**: Слайсы должны быть максимально независимы друг от друга, чтобы их можно было легко изменять, удалять или переиспользовать без воздействия на другие части приложения.

**Ключевые принципы работы со слайсами**:

- **Стратегия Local First (Colocation)**: Держите код как можно ближе к месту его использования. Выносите код на более высокие слои или в общие модули только тогда, когда он действительно понадобится где-то еще. Это помогает избежать преждевременной декомпозиции и размазывания кода.
- **Public API для слайсов**: Каждый слайс должен явно определять свой **публичный API** через `index.ts` (или аналогичный файл), экспортируя только те части, которые доступны для использования во внешних модулях. Это предотвращает глубокие импорты и позволяет контролировать внешнее взаимодействие.
- **Решение для кросс-импортов**: **Кросс-импорты** (импорт кода из другого слайса в рамках того же слоя) **строго запрещены** в FSD, чтобы обеспечить независимость модулей. Однако для случаев, когда модули **явно связаны** и абстракции не имеют смысла, FSD 2.1 ввела **новую фичу – `@/x` нотацию** (например, `_product/x/cart`). Она позволяет явно описывать публичный API для смежных слайсов, требующих контролируемого кросс-импорта, что по сути **легализует необходимые прямые зависимости**.

---

### **3. Сегменты (Segments)**

**Сегменты** – это третий, самый низкий уровень детализации в FSD, позволяющий группировать код **по его техническому назначению** внутри слайса.

**Стандартные сегменты**:

- **UI**: UI-компоненты, верстка, все, что связано с отображением пользовательского интерфейса.
- **API**: Взаимодействие с бэкендом, функции запросов, типы данных, мапперы.
- **Model**: Модели данных, схемы, интерфейсы, хранилища состояний, бизнес-логика, относящаяся к конкретному слайсу.
- **Lib (Library)**: Библиотечный код, который нужен другим модулям этого слайса; может содержать общие утилиты или переиспользуемые части, аналогичные бывшим `utils`.
- **Config**: Файлы конфигурации, фича-флаги, точечные изменения, зависящие от окружения.

**Особенности сегментов**:

- Сегменты присутствуют **во всех слоях**, включая App и Shared (где нет слайсов). Например, `App/routes` или `Shared/UI`.
- Названия сегментов отвечают на вопрос **"для чего это нужно?"**, а не "что это такое?" (например, хуки, связанные с логикой, могут быть в `model`, а общие хуки – в `lib` или `shared`).
- **Public API для сегментов**: Как и для слайсов, каждый сегмент должен иметь свой **публичный API** (`index.ts` файл), который явно экспортирует только те части, предназначенные для внешнего использования.

---

### **Общие принципы и преимущества FSD**

- **Контролируемое переиспользование**: FSD поощряет повторное использование кода, но в рамках строгих правил, что предотвращает создание "мусорных" компонентов и цикличных зависимостей.
- **Гибкость и расширяемость**: FSD – это не жесткая догма. Методологию можно расширять, добавляя новые кастомные слои или пресеты в соответствии со спецификой проекта, если базового набора не хватает (например, `abstract-widgets`, `domains`, `shared-services`, `navigation`).
- **Упрощение онбординга**: Разработчик, знакомый с FSD, может быстро разобраться в любом проекте, структурированном по этой методологии, поскольку логика и расположение кода предсказуемы.
- **Устойчивость к изменениям**: Четкая структура и однонаправленные зависимости делают проект более стабильным и позволяют легко внедрять новые функции или изменять существующие без значительных проблем.
- **Решение проблем "размазывания кода"**: FSD помогает избежать ситуации, когда код оказывается разбросан по разным частям проекта, что затрудняет его поиск и поддержку.

---

