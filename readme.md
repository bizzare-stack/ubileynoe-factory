# 🍪 Завод «Юбилейное» — статический сайт

Демонстрационный статический сайт вымышленного завода по производству легендарного печенья **«Юбилейное»**. Проект создан как пример одностраничного приложения (SPA) на чистом HTML, CSS и JavaScript — без фреймворков и сборщиков.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📖 О проекте

Сайт рассказывает о вымышленном заводе, который производит печенье «Юбилейное» с 1913 года. Реализован как **одностраничное приложение** с клиентской навигацией: контент 5 страниц рендерится динамически через JavaScript без перезагрузки.

Проект подойдёт как:
- 🎓 учебный пример для изучения нативного JS и SPA-подхода;
- 🧩 шаблон для лендинга или корпоративного сайта небольшой компании;
- 🎨 референс по CSS-анимациям и адаптивной вёрстке.

---

## ✨ Возможности

- **5 страниц** с переключением без перезагрузки:
  - 🏠 **Главная** — hero-блок, преимущества завода, призыв к действию
  - 🏭 **О заводе** — история, ценности, факты о производстве
  - 🍪 **Продукция** — галерея сортов печенья
  - 📞 **Контакты** — адрес, телефоны, email, режим работы
  - ✉️ **Обратная связь** — форма с валидацией и подтверждением отправки
- **Анимации** — плавное появление блоков (`fadeUp`, `scaleIn`, `slideInLeft`), покачивание логотипа, hover-эффекты на карточках и кнопках
- **Адаптивная вёрстка** — корректно работает на десктопе, планшетах и смартфонах
- **Валидация формы** — проверка заполнения полей и корректности email
- **Иконки Font Awesome** — подключены через CDN
- **Единый стиль** — тёплая «печенюшная» палитра, подчёркивающая бренд

---

## 🏗 Архитектура приложения

```mermaid
graph TB
    User([👤 Пользователь])

    subgraph Browser["🌐 Браузер"]
        Header["📍 Header<br/>логотип + навигация"]
        Nav["🔗 Nav<br/>5 ссылок"]
        Main["📦 main#app<br/>контейнер контента"]
        Footer["🦶 Footer"]
        JS["⚙️ JavaScript<br/>pages + renderPage()"]
    end

    subgraph Pages["📄 Объект pages"]
        P1["🏠 home"]
        P2["🏭 about"]
        P3["🍪 products"]
        P4["📞 contacts"]
        P5["✉️ feedback"]
    end

    subgraph Assets["🎨 Внешние ресурсы"]
        FA["Font Awesome CDN"]
        CSS["CSS-анимации<br/>@keyframes"]
    end

    User -->|клик по ссылке| Nav
    Nav -->|data-page| JS
    JS -->|читает| Pages
    Pages -->|HTML-шаблон| Main
    Main -->|рендерит| User
    Header --> User
    Footer --> User
    FA --> Header
    FA --> Main
    CSS --> Main
    CSS --> Header

    style User fill:#fbe9d2,stroke:#8b4513,stroke-width:2px
    style JS fill:#f9d9a7,stroke:#8b4513,stroke-width:2px
    style Main fill:#fffbf2,stroke:#b87c4b,stroke-width:2px
    style Pages fill:#f5e5d3,stroke:#8b4513,stroke-width:2px
```

---

## 🔄 Схема навигации (SPA)

```mermaid
sequenceDiagram
    autonumber
    participant U as 👤 Пользователь
    participant N as 🔗 Nav
    participant R as ⚙️ renderPage()
    participant P as 📄 pages{}
    participant M as 📦 main#app

    U->>N: Клик по ссылке «Продукция»
    N->>R: renderPage('products')
    R->>P: Получить content для products
    P-->>R: HTML-шаблон
    R->>M: innerHTML = content
    R->>R: Обновить document.title
    R->>N: Подсветить активную ссылку
    R->>R: Навесить обработчики [data-page]
    M-->>U: Отобразить страницу
    Note over R,M: Перезагрузки страницы нет ✨
```

---

## 🧠 Логика работы формы обратной связи

```mermaid
flowchart TD
    Start([Пользователь открыл<br/>страницу feedback]) --> Init[initFeedbackForm]
    Init --> Fill[Заполняет поля формы]
    Fill --> Submit{Нажата кнопка<br/>«Отправить»}

    Submit -->|Нет| Fill
    Submit -->|Да| Validate{Валидация}

    Validate -->|Имя пустое| Err1[❌ Alert: заполните поля]
    Validate -->|Email пустой| Err1
    Validate -->|Сообщение пустое| Err1
    Validate -->|Email без @ или .| Err2[❌ Alert: некорректный email]

    Err1 --> Fill
    Err2 --> Fill

    Validate -->|Всё ок| Success[✅ Показать success-message]
    Success --> Reset[Очистить форму]
    Reset --> Timer[⏱ Таймер 5 сек]
    Timer --> Hide[Скрыть сообщение]
    Hide --> End([Готово])

    style Start fill:#fbe9d2,stroke:#8b4513,stroke-width:2px
    style Success fill:#d4edda,stroke:#155724,stroke-width:2px
    style Err1 fill:#f8d7da,stroke:#721c24,stroke-width:2px
    style Err2 fill:#f8d7da,stroke:#721c24,stroke-width:2px
    style End fill:#f9d9a7,stroke:#8b4513,stroke-width:2px
```

