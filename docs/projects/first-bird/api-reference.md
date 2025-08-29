# FMP API Reference - First Bird Project

**Financial Modeling Prep API** - справочник интеграции для проекта First Bird

## 🔗 Обзор API

**Base URL:** `https://financialmodelingprep.com`  
**Аутентификация:** Требуется API Key  
**Rate Limits:** Зависит от subscription plan  
**Документация:** [financialmodelingprep.com/developer/docs](https://financialmodelingprep.com/developer/docs)

## 🛠️ Поддерживаемые Endpoints

### **1. Insider Trading - Latest**
**Команда:** `Insider.Trading.Latest`  
**Endpoint:** `/stable/insider-trading/latest`  
**Метод:** GET

**Параметры:**
- `page` (опциональный): Номер страницы для pagination
- `limit` (опциональный): Количество записей для возврата

**Пример запроса:**
```json
{
  "toolName": "Insider.Trading.Latest",
  "params": {
    "page": 1,
    "limit": 10
  }
}
```

**Возвращаемые данные:**
- Детали транзакций (покупка/продажа)
- Информация о компании
- Имя и должность инсайдера  
- Даты транзакций и суммы
- Информация о ценах акций

### **2. Insider Trading - By Reporting Name**
**Команда:** `Insider.Trading.ReportingName`  
**Endpoint:** `/stable/insider-trading/reporting-name`  
**Метод:** GET

**Параметры:**
- `name` (обязательный): Имя инсайдера для поиска

**Пример запроса:**
```json
{
  "toolName": "Insider.Trading.ReportingName", 
  "params": {
    "name": "Elon Musk"
  }
}
```

**Случаи использования:**
- Отслеживание транзакций конкретных руководителей
- Мониторинг паттернов активности инсайдеров
- Исследование индивидуального торгового поведения

### **3. Insider Trading - Company Search**
**Команда:** `Insider.Trading.Search`  
**Endpoint:** `/stable/insider-trading/search`  
**Метод:** GET

**Параметры:**
- `symbol` (обязательный): Тикер компании
- `page` (опциональный): Номер страницы для pagination  
- `limit` (опциональный): Количество записей для возврата

**Пример запроса:**
```json
{
  "toolName": "Insider.Trading.Search",
  "params": {
    "symbol": "AAPL", 
    "page": 1,
    "limit": 20
  }
}
```

**Случаи использования:**
- Анализ инсайдерских операций конкретной компании
- Исследование исторических паттернов торговли
- Поддержка инвестиционных решений

### **4. Company Profile**
**Команда:** `Company.Profile`  
**Endpoint:** `/stable/profile`  
**Метод:** GET

**Параметры:**
- `symbol` (обязательный): Тикер компании

**Пример запроса:**
```json
{
  "toolName": "Company.Profile",
  "params": {
    "symbol": "MSFT"
  }
}
```

**Возвращаемые данные:**
- Название и описание компании
- Классификация по индустрии и сектору
- Рыночная капитализация
- Контактная информация
- Обзор бизнеса

## 🔧 Реализация Router

### **Таблица маршрутизации:**
```javascript
const routingTable = {
  'Insider.Trading.Latest': { path: '/stable/insider-trading/latest', paramIn: 'query' },
  'Insider.Trading.ReportingName': { path: '/stable/insider-trading/reporting-name', paramIn: 'query' },
  'Insider.Trading.Search': { path: '/stable/insider-trading/search', paramIn: 'query' },
  'Company.Profile': { path: '/stable/profile', paramIn: 'query' }
};
```

### **Обработка аутентификации:**
```javascript
// API key автоматически добавляется к каждому запросу
params.apikey = apiKey;
```

### **Построение URL:**
```javascript
// Query parameters автоматически кодируются
const queryParts = [];
for (const key in params) {
  if (params[key] !== undefined && params[key] !== null) {
    queryParts.push(encodeURIComponent(key) + '=' + encodeURIComponent(params[key]));
  }
}
finalUrl += '?' + queryParts.join('&');
```

## 📊 Форматы ответов API

### **Ответ Insider Trading:**
```json
[
  {
    "filingDate": "2024-01-15",
    "transactionDate": "2024-01-12", 
    "reportingName": "John Smith",
    "typeOfOwner": "Director",
    "securityName": "Common Stock",
    "symbol": "AAPL",
    "transactionType": "Buy",
    "sharesOwned": 1000,
    "pricePerShare": 150.25,
    "totalValue": 150250
  }
]
```

### **Ответ Company Profile:**
```json
[
  {
    "symbol": "AAPL",
    "companyName": "Apple Inc.", 
    "industry": "Consumer Electronics",
    "sector": "Technology",
    "description": "Apple Inc. проектирует, производит...",
    "ceo": "Tim Cook",
    "employees": 164000,
    "city": "Cupertino",
    "state": "California",
    "country": "United States"
  }
]
```

## ⚠️ Обработка ошибок

### **Распространенные сценарии ошибок:**

#### **Неверный API Key:**
```json
{
  "Error Message": "Invalid API key. Please retry or visit our documentation to create one FREE https://financialmodelingprep.com/developer/docs"
}
```

#### **Неверный символ:**
```json
{
  "Error Message": "Invalid symbol"
}
```

#### **Превышен лимит запросов:**
```json
{
  "Error Message": "API calls limit reached. Please upgrade your plan or wait until the next period."
}
```

### **Обработка ошибок в Router:**
```javascript
if (!route) {
  throw new Error(`Ошибка: Команда "${toolName}" не найдена в таблице маршрутизации.`);
}

if (!apiKey) {
  throw new Error('FMP API Key не настроен в конфигурации workflow.');
}
```

## 🔐 Лучшие практики безопасности

### **Управление API Key:**
- **Никогда не вставляйте** API keys в workflow файлы
- **Используйте n8n credentials** для secure key storage
- **Регулярно обновляйте** ключи для безопасности
- **Мониторьте использование** для выявления неожиданной активности

### **Защита данных:**
- **Финансовые данные** обрабатываются, но не хранятся long-term
- **Временная обработка** только в memory во время выполнения
- **Без логирования** sensitive financial information
- **Безопасная передача** только через HTTPS

## 📈 Оптимизация производительности

### **Эффективность API:**
- **Pagination** для больших datasets
- **Подходящие limits** предотвращают timeout issues
- **Кэширование** где применимо (будущее улучшение)
- **Batch requests** когда возможно

### **Rate Limiting:**
- **Мониторинг использования** против subscription limits
- **Реализация задержек** при приближении к лимитам
- **Error recovery** для rate limit scenarios
- **Отслеживание использования** для cost management

## 🧪 Процедуры тестирования

### **Тестирование Endpoints:**
```json
// Тестовые данные для каждого endpoint
{
  "Insider.Trading.Latest": { "limit": 5 },
  "Insider.Trading.ReportingName": { "name": "Elon Musk" },
  "Insider.Trading.Search": { "symbol": "AAPL", "limit": 5 },
  "Company.Profile": { "symbol": "MSFT" }
}
```

### **Критерии валидации:**
- **Структура ответа** соответствует ожидаемому формату
- **Типы данных** правильные для каждого поля
- **Обязательные поля** присутствуют в ответе
- **Обработка ошибок** правильная для invalid inputs

### **Автоматизация тестирования:**
- **DEV workflows** содержат test triggers
- **Test Orchestrator** integration для automated testing
- **Response validation** через automated checks
- **Performance monitoring** response times

## 🎯 Текущая интеграция (v1.2)

### **Активные workflows:**
- **✅ AI Deepseek DEV** (ID: 0VAipR4PLHbtkIzw) - использует FMP Router
- **✅ FMP API Router DEV** (ID: UmUET85BJqPbpRPp) - обрабатывает все FMP calls
- **✅ Test Orchestrator** (ID: ElnSprIVyJXKlkl3) - тестирует FMP integration

### **Test Orchestrator Integration:**
```json
// Пример тестового запроса
{
  "testData": {
    "fmp-router": {
      "toolName": "Insider.Trading.Latest",
      "params": { "limit": 5 }
    }
  }
}
```

## 🔄 Руководство по расширению

### **Добавление новых endpoints:**

1. **Обновить таблицу маршрутизации:**
```javascript
'New.Endpoint.Command': { path: '/stable/new-endpoint', paramIn: 'query' }
```

2. **Документировать параметры:**
```markdown
### **New Endpoint**
**Команда:** `New.Endpoint.Command`
**Параметры:** 
- `param1` (обязательный): Описание
```

3. **Добавить тест-кейсы:**
```json
{
  "toolName": "New.Endpoint.Command",
  "params": { "param1": "test_value" }
}
```

4. **Обновить описание AI Agent:**
- Добавить команду в description AI Agent tool
- Включить requirements параметров
- Предоставить примеры использования

### **Обслуживание:**
- **Регулярное тестирование** всех endpoints
- **Обновления документации** для изменений API
- **Мониторинг ошибок** для новых issues
- **Отслеживание производительности** для оптимизации

---

**Этот справочник API обеспечивает полное покрытие FMP integration для проекта First Bird с фокусом на безопасность, производительность и maintainability.**

*Последнее обновление: Август 2025 - v1.2 Testing Framework Active*