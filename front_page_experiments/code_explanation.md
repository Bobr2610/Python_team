# Объяснение кода финансовой панели

## Содержание
1. [HTML структура](#html-структура)
2. [CSS стили](#css-стили)
3. [JavaScript функционал](#javascript-функционал)
4. [JSON данные](#json-данные)

## HTML

### Основные компоненты

#### Сайдбар (`<aside class="sidebar">`)
- **Логотип с ссылкой наверх**
  ```html
  <div class="logo">
    <a href="#top" title="Наверх">
      <img src="Logo.png" alt="Логотип FIIT">
    </a>
  </div>
  ```
  - Использует семантический тег `<aside>` для боковой панели
  - Содержит логотип с якорем для быстрого возврата наверх
  - Включает атрибут `title` для подсказки при наведении

- **Навигационное меню с иконками**
  ```html
  <nav class="main-nav">
    <a href="#alerts" class="nav-item">
      <i class="fas fa-bell"></i>
      <span>Оповещения</span>
    </a>
    <!-- Другие пункты меню -->
  </nav>
  ```
  - Использует семантический тег `<nav>` для навигации
  - Каждый пункт меню содержит иконку и текст
  - Иконки загружаются через Font Awesome
  - Пункты меню имеют якоря для быстрой навигации

- **Секция отслеживаемых активов**
  ```html
  <div class="tracked-assets">
    <div class="section-header">
      <h3>Отслеживаемые активы</h3>
      <button class="refresh-btn" title="Обновить курсы">
        <i class="fas fa-sync-alt"></i>
      </button>
    </div>
    <div class="assets-list">
      <!-- Список активов -->
    </div>
  </div>
  ```
  - Отображает текущие курсы валют
  - Включает кнопку обновления данных
  - Использует сетку для отображения активов

#### Основной контент (`<div class="main-content">`)
- **Верхняя панель**
  ```html
  <div class="top-bar">
    <div class="account-group">
      <!-- Элементы аккаунта -->
    </div>
    <div class="theme-selector">
      <!-- Селектор темы -->
    </div>
  </div>
  ```
  - Содержит элементы управления аккаунтом
  - Включает переключатель тем оформления
  - Адаптивно изменяет расположение на мобильных устройствах

- **Секции контента**
  ```html
  <div class="chart-container" id="alerts">
    <!-- Секция оповещений -->
  </div>
  <div class="portfolio" id="portfolio">
    <!-- Секция портфеля -->
  </div>
  <div class="chart-container" id="news">
    <!-- Секция новостей -->
  </div>
  ```
  - Каждая секция имеет уникальный идентификатор
  - Использует единый стиль оформления
  - Поддерживает интерактивные элементы

### Особенности реализации
- **Семантические теги HTML5**
  - `<aside>` для боковой панели
  - `<nav>` для навигации
  - `<main>` для основного контента
  - `<section>` для логических разделов

- **Адаптивный дизайн**
  - Использование относительных единиц измерения
  - Медиа-запросы для разных размеров экрана
  - Гибкая сетка с использованием Grid и Flexbox

- **Доступность**
  - ARIA-атрибуты для улучшения навигации
  - Семантическая структура документа
  - Поддержка клавиатурной навигации
  - Альтернативные тексты для изображений

## CSS стили

### Система переменных
```css
:root {
  /* Размеры элементов интерфейса */
  --sidebar-width: 250px;
  --header-height: 60px;
  --border-radius: 8px;
  
  /* Отступы и промежутки */
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;
  
  /* Тени для создания глубины */
  --shadow-sm: 0 2px 4px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
  
  /* Скорость анимаций */
  --transition-speed: 0.3s;
  
  /* Типографика */
  --font-family: 'Roboto', sans-serif;
  --font-size-xs: 12px;
  --font-size-sm: 14px;
  --font-size-md: 16px;
  --font-size-lg: 18px;
  --font-size-xl: 24px;
  --font-size-2xl: 32px;
  
  /* Цвета графиков для светлой темы */
  --chart-btc-color: #ff9800;
  --chart-eth-color: #007bff;
  --chart-ton-color: #28a745;
  --chart-eur-color: #6f42c1;
  --chart-usd-color: #007bff;
  --chart-aed-color: #ff5722;
  --chart-cny-color: #28a745;
  
  /* Прозрачность для фона графиков */
  --chart-bg-opacity: 0.1;

  /* Значения по умолчанию для графиков */
  --chart-line-width: 2px;
  --chart-point-radius: 3px;
  --chart-point-hover-radius: 5px;
  --chart-point-border-width: 2px;
  --chart-point-hover-border-width: 3px;
  --chart-line-tension: 0.3;

  /* Стили точек по умолчанию */
  --chart-btc-point-style: 'circle';
  --chart-eth-point-style: 'circle';
  --chart-ton-point-style: 'circle';
  --chart-eur-point-style: 'circle';
  --chart-usd-point-style: 'circle';
  --chart-aed-point-style: 'circle';
  --chart-cny-point-style: 'circle';

  /* Типы линий по умолчанию */
  --chart-btc-border-dash: [];
  --chart-eth-border-dash: [];
  --chart-ton-border-dash: [];
  --chart-eur-border-dash: [];
  --chart-usd-border-dash: [];
  --chart-aed-border-dash: [];
  --chart-cny-border-dash: [];
}
```

### Темы
- **Светлая тема (по умолчанию)**
  ```css
  :root {
    --bg-primary: #ffffff;
    --text-primary: #2c3e50;
    --accent-primary: #3498db;
    /* ... */
  }
  ```
  - Использует светлые цвета фона
  - Контрастные цвета текста
  - Яркие акцентные цвета
  - Оптимизированные цвета для графиков

- **Темная тема**
  ```css
  [data-theme="dark"] {
    --bg-primary: #1a1a1a;
    --text-primary: #ffffff;
    --accent-primary: #3498db;
    /* ... */
    
    /* Цвета графиков для темной темы */
    --chart-btc-color: #ffa726;
    --chart-eth-color: #42a5f5;
    /* ... */
  }
  ```
  - Темные цвета фона
  - Светлые цвета текста
  - Сохранение контраста
  - Адаптированные цвета для графиков

- **Тема с высоким контрастом**
  ```css
  [data-theme="colorblind"] {
    --bg-primary: #ffffff;
    --text-primary: #000000;
    --accent-primary: #0000ff;
    /* ... */
    
    /* Цвета графиков для темы с высоким контрастом */
    --chart-btc-color: #0000ff;
    --chart-eth-color: #000080;
    /* ... */
  }
  ```
  - Максимальный контраст
  - Безопасные цвета для дальтоников
  - Увеличенные размеры элементов
  - Специально подобранные цвета для графиков

### Адаптивный дизайн
```css
@media (max-width: 768px) {
  .sidebar {
    width: 100%;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    border-right: none;
    border-bottom: 1px solid var(--border-color);
  }

  .sidebar nav {
    flex: 1;
    margin: 0 var(--spacing-sm);
    padding: var(--spacing-xs);
  }

  .sidebar nav a span {
    display: none; /* Скрываем текст на мобильных */
  }
}
```

### Особенности стилизации
- **Flexbox и Grid**
  ```css
  .main-content {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: var(--spacing-lg);
  }
  ```
  - Гибкая сетка для контента
  - Адаптивное расположение элементов
  - Автоматическое распределение пространства

- **Анимации и переходы**
  ```css
  .nav-item {
    transition: all var(--transition-speed) ease;
  }
  .nav-item:hover {
    transform: translateX(5px);
    background-color: var(--hover-bg);
  }
  ```
  - Плавные переходы состояний
  - Анимации при наведении
  - Эффекты при взаимодействии

- **Цветовая система графиков**
  ```css
  /* Определение цветов для каждой валюты */
  --chart-btc-color: #ff9800;
  --chart-eth-color: #007bff;
  /* ... */
  
  /* Прозрачность для фона */
  --chart-bg-opacity: 0.1;
  ```
  - Уникальные цвета для каждой валюты
  - Адаптация под разные темы
  - Оптимизация для дальтоников
  - Настраиваемая прозрачность фона

- **Стили графиков по умолчанию**
  ```css
  /* Значения по умолчанию для графиков */
  --chart-line-width: 2px;
  --chart-point-radius: 3px;
  --chart-point-hover-radius: 5px;
  --chart-point-border-width: 2px;
  --chart-point-hover-border-width: 3px;
  --chart-line-tension: 0.3;

  /* Стили точек по умолчанию */
  --chart-btc-point-style: 'circle';
  --chart-eth-point-style: 'circle';
  --chart-ton-point-style: 'circle';
  --chart-eur-point-style: 'circle';
  --chart-usd-point-style: 'circle';
  --chart-aed-point-style: 'circle';
  --chart-cny-point-style: 'circle';

  /* Типы линий по умолчанию */
  --chart-btc-border-dash: [];
  --chart-eth-border-dash: [];
  --chart-ton-border-dash: [];
  --chart-eur-border-dash: [];
  --chart-usd-border-dash: [];
  --chart-aed-border-dash: [];
  --chart-cny-border-dash: [];
  ```
  - Все значения по умолчанию определены в CSS переменных
  - Стили точек и типы линий задаются для каждой валюты отдельно
  - В теме с высоким контрастом эти значения переопределяются
  - JavaScript код просто использует эти переменные без дополнительной логики

- **Специальные стили для темы с высоким контрастом**
  ```css
  [data-theme="colorblind"] {
    /* Цвета графиков для темы с высоким контрастом */
    --chart-btc-color: #0000ff;
    --chart-eth-color: #000080;
    --chart-ton-color: #008000;
    --chart-eur-color: #800080;
    --chart-usd-color: #0000ff;
    --chart-aed-color: #ff0000;
    --chart-cny-color: #008000;
    
    /* Увеличенная толщина линий и размер маркеров */
    --chart-line-width: 3px;
    --chart-point-radius: 6px;
    --chart-point-hover-radius: 8px;
    --chart-point-border-width: 3px;
    --chart-point-hover-border-width: 4px;
  }
  ```
  - Максимально контрастные цвета для лучшей видимости
  - Увеличенная толщина линий (3px)
  - Крупные маркеры точек (6px)
  - Увеличенные маркеры при наведении (8px)
  - Толстые границы маркеров (3px)
  - Увеличенные границы при наведении (4px)
  - Оптимизированные цвета для дальтоников

### Специальные стили для темы с высоким контрастом
- Использование максимально контрастных цветов для лучшей видимости
- Увеличенная толщина линий (3px) для графиков
- Увеличенные маркеры точек (6px) и увеличенные размеры при наведении (8px)
- Толстые границы для маркеров (3px) и увеличенные границы при наведении (4px)
- Оптимизированные цвета для дальтоников
- Уникальные формы маркеров для каждой валюты:
  - BTC: круг
  - ETH: треугольник
  - TON: квадрат
  - EUR: звезда
  - USD: ромб
  - AED: крест
  - CNY: повернутый крест
- Разные типы линий для каждой валюты:
  - BTC: сплошная линия
  - ETH: пунктир (5,5)
  - TON: пунктир (10,5,5,5)
  - EUR: пунктир (5,10)
  - USD: пунктир (10,10)
  - AED: пунктир (5,5,5,5)
  - CNY: пунктир (15,5)

## JavaScript

### Основные функции

#### `generateLabels(start, count, isDaily)`
Генерирует метки времени для графиков:
- Для месячного интервала создает ежедневные метки
- Для остальных интервалов создает месячные метки
- Поддерживает форматирование дат для отображения

#### `combineYearlyData(yearlyData)`
Объединяет данные по годам в единый массив:
- Объединяет данные за 2023, 2024 и 2025 годы
- Используется для отображения долгосрочных графиков

#### `getDataForInterval(data, interval)`
Получает данные в зависимости от выбранного интервала:
- Для месячного интервала использует ежедневные данные
- Для остальных интервалов объединяет годовые данные
- Поддерживает все типы интервалов (1m, 6m, 1y, 3y)

#### `createChartConfig(type, data, options)`
Создает конфигурацию для графиков Chart.js:
- Получает стили из CSS переменных
- Настраивает цвета, размеры и стили точек
- Конфигурирует оси и подписи
- Поддерживает кастомные опции

### Функции управления темами

#### `handleThemeChange(e)`
Обрабатывает изменение темы через селектор:
- Сохраняет выбранную тему в localStorage
- Обновляет иконку темы
- Перезагружает страницу для применения новой темы

#### `handleThemeToggle()`
Обрабатывает переключение темы через кнопку:
- Циклически переключает между темами
- Обновляет селектор и localStorage
- Перезагружает страницу для применения новой темы

#### `updateThemeIcon(theme)`
Обновляет иконку темы:
- Устанавливает соответствующую иконку Font Awesome
- Поддерживает все типы тем (светлая, темная, высокий контраст)

### Инициализация и обновление графиков

#### `initializeCharts()`
Основная функция инициализации:
- Загружает данные из JSON файла
- Создает графики с дефолтными настройками
- Устанавливает обработчики событий

#### `updateCharts(interval)`
Обновляет графики при изменении интервала:
- Обновляет метки времени
- Пересчитывает данные для выбранного интервала
- Обновляет отображение графиков

#### `getMonthCount(interval)`
Определяет количество месяцев для интервала:
- Поддерживает все типы интервалов
- Возвращает соответствующее количество месяцев

## Взаимодействие компонентов

1. При загрузке страницы:
   - Инициализируются графики
   - Загружается сохраненная тема
   - Устанавливаются обработчики событий

2. При изменении интервала:
   - Обновляются метки времени
   - Пересчитываются данные
   - Обновляются графики

3. При смене темы:
   - Сохраняется новая тема
   - Обновляется иконка
   - Перезагружается страница для применения стилей

## Оптимизация производительности

1. Кэширование данных:
   - Данные загружаются один раз при инициализации
   - Переиспользуются при обновлении графиков

2. Эффективное обновление:
   - Обновляются только измененные данные
   - Минимизируется количество перерисовок

3. Оптимизация памяти:
   - Очистка неиспользуемых ресурсов
   - Эффективное управление объектами графиков

## JSON

### Структура данных
```json
{
  "crypto": {
    "BTC": {
      "2023": [16500, 23000, /* ... */],
      "2024": [43000, 48000, /* ... */],
      "2025": [93391.98, 94392.51, /* ... */],
      "daily_2025_01": [/* ... */]
    },
    "ETH": { /* ... */ },
    "TON": { /* ... */ }
  },
  "fiat": {
    "EUR/RUB": { /* ... */ },
    "USD/RUB": { /* ... */ },
    "AED/RUB": { /* ... */ },
    "CNY/RUB": { /* ... */ }
  }
}
```

### Типы данных
- **Исторические данные**
  - Ежемесячные значения за 2023-2025 годы
  - Структурированы по годам для удобства
  - Поддерживают разные временные интервалы

- **Ежедневные данные**
  - Подробные значения за январь 2025
  - Используются для краткосрочного анализа
  - Обновляются в реальном времени

### Особенности
- **Организация данных**
  - Разделение на криптовалюты и фиат
  - Иерархическая структура
  - Легкое масштабирование

- **Временные интервалы**
  - Поддержка разных периодов
  - Гибкая система обновления
  - Оптимизированное хранение

## Технические особенности

### Производительность
- **Оптимизация загрузки**
  ```html
  <script src="scripts.js" defer></script>
  <link rel="preload" href="styles.css" as="style">
  ```
  - Асинхронная загрузка скриптов
  - Предварительная загрузка стилей
  - Оптимизация ресурсов

- **CSS оптимизации**
  ```css
  .chart-container {
    will-change: transform;
    transform: translateZ(0);
  }
  ```
  - Аппаратное ускорение
  - Оптимизация анимаций
  - Эффективное использование памяти

### Доступность
- **ARIA-атрибуты**
  ```html
  <button 
    class="theme-toggle" 
    aria-label="Переключить тему"
    aria-expanded="false"
  >
    <i class="fas fa-moon"></i>
  </button>
  ```
  - Описательные метки
  - Состояния элементов
  - Роли компонентов

- **Клавиатурная навигация**
  ```css
  .nav-item:focus {
    outline: 2px solid var(--accent-primary);
    outline-offset: 2px;
  }
  ```
  - Визуальные индикаторы фокуса
  - Логический порядок табуляции
  - Поддержка горячих клавиш

### Адаптивность
- **Медиа-запросы**
  ```css
  @media (max-width: 768px) {
    /* Мобильная версия */
  }
  @media (min-width: 769px) and (max-width: 1024px) {
    /* Планшетная версия */
  }
  @media (min-width: 1025px) {
    /* Десктопная версия */
  }
  ```
  - Разные макеты для устройств
  - Адаптивные размеры шрифтов
  - Оптимизированные отступы

### Безопасность
- **Валидация данных**
  ```javascript
  function validateData(data) {
    if (!data || typeof data !== 'object') {
      throw new Error('Invalid data format');
    }
    // Дополнительные проверки
  }
  ```
  - Проверка формата данных
  - Обработка ошибок
  - Безопасное хранение

- **Защита от XSS**
  ```javascript
  function sanitizeInput(input) {
    return input.replace(/[<>]/g, '');
  }
  ```
  - Экранирование данных
  - Безопасный вывод
  - Валидация ввода 

## API Интеграции

### Московская биржа (MOEX)

#### Структура ответа API
```json
{
  "securities": {
    "metadata": {
      "SECID": {"type": "string", "bytes": 36},
      "BOARDID": {"type": "string", "bytes": 12},
      "PREVPRICE": {"type": "double"},
      "STATUS": {"type": "string", "bytes": 3}
      // ... другие поля метаданных
    },
    "columns": ["SECID", "BOARDID", "SHORTNAME", "LOTSIZE", "SETTLEDATE", "DECIMALS", "FACEVALUE", "MARKETCODE", "MINSTEP", "PREVDATE", "SECNAME", "REMARKS", "STATUS", "FACEUNIT", "PREVPRICE", "PREVWAPRICE", "CURRENCYID", "LATNAME", "LOTDIVIDER"],
    "data": [
      ["EUR000TODTOM", "AUCB", "EUR_TODTOM", 100000, "2025-03-21", 6, 1, "CURR", 0.0001, "2025-03-20", "EUR_TODTOM - СВОП EUR/РУБ", null, "A", "EUR", null, null, "RUB", "EUR_TODTOM - SWAP EUR/RUB", 1],
      // ... другие инструменты
    ]
  }
}
```

#### Ключевые поля
- `SECID` - уникальный идентификатор инструмента
- `BOARDID` - идентификатор торговой площадки
- `PREVPRICE` - предыдущая цена закрытия
- `STATUS` - статус инструмента (A - активный)
- `CURRENCYID` - базовая валюта инструмента

#### Идентификаторы инструментов
- USD: `USD000UTSTOM` (TOM)
- EUR: `EUR_RUB__TOM` (TOM)
- CNY: `CNYRUB_TOM` (TOM)
- AED: `AEDRUB_TOM` (TOM)

#### Обработка данных
```javascript
async function getFiatPricesFromMOEX() {
  try {
    const response = await fetch('https://iss.moex.com/iss/engines/currency/markets/selt/securities.json');
    const data = await response.json();
    
    const prices = {};
    const securities = data.securities.data;
    const columns = data.securities.columns;
    
    // Определяем индексы нужных колонок
    const secIdIndex = columns.indexOf('SECID');
    const prevPriceIndex = columns.indexOf('PREVPRICE');
    const boardIdIndex = columns.indexOf('BOARDID');
    
    securities.forEach(security => {
      const secId = security[secIdIndex];
      const boardId = security[boardIdIndex];
      const price = parseFloat(security[prevPriceIndex]);
      
      // Используем только активные инструменты с ценой
      if (security[columns.indexOf('STATUS')] === 'A' && !isNaN(price)) {
        // Обработка курсов для разных валют
        if (secId === 'USD000UTSTOM') prices.USD = price;
        else if (secId === 'EUR_RUB__TOM') prices.EUR = price;
        else if (secId === 'CNYRUB_TOM') prices.CNY = price;
        else if (secId === 'AEDRUB_TOM') prices.AED = price;
      }
    });
    
    return prices;
  } catch (error) {
    console.error('Ошибка при получении курсов фиатных валют:', error);
    return null;
  }
}
```

### Binance API

#### Получение курсов криптовалют
```javascript
async function getBTCPriceFromBinance() {
  try {
    // Получаем курс BTC/USDT
    const btcUsdtResponse = await fetch('https://api.binance.com/api/v3/ticker/price?symbol=BTCUSDT');
    const btcUsdtData = await btcUsdtResponse.json();
    const btcUsdtPrice = parseFloat(btcUsdtData.price);

    // Получаем курс USDT/RUB
    const usdtRubResponse = await fetch('https://api.binance.com/api/v3/ticker/price?symbol=USDTRUB');
    const usdtRubData = await usdtRubResponse.json();
    const usdtRubPrice = parseFloat(usdtRubData.price);

    // Рассчитываем курс BTC в рублях
    return btcUsdtPrice * usdtRubPrice;
  } catch (error) {
    console.error('Ошибка при получении курса BTC:', error);
    return null;
  }
}
```

#### Особенности работы с API
- Использование Promise.all для параллельных запросов
- Обработка ошибок и валидация данных
- Кэширование результатов
- Автоматическое обновление курсов 