---

## 📂 Структура проекта

```mermaid
graph LR
    Root["📁 ubileynoe-factory/"]
    Root --> Index["📄 index.html<br/><i>разметка + стили + скрипты</i>"]
    Root --> Readme["📝 README.md"]
    Root --> Git["📁 .github/<br/><i>(опционально)</i>"]
    Git --> WF["⚙️ workflows/<br/>deploy.yml"]

    style Root fill:#8b4513,color:#fff5e6,stroke:#3e2c1b,stroke-width:2px
    style Index fill:#fbe9d2,stroke:#8b4513,stroke-width:2px
    style Readme fill:#f5e5d3,stroke:#b87c4b,stroke-width:2px
    style Git fill:#f0dcc5,stroke:#b87c4b,stroke-width:2px
```

```
ubileynoe-factory/
├── index.html      # Вся разметка, стили и скрипты в одном файле
└── README.md       # Этот файл
```

> Всё приложение уместилось в один HTML-файл: стили — в `<style>`, логика — в `<script>`. Такой подход удобен для демонстрации и быстрого деплоя на GitHub Pages.

---

## 🚀 Запуск

### Локально

1. Склонируйте репозиторий:
   ```bash
   git clone https://github.com/your-username/ubileynoe-factory.git
   ```
2. Перейдите в папку проекта:
   ```bash
   cd ubileynoe-factory
   ```
3. Откройте `index.html` в браузере (двойным кликом или через Live Server).

### GitHub Pages

```mermaid
flowchart LR
    A[📤 git push] --> B[🐙 GitHub repo]
    B --> C{⚙️ Settings → Pages}
    C --> D[Branch: main<br/>Folder: / root]
    D --> E[🚀 GitHub Pages build]
    E --> F[🌐 bizzare-stack.github.io/<br/>ubileynoe-factory/]

    style A fill:#fbe9d2,stroke:#8b4513,stroke-width:2px
    style F fill:#d4edda,stroke:#155724,stroke-width:2px
```

1. Запушьте проект в репозиторий на GitHub.
2. Перейдите в **Settings → Pages**.
3. Выберите ветку `main` и папку `/ (root)`.
4. Сохраните — сайт будет доступен по адресу `https://your-username.github.io/ubileynoe-factory/`.

> ⚠️ Файл **обязательно** должен называться `index.html` и лежать в корне — иначе GitHub Pages вернёт 404.

---

## 🧭 Как работает навигация

Контент всех страниц хранится в JS-объекте `pages`:

```javascript
const pages = {
  home:     { title: 'Главная',        content: `...` },
  about:    { title: 'О заводе',       content: `...` },
  products: { title: 'Продукция',      content: `...` },
  contacts: { title: 'Контакты',       content: `...` },
  feedback: { title: 'Обратная связь', content: `...` },
};
```

При клике по пункту меню вызывается `renderPage(pageKey)`, который:
1. подставляет HTML в `<main id="app">`;
2. обновляет `<title>` документа;
3. подсвечивает активную ссылку;
4. навешивает обработчики на внутренние кнопки навигации;
5. инициализирует форму, если открыта страница «Обратная связь».

---

## 📝 Форма обратной связи

Форма на странице «Обратная связь» включает поля:
- **Имя** (обязательное)
- **Email** (обязательное, с проверкой формата)
- **Тема обращения** (выпадающий список)
- **Сообщение** (обязательное, textarea)

После отправки:
- выполняется валидация;
- отображается сообщение об успехе (`<div class="success-message">`);
- форма сбрасывается;
- сообщение автоматически скрывается через 5 секунд.

> ⚠️ Сейчас данные **никуда не отправляются** — это демонстрация. Для реальной работы подключите бэкенд или сервис вроде Formspree / EmailJS.

---

## 🎨 Кастомизация

| Что менять | Где искать |
|------------|------------|
| Цвета бренда | CSS-переменные в `body` и `header` (`#8b4513`, `#fef9e9`, `#d4a373`) |
| Скорость анимаций | Значения `duration` в правилах `@keyframes` и `animation` |
| Тексты страниц | Объект `pages` в `<script>` |
| Иконки | Классы Font Awesome (`fa-cookie-bite`, `fa-industry` и т.д.) |
| Список продукции | Блок `.gallery` на странице `products` |

---

## 🌐 Совместимость

Проект протестирован в актуальных версиях:
- Chrome / Edge
- Firefox
- Safari
- Opera

Требуется поддержка ES6 и CSS-анимаций (все современные браузеры).

---

## 📄 Лицензия

Проект распространяется под лицензией **MIT** — используйте свободно в учебных и коммерческих целях.

> Бренд «Юбилейное» и логотипы являются собственностью их правообладателей. Сайт создан в демонстрационных целях и не связан с реальным производителем.

---

## 🙌 Благодарности

- [Font Awesome](https://fontawesome.com/) — за иконки
- Вдохновение — легендарному печенью «Юбилейное» 🍪

---

<p align="center">Сделано с любовью к печенью и чистому коду ❤️</p>