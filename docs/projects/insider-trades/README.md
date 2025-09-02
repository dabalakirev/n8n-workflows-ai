# Insider Trades

## Documentation Levels  
- **📝 Level 1:** [Бриф (идея)](brief-idea.md) - ✅ APPROVED
- **🔧 Level 2:** [Технический бриф](technical-brief.md) - ✅ APPROVED
- **🏗️ Level 3:** [Архитектурное решение](architecture.md) - ✅ COMPLETE (100%)
- **📋 Архитектурные тезисы:** [Architecture Theses](architecture_theses.md) - ✅ CREATED

## Implementation Status
- **Documentation:** ✅ All 3 levels complete and approved
- **Architecture:** ✅ Complete architectural solution (25 nodes in 5 blocks)
- **Node Specifications:** ✅ All blocks complete with detailed specifications
- **DEV:** 🚀 READY FOR IMPLEMENTATION
- **PROD:** ⏸️ Waiting for DEV completion

## Sequential Validation Status
- [x] **Level 1 APPROVED** - Business idea validated
- [x] **Level 2 APPROVED** - Technical specifications validated
- [x] **Level 3 COMPLETE** - Architectural solution 100% ready
- [x] **Architecture Theses APPROVED** - Core architectural decisions finalized
- [x] **All Blocks FINALIZED** - Complete node specifications (25 nodes)

## Level 3: Complete Architecture Documentation

**[Архитектурное решение](architecture.md)** - Полная спецификация 25 узлов n8n в 5 блоках:

### ✅ Завершенная архитектура (5/5 блоков):
- **✅ Block 1:** [Data Collection & Filtering](block-1-data-collection.md) - Узлы 1-4
  - Cron Trigger, FMP API, фильтрация, early exit logic
- **✅ Block 2:** [Database Operations & Card Management](block-2-database-operations.md) - Узлы 5-12  
  - Split processing, MongoDB операции, дедупликация, статусная модель
- **✅ Block 3:** [AI Analysis & Intelligence](block-3-ai-analysis.md) - Узлы 13-17
  - AI Agent + DeepSeek + SerpApi ecosystem, автономный web search
- **✅ Block 4:** [Content Generation & Publishing](block-4-content-publishing.md) - Узлы 18-23
  - Telegraph article creation, Telegram Bot publishing с inline кнопками
- **✅ Block 5:** [State Management & Completion](block-5-state-management.md) - Узлы 24-25
  - Survey updates, status transitions, cycle finalization

## Architectural Foundations
**[Architecture Theses](architecture_theses.md)** - Фундаментальные архитектурные решения:
- **Единый монолитный workflow** - 25 узлов в едином процессе
- **5 логических блоков** - модульная структура с четким разделением ответственности
- **Узловая архитектура** - принципы минимализма и максимальной эффективности
- **End-to-End optimization** - 60-минутный цикл с полной автоматизацией

## Technical Implementation Ready

### 🔧 **Complete Credentials Matrix:**
- **FMP API** - httpQueryAuth (узлы 2, 10)
- **MongoDB** - mongoDb (узлы 7, 12, 13, 17, 18, 22, 24)
- **DeepSeek API** - deepSeekApi (узел 15a)
- **SerpApi** - serpApi (узел 15b)
- **Telegraph API** - telegraphApi (узел 20)
- **Telegram Bot** - telegramBot (узел 23)

### 📊 **Complete Workflow Architecture:**
```
Block 1: 1→2→3→4[TRUE]→Block 2 | 4[FALSE]→END
Block 2: 5[Loop]→6→7→8→9[TRUE/FALSE]→10→11→12→5[Loop] | [Done]→Block 3
Block 3: 13→14[Loop]→15→16→17→14[Loop] | [Done]→Block 4
Block 4: 18→19[Loop]→20→21→22→23→19[Loop] | [Done]→Block 5
Block 5: 24→25→[CYCLE COMPLETE]
```

### 🎯 **AI Agent Ecosystem (Block 3):**
- **AI Agent (15)** ↔ **DeepSeek Chat Model (15a)** ↔ **SerpApi Tool (15b)**
- **Автономный web search** - AI принимает решения о поиске Google
- **Structured JSON output** - formatted QA pairs для Telegraph публикации

## Quick Reference
- **Business Goal:** Автоматический мониторинг инсайдерских покупок с ИИ анализом и публикацией в Telegram
- **Tech Stack:** FMP API, DeepSeek API, Telegraph, Telegram Bot, MongoDB, Finviz Charts, SerpApi
- **Architecture:** 60-минутный цикл, 25 узлов, статусная модель карточек (New/Renew/Old)
- **Data Flow:** 7-этапный процесс через 5 логических блоков
- **AI Integration:** Автономный AI Agent с web search capabilities

## Technical Specifications Summary
- **End-to-End процесс:** Complete 25-node workflow спецификация
- **API Интеграции:** 6 внешних сервисов полностью интегрированы
- **Data Structures:** MongoDB схемы коллекций deals и surveys
- **Business Logic:** Идемпотентная обработка с comprehensive error handling
- **AI Architecture:** DeepSeek + SerpApi для автономного анализа и web research
- **Publishing Pipeline:** Telegraph → Telegram с rich content formatting

---

**Project Status:** 🟢 IMPLEMENTATION READY - Complete architectural solution  
**Total Specification:** 25 nodes, 5 blocks, 6 API integrations, comprehensive error handling  
**Next Step:** Create [FEATURE] Issue для начала development phase