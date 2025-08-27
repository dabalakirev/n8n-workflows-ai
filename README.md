# n8n-workflows-ai

**Test-Driven Automation Development** для n8n workflows с AI агентом

## 🎯 Описание проекта

Репозиторий содержит n8n workflows для автоматизации финансовых данных, разработанных с использованием AI агента и современных практик DevOps.

### Основные компоненты:
- **AI Deepseek** - AI-агент для анализа финансовых данных
- **FMP API Router** - маршрутизатор для Financial Modeling Prep API
- **Test Orchestrator** - система автоматизированного тестирования

## 🗺️ Project Roadmap

### 📅 **Current Status: Milestone v1.1 - Testing Framework**
```
v1.1 Testing Framework:     ████████░░ 80% (2/5 issues completed)
v1.2 Infrastructure:        ░░░░░░░░░░  0% (planning phase)
v1.3 Advanced Features:     ░░░░░░░░░░  0% (future planning)

Overall Project Progress:   ██████░░░░ 60%
```

### 🎯 **Active Milestones:**
- **🧪 v1.1 - Testing Framework** (Sept-Oct 2025) - *Priority: CRITICAL*
  - Issue #2: Create Test Orchestrator workflow ✅ *In Progress*
  - Issue #3: Add Execute Workflow Triggers ✅ *In Progress*
  - Next: Webhook setup & GitHub Actions integration
  
- **🏗️ v1.2 - Infrastructure & Automation** (Nov 2025) - *Priority: HIGH*
  - Full CI/CD pipeline with validation
  - Automated deployment DEV → PROD
  - Advanced monitoring & alerting

- **🚀 v1.3 - Advanced Features** (Dec 2025) - *Priority: MEDIUM*
  - Multi-environment support
  - Performance optimization
  - Enterprise integrations

📖 **[Детальный Roadmap →](docs/roadmap.md)**

## 🏗️ Архитектура

### Окружения:
- **DEV** - разработка и тестирование (2 триггера: Manual + Execute Workflow)
- **PROD** - продакшн версии (1 триггер: только Manual)
- **Test Framework** - автоматизированное тестирование через Test Orchestrator

### Структура репозитория:
```
├── workflows/           # JSON файлы n8n workflows
│   ├── dev/            # DEV версии с тестовыми триггерами
│   └── prod/           # PROD версии (только рабочие триггеры)
├── docs/               # Документация проекта
│   ├── roadmap.md                    # Project Roadmap с milestone
│   ├── context-handoff-protocol.md  # Передача контекста между AI агентами
│   ├── testing-strategy.md          # Стратегия тестирования с Test Orchestrator
│   └── github-issues-protocol.md    # Протокол работы с GitHub Issues
└── .github/
    ├── workflows/      # GitHub Actions (CI/CD)
    └── ISSUE_TEMPLATE/ # Шаблоны для Issues
```

## 🚀 CI/CD Pipeline

### ✅ **Активные GitHub Actions:**
- **📝 validate-workflows.yml** - Валидация JSON структуры и n8n схем
- **🎫 issue-automation.yml** - Автоматизация Issues (labels, milestones, validation)
- **🧪 test-orchestrator-placeholder.yml** - Placeholder для интеграции с Test Orchestrator

### 🚧 **В разработке:**
- **Test Orchestrator Integration** - автоматизированное тестирование (Issue #2)
- **Automated Deployment Pipeline** - DEV → PROD миграция
- **Advanced Monitoring** - performance и error tracking

## 📋 Протоколы и процессы

### ⚠️ ВАЖНО: Следование протоколам обязательно

Все участники проекта, включая AI агентов, должны строго следовать установленным протоколам:

#### 🎫 **GitHub Issues Protocol**
- **Обязательное создание Issues** для всех изменений workflow, багов, новых функций, тестирования и документации
- **Использование шаблонов** для стандартизации процесса
- **Lifecycle управление** от создания до закрытия Issue
- 📖 **[Полный протокол →](docs/github-issues-protocol.md)**

#### 🔄 **Context Handoff Protocol** 
- **Передача контекста** между AI агентами при смене чата
- **Структурированное документирование** состояния проекта
- **Continuous workflow** разработки
- 📖 **[Детали процедуры →](docs/context-handoff-protocol.md)**

#### 🧪 **Testing Strategy**
- **Test Orchestrator** для автоматизированного тестирования
- **Двойные триггеры** в DEV (Manual + Execute Workflow)
- **Валидация** перед переносом в PROD
- 📖 **[Стратегия тестирования →](docs/testing-strategy.md)**

## 🚀 Быстрый старт

### Для AI агентов:
1. Прочитать **все протоколы** в `docs/`
2. Проверить **Project Roadmap** для понимания текущих приоритетов
3. Проверить состояние проекта через `n8n_health_check`
4. **Создать Issue** перед любыми изменениями
5. Следовать установленным процедурам

### Для разработчиков:
1. Клонировать репозиторий
2. Изучить **[Roadmap](docs/roadmap.md)** для понимания архитектуры
3. Импортировать workflows в n8n
4. Настроить DEV/PROD проекты
5. Изучить документацию протоколов

## 🛠️ Технологии

- **n8n** - основная платформа автоматизации
- **GitHub** - версионирование и управление проектом
- **GitHub Actions** - CI/CD pipeline
- **GitHub Issues** - трекинг задач и изменений
- **MCP (Model Context Protocol)** - интеграция с AI агентами
- **Financial Modeling Prep API** - источник финансовых данных
- **DeepSeek API** - AI языковая модель

## 📊 Метрики проекта

- **Workflows**: 3 активных (AI Deepseek, FMP Router, Test Orchestrator)
- **Issues**: 4 active, 0 completed (view on [GitHub Issues](../../issues))
- **Automation**: GitHub Actions настроены для валидации и Issue management
- **Coverage**: Target 100% DEV workflows automation (в процессе разработки)
- **Environments**: DEV/PROD разделение с контролируемой миграцией
- **Documentation**: Полное покрытие всех процессов и архитектурных решений

## 🤝 Правила разработки

### Для всех участников:
1. **Никаких изменений** без Issues
2. **Следование Roadmap** и milestone приоритетам
3. **Обязательное тестирование** через Test Orchestrator (когда готов)
4. **Документирование** всех архитектурных решений
5. **Следование установленным протоколам**

### Для AI агентов:
1. **Читать контекст** из документации перед началом работы
2. **Проверять Roadmap** для понимания текущих приоритетов
3. **Создавать Issues** для всех планируемых изменений
4. **Валидировать workflows** перед коммитом
5. **Обновлять документацию** при изменениях

## 📞 Поддержка

- **Issues**: Использовать GitHub Issues с соответствующими шаблонами
- **Documentation**: Полная документация в папке `docs/`
- **Roadmap**: Актуальное планирование в [docs/roadmap.md](docs/roadmap.md)
- **AI Agent Support**: Следовать Context Handoff Protocol

---

**Этот проект демонстрирует современные практики разработки автоматизаций с использованием AI агентов, строгих протоколов, автоматизированного тестирования и структурированного roadmap планирования.**