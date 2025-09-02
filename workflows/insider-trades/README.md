# Insider Trades

**📊 AI-Powered Financial Data Automation System**

Автоматическая система мониторинга инсайдерских покупок с ИИ анализом и автоматической публикацией в Telegram.

---

## 📋 Architecture Documentation

### 🏠 **Архитектурная документация (Level 3):**

Полная спецификация n8n workflow из 25 узлов в 5 логических блоках:

#### 📁 **Block 1: Data Collection & Filtering**
- **[📄 Подробное описание](block-1-data-collection.md)**
- **Узлы 1-4:** Cron Trigger → FMP API → Data Filtering → Early Exit
- **Назначение:** Получение свежих инсайдерских сделок, строгая фильтрация
- **Статус:** ✅ **COMPLETE** - готово к implementation

#### 📂 **Block 2: Database Operations & Card Management**
- **[📄 Подробное описание](block-2-database-operations.md)**
- **Узлы 5-12:** Split Processing → MongoDB Operations → Status Logic → Card Management
- **Назначение:** Идемпотентная обработка, дедупликация, статусная модель
- **Статус:** ✅ **COMPLETE** - готово к implementation

#### 🤖 **Block 3: AI Analysis & Intelligence**
- **[📄 Подробное описание](block-3-ai-analysis.md)**
- **Узлы 13-17:** AI Agent + DeepSeek + SerpApi → Analysis Processing → Survey Insert
- **Назначение:** Автономный AI анализ компаний с web search
- **Статус:** ✅ **COMPLETE** - готово к implementation

#### 📝 **Block 4: Content Generation & Publishing**
- **[📄 Подробное описание](block-4-content-publishing.md)**
- **Узлы 18-23:** Telegraph API → Content Processing → Telegram Publishing
- **Назначение:** Создание статей, публикация с chart images
- **Статус:** ✅ **COMPLETE** - готово к implementation

#### 🏁 **Block 5: State Management & Completion**
- **[📄 Подробное описание](block-5-state-management.md)**
- **Узлы 24-25:** Survey Updates → Cycle Completion & Status Finalization
- **Назначение:** Финализация цикла, подготовка к следующему запуску
- **Статус:** ✅ **COMPLETE** - готово к implementation

---

## 🔧 Implementation Status

### 📊 **Общая готовность: 100% Level 3 Architecture**
- **✅ Все 5 блоков** полностью специфицированы
- **✅ Все 25 узлов** с детальными техническими спецификациями
- **✅ Полная архитектурная покрытость** - от Cron trigger до cycle completion
- **✅ Modular block structure** - обслуживаемая документация

### 🚀 **Implementation Workflow Structure:**
```
workflows/insider-trades/
├── dev/                     # DEV workflows ✏️ Нужно создать
├── prod/                    # PROD workflows 🚀 Нужно создать
├── README.md               # Этот файл
├── block-1-data-collection.md     ✅ Копия готова
├── block-2-database-operations.md  ✅ Копия готова
├── block-3-ai-analysis.md         ✅ Копия готова
├── block-4-content-publishing.md  ✅ Копия готова
└── block-5-state-management.md    ✅ Копия готова
```

---

## 🚀 Ready for Next Phase

### 🎦 **Available Next Steps:**

1. **🚀 [FEATURE] Issue Creation** - начало implementation phase
2. **👨‍💻 Developer Assignment** - actual workflow development  
3. **🧪 Incremental Testing** - block-by-block implementation с MCP webhook testing
4. **🔄 Production Deployment** - после DEV validation

### 🔧 **Technical Specifications Ready:**
- **6 API integrations:** FMP, DeepSeek, SerpApi, Telegraph, Telegram, MongoDB
- **25-node workflow:** Полная спецификация каждого узла
- **Error handling:** Comprehensive error handling strategy
- **Connection flow:** Полностью задокументированные связи
- **Credentials mapping:** Все необходимые credentials специфицированы

### 📊 **Key Features Designed:**
- **⚙️ Автономность:** 60-минутные циклы без вмешательства
- **🤖 AI Integration:** DeepSeek + Google Search автоматическая аналитика
- **📝 Контент:** Telegraph + Telegram публикация
- **🔄 Надёжность:** Idempotent design, error handling, audit trail
- **📊 Масштабируемость:** Модульная архитектура для расширений

---

**🏆 STATUS:** ✅ **IMPLEMENTATION READY** - готов к переходу от documentation к actual development phase  
**📅 Updated:** September 2, 2025