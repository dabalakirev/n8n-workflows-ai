# n8n-workflows-ai

**Test-Driven Automation Development** для n8n workflows с AI агентом

## 🎯 Описание проекта

Репозиторий содержит n8n workflows для автоматизации финансовых данных, разработанных с использованием AI агента и современных практик DevOps.

### Основные компоненты:
- **AI Deepseek** - AI-агент для анализа финансовых данных
- **FMP API Router** - маршрутизатор для Financial Modeling Prep API
- **Test Orchestrator** - система автоматизированного тестирования

## 🗺️ Project Roadmap

### 📅 **Current Status: Milestone v1.1 - Documentation & Infrastructure**
```
v1.1 Documentation & Infrastructure:  ██████████ 90% (7/10 issues completed)
v1.2 Testing Framework:               ██░░░░░░░░ 20% (ready for activation)
v1.3 Advanced Features:               ░░░░░░░░░░  0% (future planning)

Overall Project Progress:             ███████░░░ 75%
```

### 🎯 **Active Milestones:**
- **🏗️ v1.1 - Documentation & Infrastructure** (Sept 2025) - *Priority: CRITICAL*
  - Issue #16: Backup Essentials ✅ *COMPLETED*
  - Issue #8: AI Agent Roles & Protocols ⏳ *In Progress*
  - Issue #6: README Enhancement ⏳ *In Progress*
  - Next: GitHub optimization & release system
  
- **🧪 v1.2 - Testing Framework** (Oct-Nov 2025) - *Priority: HIGH*
  - Issue #2: Test Orchestrator workflow (ready for activation)
  - Issue #3: Execute Workflow Triggers (ready for activation)
  - Full CI/CD pipeline with validation

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
│   ├── roadmap.md                       # Project Roadmap с milestone
│   ├── ai-agent-execution-protocol.md   # AI Agent выполнение заданий
│   ├── ai-agent-roles-protocols.md     # AI Agent роли и SDLC процессы
│   ├── context-handoff-protocol.md     # Передача контекста между AI агентами
│   ├── testing-strategy.md             # Стратегия тестирования с Test Orchestrator
│   ├── github-issues-protocol.md       # Протокол работы с GitHub Issues
│   ├── backup-essentials.md            # Упрощенная backup стратегия
│   └── security-best-practices.md      # Безопасность credentials и данных
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

#### 🤖 **AI Agent Execution Protocol**
- **Обязательная последовательность** выполнения любого задания: Plan → Propose → Get Approval → Execute → Document
- **Mandatory system integration** для всей создаваемой документации
- **Фокус на командную работу** и документальное сопровождение
- 📖 **[Enhanced execution flow →](docs/ai-agent-execution-protocol.md)**

#### 👥 **AI Agent Roles & Protocols**
- **5 ролей AI агента** для SDLC процессов: Solution Architect, Developer, QA Engineer, Technical Writer, DevOps Engineer
- **Role switching protocol** и entry/exit criteria
- **Issues creation strategy** для каждой роли
- 📖 **[Полные роли и процедуры →](docs/ai-agent-roles-protocols.md)**

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

#### 💾 **Backup Essentials**
- **Manual backup procedures** для workflow JSON и credentials
- **Simple recovery guide** без enterprise complexity
- **Pre-change checklists** для critical workflow updates
- 📖 **[Backup procedures →](docs/backup-essentials.md)**

#### 🔐 **Security Best Practices**
- **Credentials management** и secure storage
- **API security** и access control
- **Data protection** и privacy guidelines
- 📖 **[Security guidelines →](docs/security-best-practices.md)**

## 📚 Документация

### **Core Documentation:**
- **[AI Agent Execution Protocol](docs/ai-agent-execution-protocol.md)** - обязательный workflow для AI агентов
- **[AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)** - роли и SDLC процессы
- **[GitHub Issues Protocol](docs/github-issues-protocol.md)** - управление задачами и изменениями
- **[Context Handoff Protocol](docs/context-handoff-protocol.md)** - передача контекста между AI
- **[Testing Strategy](docs/testing-strategy.md)** - автоматизированное тестирование
- **[Project Roadmap](docs/roadmap.md)** - планирование и milestone

### **Security & Operations:**
- **[Security Best Practices](docs/security-best-practices.md)** - защита credentials и данных
- **[Backup Essentials](docs/backup-essentials.md)** - защита критических данных

## 🚀 Быстрый старт

### Для AI агентов:
1. **Прочитать AI Agent Execution Protocol** - обязательный workflow для всех заданий
2. **Изучить AI Agent Roles & Protocols** - понимание ролей и SDLC процессов
3. Изучить **все остальные протоколы** в `docs/`
4. Проверить **Project Roadmap** для понимания текущих приоритетов
5. Проверить состояние проекта через `n8n_health_check`
6. **Следовать 5-step execution flow** для каждого задания
7. **ВАЖНО:** Проверять backup и security requirements перед major workflow changes

### Для разработчиков:
1. Клонировать репозиторий
2. Изучить **[Roadmap](docs/roadmap.md)** для понимания архитектуры
3. Импортировать workflows в n8n
4. Настроить DEV/PROD проекты
5. Изучить документацию протоколов
6. Следовать **[Security Best Practices](docs/security-best-practices.md)** для credentials
7. Следовать **[Backup Essentials](docs/backup-essentials.md)** перед изменениями

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
- **Issues**: 10 active, 2 completed (view on [GitHub Issues](../../issues))
- **Automation**: GitHub Actions настроены для валидации и Issue management
- **Coverage**: Target 100% DEV workflows automation (в процессе разработки)
- **Environments**: DEV/PROD разделение с контролируемой миграцией
- **Documentation**: Comprehensive coverage всех процессов и архитектурных решений

## 🤝 Правила разработки

### Для всех участников:
1. **Никаких изменений** без Issues
2. **Следование Roadmap** и milestone приоритетам
3. **Обязательное соблюдение security practices** (см. [Security Best Practices](docs/security-best-practices.md))
4. **Обязательный backup** перед major workflow changes (см. [Backup Essentials](docs/backup-essentials.md))
5. **Обязательное тестирование** через Test Orchestrator (когда готов)
6. **Документирование** всех архитектурных решений
7. **Следование установленным протоколам**

### Для AI агентов:
1. **Следовать AI Agent Execution Protocol** для каждого задания
2. **Использовать appropriate AI Agent Role** согласно [AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)
3. **Читать контекст** из документации перед началом работы
4. **Проверять Roadmap** для понимания текущих приоритетов
5. **Создавать Issues** для всех планируемых изменений
6. **Обновлять документацию** при изменениях
7. **Проверять security и backup requirements** согласно соответствующим protocols

## 📞 Поддержка

- **Issues**: Использовать GitHub Issues с соответствующими шаблонами
- **Documentation**: Полная документация в папке `docs/`
- **Roadmap**: Актуальное планирование в [docs/roadmap.md](docs/roadmap.md)
- **AI Agent Support**: Следовать AI Agent Execution Protocol и Context Handoff Protocol
- **Security Support**: Руководство по безопасности в [docs/security-best-practices.md](docs/security-best-practices.md)
- **Backup Support**: Руководство по восстановлению в [docs/backup-essentials.md](docs/backup-essentials.md)

---

**Этот проект демонстрирует современные практики разработки автоматизаций с использованием AI агентов, строгих протоколов, comprehensive security practices, автоматизированного тестирования, надежных backup procedures и структурированного roadmap планирования.**