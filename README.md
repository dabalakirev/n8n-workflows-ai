# n8n-workflows-ai

![GitHub Issues](https://img.shields.io/github/issues/dabalakirev/n8n-workflows-ai)
![Platform Status](https://img.shields.io/badge/platform-v1.1--foundation-orange)
![License](https://img.shields.io/badge/license-Friends%20Only-purple)

**AI-Powered Automation Platform** для разработки n8n workflows с test-driven development и современными DevOps практиками

## 📋 Содержание
- [🎯 Обзор Платформы](#-обзор-платформы)
- [🐦 Текущий Проект: "First Bird"](#-текущий-проект-first-bird)
- [🛠️ Платформенные Инструменты](#️-платформенные-инструменты)
- [🗺️ Roadmap Платформы](#️-roadmap-платформы)
- [🏗️ Архитектура и Структура Окружения](#️-архитектура-и-структура-окружения)
- [🚀 Начало Работы](#-начало-работы)
- [🧪 Testing Framework Платформы](#-testing-framework-платформы)
- [🔧 Технологии Платформы](#-технологии-платформы)
- [🤝 Правила Разработки](#-правила-разработки)
- [🎯 Будущие Проекты](#-будущие-проекты)
- [📞 Поддержка Платформы](#-поддержка-платформы)
- [🌐 Языковая Политика Проекта](#-языковая-политика-проекта)
- [📄 Лицензия](#-лицензия)

## 🎯 Обзор Платформы

**n8n-workflows-ai** - это универсальная платформа для создания, тестирования и управления n8n automation проектами с использованием AI agents и structured development protocols.

### 🏗️ **Архитектура Платформы**

```
n8n-workflows-ai Platform
├── 🤖 AI Agent Protocols          # Structured development с AI
├── 🧪 Testing Framework           # Universal Test Orchestrator
├── 🚀 CI/CD Pipeline             # GitHub Actions automation
├── 📚 Documentation System       # Comprehensive guides & protocols
└── 📁 Projects                   # Individual automation projects
    └── 🐦 First Bird (current)   # Financial data automation
```

### ⚡ **Возможности Платформы**

- **AI-Assisted Development** с structured roles и protocols
- **Universal Testing Framework** через Test Orchestrator
- **Multi-Project Support** с DEV/PROD environment separation
- **Automated CI/CD** через GitHub Actions
- **Comprehensive Documentation** с protocols и best practices
- **Scalable Architecture** готовая для новых automation проектов

---

## 🐦 Текущий Проект: "First Bird"

**Financial Data Automation** - пилотный проект демонстрирующий возможности платформы

### **Область Проекта:**
- **Источник Данных:** Financial Modeling Prep API
- **AI Analysis:** Market insights и обработка финансовых данных
- **Цели Автоматизации:** Streamlined financial data workflows

### **Workflows Проекта:**
- **🤖 AI Deepseek** - Анализ финансовых данных с AI language model
- **🔗 FMP API Router** - Financial Modeling Prep API routing и data transformation

### **Статус Проекта:**
```
📊 First Bird Progress:        ██████████ 100% (workflows реализованы)
🧪 Testing Integration:        ████████░░  80% (Test Orchestrator готов)
📚 Documentation:              ████████░░  80% (protocols & guides готовы)
🚀 Production Readiness:       ███████░░░  70% (готов к deployment)
```

---

## 🛠️ Платформенные Инструменты

### 🧪 **Test Orchestrator** *(Universal Testing Tool)*
- **Назначение:** Automated testing для ЛЮБЫХ n8n workflows
- **Область:** Platform-level tool, не project-specific
- **Возможности:** Execute workflow testing, result aggregation, comprehensive reporting
- **Использование:** Работает со всеми проектами созданными на платформе

### 🚀 **GitHub Actions Pipeline**
- **Workflow Validation:** JSON structure и n8n schema validation
- **Issue Automation:** Labels, milestones, lifecycle management
- **Release Management:** Automated versioning и deployment
- **Quality Gates:** Automated testing перед production deployment

### 📚 **Documentation System**
- **AI Agent Protocols** - Structured development workflows
- **Development Guides** - Best practices и procedures
- **Security Standards** - Credential management и data protection
- **Testing Procedures** - Quality assurance processes

---

## 🗺️ Roadmap Платформы

### 📅 **Текущий Статус: Milestone v1.1 - Documentation & Infrastructure**
```
v1.1 Documentation & Infrastructure:  ██████████ 90% (platform foundation)
v1.2 Testing Framework:               ████░░░░░░ 40% (Test Orchestrator готов)
v1.3 Advanced Features:               ░░░░░░░░░░  0% (multi-project scaling)

Общий Прогресс Платформы:             ███████░░░ 75%
```

### 🎯 **Вехи Платформы:**
- **🏗️ v1.1 - Platform Foundation** (Сентябрь 2025) - *Documentation & Infrastructure*
  - Завершить AI Agent protocols и development procedures
  - Оптимизировать GitHub environment для productivity
  - Установить release и version management systems
  
- **🧪 v1.2 - Testing Framework** (Октябрь-Ноябрь 2025) - *Universal Testing Infrastructure*
  - Активировать Test Orchestrator для automated testing
  - Интегрировать testing с CI/CD pipeline
  - Установить quality gates для deployment
  
- **🚀 v1.3 - Multi-Project Platform** (Декабрь 2025) - *Scaling & Advanced Features*
  - Multi-project support и management
  - Performance optimization suite
  - Enterprise integrations и features

📖 **[Detailed Platform Roadmap →](docs/roadmap.md)**

---

## 🏗️ Архитектура и Структура Окружения

### **Multi-Environment Support:**
- **DEV Environment** - Development и testing (2 triggers: Manual + Execute Workflow)
- **PROD Environment** - Production deployments (1 trigger: Manual только)
- **Test Framework** - Automated quality assurance через Test Orchestrator

### **Структура Repository:**
```
├── workflows/           # Реализации project workflows
│   ├── dev/            # DEV версии с testing triggers
│   └── prod/           # PROD версии (production-ready)
├── docs/               # Документация платформы и protocols
│   ├── roadmap.md                       # Platform development roadmap
│   ├── ai-agent-execution-protocol.md   # AI Agent structured workflows
│   ├── ai-agent-roles-protocols.md     # AI Agent roles в SDLC
│   ├── context-handoff-protocol.md     # AI context transfer procedures
│   ├── testing-strategy.md             # Platform testing methodology
│   ├── github-issues-protocol.md       # Issue management procedures
│   ├── backup-essentials.md            # Data protection procedures
│   └── security-best-practices.md      # Security standards & guidelines
└── .github/
    ├── workflows/      # GitHub Actions (CI/CD automation)
    └── ISSUE_TEMPLATE/ # Standardized issue templates
```

---

## 🚀 Начало Работы

### **Для AI Agents:**
1. **Read AI Agent Execution Protocol** - обязательный workflow для всех assignments
2. **Study AI Agent Roles & Protocols** - понимание SDLC roles и processes
3. **Изучить все platform protocols** в `docs/` directory
4. **Проверить Platform Roadmap** для текущих приоритетов и milestone status
5. **Verify platform status** через `n8n_health_check`
6. **Follow 5-step execution flow** для каждого assignment
7. **ВАЖНО:** Изучить backup и security requirements перед major changes

### **Для Developers:**
1. Clone repository и изучить platform structure
2. Изучить **[Platform Roadmap](docs/roadmap.md)** для понимания архитектуры
3. Импортировать project workflows в n8n DEV/PROD environments
4. Настроить development environment следуя platform protocols
5. Следовать **[Security Best Practices](docs/security-best-practices.md)** для credentials
6. Следовать **[Backup Essentials](docs/backup-essentials.md)** перед major changes

### **Для Новых Проектов:**
1. Изучить platform architecture и существующую project structure
2. Создать project-specific workflows в DEV environment
3. Следовать platform testing procedures с Test Orchestrator
4. Использовать platform documentation templates и protocols
5. Deploy в PROD environment следуя установленным procedures

---

## 🧪 Testing Framework Платформы

### ✅ **Universal Test Orchestrator:**
- **Возможности:** Тестирует ЛЮБЫЕ n8n workflows созданные на платформе
- **Архитектура:** Platform-level tool обслуживающий все проекты
- **Интеграция:** Работает с DEV environments (dual triggers: Manual + Execute Workflow)
- **Автоматизация:** Интегрирован с GitHub Actions для automated testing
- **Scalability:** Готов тестировать множество проектов по мере роста платформы

### 📊 **Testing Methodology:**
- **DEV Workflows:** Dual triggers позволяют manual и automated testing
- **PROD Workflows:** Single manual trigger для production stability
- **Quality Gates:** Automated testing блокирует defective deployments
- **Test Coverage:** Цель 100% automation критических workflow paths

---

## 🔧 Технологии Платформы

- **n8n** - Core automation platform
- **GitHub** - Version control, project management, и CI/CD
- **GitHub Actions** - Automated pipeline и quality gates
- **GitHub Issues** - Structured task и change management
- **MCP (Model Context Protocol)** - AI agent platform integration
- **Test Orchestrator** - Universal workflow testing framework

---

## 📊 Метрики Платформы

- **Текущие Проекты**: 1 (First Bird - financial automation)
- **Platform Tools**: Test Orchestrator, GitHub Actions, Documentation System
- **Активные Issues**: 11 platform и project issues (смотри [GitHub Issues](../../issues))
- **Automation Coverage**: Цель 100% DEV workflows (в разработке)
- **Архитектура**: Multi-environment с контролируемой DEV → PROD migration
- **Документация**: Comprehensive coverage всех platform processes

---

## 🤝 Правила Разработки

### **Для всех Участников Платформы:**
1. **Следовать Platform Protocols** - все установленные процедуры обязательны
2. **No Changes Without Issues** - structured change management required
3. **Следовать Platform Roadmap** - выравнивание с milestone priorities
4. **Security First** - обязательные security practices (см. [Security Best Practices](docs/security-best-practices.md))
5. **Backup Before Major Changes** - защита данных required (см. [Backup Essentials](docs/backup-essentials.md))
6. **Universal Testing** - все изменения должны пройти Test Orchestrator validation
7. **Documentation Integration** - все архитектурные решения должны быть задокументированы
8. **Protocol Compliance** - установленные workflows должны соблюдаться

### **Для AI Agents:**
1. **Follow AI Agent Execution Protocol** - обязательно для каждого assignment
2. **Use Appropriate AI Agent Role** - согласно [AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)
3. **Context Integration** - читать platform documentation перед началом работы
4. **Roadmap Awareness** - проверять текущие priorities и milestones
5. **Issue Management** - создавать и обновлять Issues для всех планируемых изменений
6. **Documentation Updates** - поддерживать platform documentation с изменениями
7. **Security and Backup Compliance** - проверять requirements согласно protocols

---

## 🎯 Будущие Проекты

Платформа спроектирована для scalability и готова поддерживать дополнительные automation проекты:

- **Multi-Project Architecture** - Repository structure поддерживает project separation
- **Universal Testing Framework** - Test Orchestrator работает с любыми n8n workflows
- **Reusable Protocols** - AI Agent и development procedures применимы ко всем проектам
- **Scalable CI/CD** - GitHub Actions pipeline адаптируется к множеству проектов
- **Documentation Templates** - Установленные паттерны для new project documentation

---

## 📞 Поддержка Платформы

- **Issues**: Использовать GitHub Issues с standardized templates
- **Документация**: Comprehensive guides в `docs/` directory
- **Roadmap**: Текущий development status в [docs/roadmap.md](docs/roadmap.md)
- **AI Agent Support**: Следовать AI Agent Execution Protocol и Context Handoff Protocol
- **Security Support**: Security guidelines в [docs/security-best-practices.md](docs/security-best-practices.md)
- **Backup Support**: Recovery procedures в [docs/backup-essentials.md](docs/backup-essentials.md)

---

## 🌐 Языковая Политика Проекта

### **🇷🇺 Основной Язык: Русский**
Вся документация, комментарии, описания issues и коммуникация должны быть на русском языке для максимального понимания и доступности среди русскоязычной команды.

### **🔥 Англицизмы Приветствуются**
Мы используем англицизмы согласно следующей политике: активно применяем технические термины, устоявшиеся концепции, устойчивые выражения, а также выражения, которые претендуют стать устойчивыми - но избегаем превращения обычных слов в англицизмы без необходимости.

**В профессиональном контексте поощряется использование:**
- **Technical Terms**: workflows, CI/CD, testing framework, deployment
- **Development Terms**: commit, merge, pull request, issue, repository
- **Platform Terms**: scalability, automation, integration, orchestrator
- **Business Terms**: roadmap, milestones, deliverables, best practices

### **🎯 Translation Policy**
Специфические термины и концепции могут переводиться на английский для международной совместимости:
- **Friend Definition** вместо "Определение Друга"
- **Platform Architecture** alongside "Архитектура Платформы" 
- **Quality Gates** вместо "Шлюзы Качества"

### **✅ Best Practices:**
- Основной текст на русском с профессиональными англицизмами
- Технические термины остаются на английском
- Code comments предпочтительно на английском
- Issue titles могут содержать английские технические термины

---

## 📄 Лицензия

**Friends Only License v1.0** 🤝

Данный проект работает под эксклюзивными условиями лицензии "Только для друзей":

### **Разрешённые Пользователи:**
- **dabalakirev** (создатель проекта) ✅
- **Друзья dabalakirev** (explicitly approved individuals) ✅
- **AI Agents работающие с dabalakirev** (при правильной конфигурации) 🤖

### **Права Использования:**
- **Full access:** Создавать, изменять, использовать и deploy что угодно
- **Learning purposes:** Изучать код, документацию и архитектуру
- **Private use:** Запускать workflows для личных/дружеских проектов
- **Collaboration:** Работать вместе с dabalakirev над улучшениями

### **Ограничения:**
- ❌ **Commercial use** не-друзьями строго запрещено
- ❌ **Public redistribution** без явного разрешения
- ❌ **Corporate usage** неизвестными организациями запрещено
- ❌ **Reverse engineering** для конкурентных целей запрещено

### **🎯 Friend Definition:**
*"Friend" - это человек, которого dabalakirev искренне пригласил бы на кофе, помог бы debug код в 2 утра, или доверил бы пароль от WiFi.* ☕

### **Последствия при Нарушении:**
Неавторизованное использование приведёт к разочарованным взглядам, грустным эмодзи и потенциальному исключению из будущих кофейных приглашений. 😔

**Для licensing inquiries или проверки friend status, обращайтесь к dabalakirev напрямую.**

---

**Эта платформа демонстрирует современную AI-powered automation разработку со structured protocols, comprehensive security practices, universal testing framework, надёжными backup procedures и scalable multi-project architecture.**