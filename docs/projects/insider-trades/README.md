# Insider Trades

## Documentation Levels  
- **📝 Level 1:** [Бриф (идея)](brief-idea.md) - ✅ APPROVED
- **🔧 Level 2:** [Технический бриф](technical-brief.md) - ✅ COMPLETE
- **🏗️ Level 3:** [Архитектурное решение](architecture.md) - ⏳ PENDING
- **📋 Архитектурные тезисы:** [Architecture Theses](architecture_theses.md) - ✅ CREATED

## Implementation Status
- **Documentation:** ✅ Level 1 & Level 2 complete, Level 3 pending
- **Architecture Foundations:** ✅ Core architectural decisions documented
- **DEV:** ⏸️ Waiting for Level 3 completion
- **PROD:** ⏸️ Waiting for DEV completion

## Sequential Validation Status
- [x] **Level 1 APPROVED** - Business idea validated
- [x] **Level 2 COMPLETE** - Technical specifications ready for validation
- [x] **Architecture Theses CREATED** - Core architectural decisions documented
- [ ] **Level 3 APPROVED** - Architecture design pending

## Architectural Foundations
**[Architecture Theses](architecture_theses.md)** - Фундаментальные архитектурные решения:
- **Единый монолитный workflow** - обоснование против sub-workflows
- **5 логических блоков** - структурированное разделение системы
- **Узловая архитектура** - принципы минимализма и эффективности
- **Оптимальность решения** - производительность, надежность, масштабируемость

## Quick Reference
- **Business Goal:** Автоматический мониторинг инсайдерских покупок с ИИ анализом и публикацией в Telegram
- **Tech Stack:** FMP API, DeepSeek API, Telegraph, Telegram Bot, MongoDB, Finviz Charts
- **Architecture:** 60-минутный цикл с статусной моделью карточек (New/Renew/Old)
- **Data Flow:** 7-этапный процесс: Сбор → Фильтрация → MongoDB → AI → Telegraph → Telegram → Архивирование

## Technical Specifications (Level 2)
- **End-to-End процесс:** Детализированный 7-этапный технический сценарий
- **API Интеграции:** 5 внешних сервисов полностью специфицированы
- **Data Structures:** MongoDB схемы коллекций deals и surveys
- **Business Logic:** Алгоритмы идемпотентности и статусной модели
- **Error Handling:** Стратегии для всех failure scenarios
- **AI Agent Architecture:** DeepSeek + SerpApi интеграция для автономного web search

---

**Project Status:** 🟡 Level 2 Complete, Architecture Foundations Set  
**Next Step:** Level 2 validation → Create Level 3: Архитектурное решение