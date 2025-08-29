# n8n-workflows-ai

![Platform Status](https://img.shields.io/badge/platform-v1.1--foundation-orange)
![License](https://img.shields.io/badge/license-Friends%20Only-purple)

**AI-Powered Automation Platform** для разработки n8n workflows с test-driven development и современными DevOps практиками

## 📋 Содержание
- [🎯 Обзор Платформы](#-обзор-платформы)
- [🐦 Текущий Проект: "First Bird"](#-текущий-проект-first-bird)
- [🛠️ Платформенные Инструменты](#️-платформенные-инструменты)
- [🗺️ Roadmap Платформы](#️-roadmap-платформы)
- [🏗️ Project-Centric Архитектура](#️-project-centric-архитектура)
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

### **Project Documentation:**
- **📖 [Project Overview](docs/projects/first-bird/README.md)** - Complete project details
- **🔗 [API Reference](docs/projects/first-bird/api-reference.md)** - FMP API integration guide
- **🛠️ [Workflow Guide](docs/projects/first-bird/workflow-guide.md)** - Usage instructions
- **⚙️ [Workflow README](workflows/first-bird/README.md)** - Technical workflow details

### **Статус Проекта:**
```
📊 First Bird Progress:        ██████████ 100% (workflows реализованы)
🧪 Testing Integration:        ████████░░  80% (Test Orchestrator готов)
📚 Documentation:              ██████████ 100% (complete project docs)
🚀 Production Readiness:       ████████░░  80% (готов к deployment)
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
- **Project-Centric Validation:** Multi-project structure compliance
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
v1.1 Documentation & Infrastructure:  ████████░░ 90% (project-centric complete)
v1.2 Testing Framework:               ████░░░░░░ 40% (Test Orchestrator готов)
v1.3 Advanced Features:               ░░░░░░░░░░  0% (multi-project scaling)

Общий Прогресс Платформы:             ████████░░ 80%
```

### 🎯 **Вехи Платформы:**
- **🏗️ v1.1 - Platform Foundation** (Сентябрь 2025) - *Documentation & Infrastructure*
  - ✅ Project-Centric Architecture реализована
  - ✅ AI Agent protocols и development procedures готовы
  - ✅ GitHub Actions optimized для multi-project support
  - 🔄 Release и version management systems (в процессе)
  
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

## 🏗️ Project-Centric Архитектура

### **Project Structure:**
```
workflows/
├── first-bird/             # Financial Data Automation project
│   ├── dev/                # DEV workflows (2 triggers each)
│   │   ├── ai-deepseek-dev.json      (Manual + Execute Workflow)
│   │   └── fmp-router-dev.json       (Manual + Execute Workflow) 
│   ├── prod/               # PROD workflows (1 trigger each)
│   │   ├── ai-deepseek-prod.json     (Manual only)
│   │   └── fmp-router-prod.json      (Manual only)
│   └── README.md           # Project-specific workflow documentation
├── [future-project]/       # Template для новых проектов
│   ├── dev/                # DEV environment для проекта
│   ├── prod/               # PROD environment для проекта  
│   └── README.md           # Project documentation
└── README.md              # Platform workflows guide
```

### **Documentation Structure:**
```
docs/
├── [платформенная документация]     # Universal protocols
└── projects/               # Project-specific documentation  
    └── first-bird/         # First Bird project docs
        ├── README.md       # Project overview
        ├── api-reference.md # FMP API documentation
        └── workflow-guide.md # Usage guide
```

### **Multi-Environment Support:**
- **DEV Environment** - Development и testing (2 triggers: Manual + Execute Workflow)
- **PROD Environment** - Production deployments (1 trigger: Manual только)
- **Test Framework** - Automated quality assurance через Test Orchestrator

### **Platform Navigation:**
- **📋 [Workflows Overview](workflows/README.md)** - Platform workflow architecture
- **🐦 [First Bird Project](workflows/first-bird/README.md)** - Project workflow details
- **📚 [Platform Protocols](docs/)** - Development guidelines и procedures

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
1. Clone repository и изучить project-centric structure
2. Изучить **[Platform Roadmap](docs/roadmap.md)** для понимания архитектуры
3. Изучить **[First Bird Project](docs/projects/first-bird/README.md)** как пример
4. Импортировать project workflows из `workflows/first-bird/` в n8n
5. Следовать **[Security Best Practices](docs/security-best-practices.md)** для credentials
6. Следовать **[Backup Essentials](docs/backup-essentials.md)** перед major changes

### **Для Новых Проектов:**
1. Изучить **[Platform Architecture](workflows/README.md)** и project structure
2. Создать new project папку в `workflows/[project-name]/`
3. Следовать project structure template: `dev/`, `prod/`, `README.md`
4. Создать project documentation в `docs/projects/[project-name]/`
5. Следовать platform testing procedures с Test Orchestrator
6. Deploy в PROD environment следуя установленным procedures

---

## 🧪 Testing Framework Платформы

### ✅ **Universal Test Orchestrator:**
- **Возможности:** Тестирует ЛЮБЫЕ n8n workflows созданные на платформе
- **Архитектура:** Platform-level tool обслуживающий все проекты
- **Project Support:** Работает с любой project structure
- **Интеграция:** Работает с DEV environments (dual triggers: Manual + Execute Workflow)
- **Автоматизация:** Интегрирован с GitHub Actions для automated testing
- **Scalability:** Готов тестировать множество проектов по мере роста платформы

### 📊 **Testing Methodology:**
- **DEV Workflows:** Dual triggers позволяют manual и automated testing
- **PROD Workflows:** Single manual trigger для production stability
- **Multi-Project Testing:** Test Orchestrator поддерживает все projects
- **Quality Gates:** Automated testing блокирует defective deployments
- **Test Coverage:** Цель 100% automation критических workflow paths

---

## 🔧 Технологии Платформы

- **n8n** - Core automation platform
- **GitHub** - Version control, project management, и CI/CD
- **GitHub Actions** - Automated pipeline и multi-project quality gates
- **GitHub Issues** - Structured task и change management
- **MCP (Model Context Protocol)** - AI agent platform integration
- **Test Orchestrator** - Universal workflow testing framework

---

## 📊 Метрики Платформы

- **Текущие Проекты**: 1 (First Bird - financial automation)
- **Platform Tools**: Test Orchestrator, GitHub Actions, Documentation System
- **Активные Issues**: 10 platform и project issues (смотри [GitHub Issues](../../issues))
- **Project Structure**: Project-centric architecture implemented
- **Automation Coverage**: Цель 100% DEV workflows (в разработке)
- **Архитектура**: Multi-project с контролируемой DEV → PROD migration
- **Документация**: Complete coverage всех platform и project processes

---

## 🤝 Правила Разработки

### **Для всех Участников Платформы:**
1. **Следовать Platform Protocols** - все установленные процедуры обязательны
2. **Project-Centric Structure** - новые проекты следуют установленной архитектуре
3. **No Changes Without Issues** - structured change management required
4. **Следовать Platform Roadmap** - выравнивание с milestone priorities
5. **Security First** - обязательные security practices (см. [Security Best Practices](docs/security-best-practices.md))
6. **Backup Before Major Changes** - защита данных required (см. [Backup Essentials](docs/backup-essentials.md))
7. **Universal Testing** - все изменения должны пройти Test Orchestrator validation
8. **Documentation Integration** - все project решения должны быть задокументированы

### **Для AI Agents:**
1. **Follow AI Agent Execution Protocol** - обязательно для каждого assignment
2. **Use Appropriate AI Agent Role** - согласно [AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)
3. **Project Context Awareness** - понимать project-specific requirements
4. **Platform Integration** - следовать universal protocols
5. **Issue Management** - создавать и обновлять Issues для всех планируемых изменений
6. **Documentation Updates** - поддерживать project и platform documentation

---

## 🎯 Будущие Проекты

Платформа спроектирована для scalability и готова поддерживать множественные automation проекты:

- **✅ Project-Centric Architecture** - Repository structure поддерживает unlimited projects
- **✅ Universal Testing Framework** - Test Orchestrator работает с любыми project workflows
- **✅ Reusable Protocols** - AI Agent и development procedures применимы ко всем проектам
- **✅ Scalable CI/CD** - GitHub Actions pipeline поддерживает multi-project validation
- **✅ Documentation Templates** - Установленные паттерны для new project documentation

### **Potential Future Projects:**
- **E-commerce Automation** (Shopify/WooCommerce APIs)
- **Social Media Management** (Twitter/LinkedIn automation)
- **IoT Data Processing** (sensor data workflows)
- **Content Management** (CMS/blogging automation)

---

## 📞 Поддержка Платформы

- **Issues**: Использовать GitHub Issues с standardized templates
- **Platform Documentation**: Comprehensive guides в `docs/` directory
- **Project Documentation**: Project-specific guides в `docs/projects/[project-name]/`
- **Workflow Documentation**: Technical details в `workflows/[project-name]/README.md`
- **Roadmap**: Текущий development status в [docs/roadmap.md](docs/roadmap.md)
- **AI Agent Support**: Следовать AI Agent Execution Protocol
- **Security Support**: Security guidelines в [docs/security-best-practices.md](docs/security-best-practices.md)
- **Backup Support**: Recovery procedures в [docs/backup-essentials.md](docs/backup-essentials.md)

---

## 🌐 Языковая Политика Проекта

### **📚 Основной Язык: Русский**
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

**Эта платформа демонстрирует современную AI-powered automation разработку с project-centric architecture, structured protocols, comprehensive documentation, universal testing framework и scalable multi-project support.**

*Updated: August 2025 - Issue #21 Project-Centric Architecture Implementation*