# n8n-workflows-ai

![Platform Status](https://img.shields.io/badge/platform-v1.2--release--ready-brightgreen)
![Release System](https://img.shields.io/badge/releases-automated-blue)
![License](https://img.shields.io/badge/license-Friends%20Only-purple)

**AI-Powered Automation Platform** для разработки n8n workflows с test-driven development и современными DevOps практиками

## 📋 Содержание
- [🎯 Обзор Платформы](#-обзор-платформы)
- [🏷️ Releases & Versioning](#️-releases--versioning)
- [🐦 Текущий Проект: "First Bird"](#-текущий-проект-first-bird)
- [🛠️ Платформенные Инструменты](#️-платформенные-инструменты)
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
├── 🧪 Testing Framework           # ✅ Test Webhook - Test Execution подход
├── 🏷️ Release Management         # ✅ Automated GitHub Releases & Tags
├── 🚀 CI/CD Pipeline             # GitHub Actions automation
├── 📚 Documentation System       # Comprehensive guides & protocols
└── 📁 Projects                   # Individual automation projects
    └── 🐦 First Bird (current)   # Financial data automation [АРХИТЕКТУРНАЯ ПОДГОТОВКА]
```

### ⚡ **Возможности Платформы**

- **AI-Assisted Development** с structured roles и protocols
- ✅ **Simplified Testing Framework** через Test Webhook - Test Execution подход
- ✅ **Professional Release Management** с automated versioning и GitHub Releases
- **Multi-Project Support** с DEV/PROD environment separation
- **Automated CI/CD** через GitHub Actions
- **Comprehensive Documentation** с protocols и best practices
- **Scalable Architecture** готовая для новых automation проектов

---

## 🏷️ Releases & Versioning

### ✅ **Release System - OPERATIONAL**
Платформа использует professional semantic versioning с automated GitHub Releases для обеспечения качественных deployments и upgrade paths.

#### **📅 Current Version Status:**
- **🔖 Ready for Release:** v1.2.0 "Simplified Testing Framework"
- **🚀 Release System:** ✅ Automated GitHub Actions workflow 
- **📦 Artifacts:** Automated workflow + documentation packaging
- **🏷️ Git Tags:** Professional semantic versioning

#### **🎯 Versioning Strategy:**
```
v1.2.0 - "Simplified Testing Framework" (READY - First Official Release)
v1.3.0 - "First Bird Complete" (Final project validation & production deployment)  
v1.4.0 - "Multi-Project Platform" (Advanced features & scaling)
v2.0.0 - "Enterprise Platform" (Breaking changes & major evolution)
```

#### **🚀 How to Create Release:**
```bash
# Using GitHub Actions (Manual Trigger)
# Navigate to: Actions → 🏷️ Create Release → Run workflow
# Input: version (v1.2.0), type (stable), name (Simplified Testing Framework)

# Or via GitHub Web Interface
# Navigate to: Releases → Create a new release
# Use prepared release notes and upload artifacts
```

---

## 🐦 Текущий Проект: "First Bird"

**Financial Data Automation** - пилотный проект демонстрирующий возможности платформы

### **Область Проекта:**
- **Источник Данных:** Financial Modeling Prep API
- **AI Analysis:** Market insights и обработка финансовых данных
- **Цели Автоматизации:** Streamlined financial data workflows

### **Workflows Проекта:**
- **🤖 AI Deepseek** - Анализ финансовых данных с AI language model (Parent Workflow)
- **🔗 FMP API Router** - Financial Modeling Prep API routing и data transformation (Child Workflow)

### **Project Documentation:**
- **📖 [Project Overview](docs/projects/first-bird/README.md)** - Complete project details
- **🔗 [API Reference](docs/projects/first-bird/api-reference.md)** - FMP API integration guide
- **🛠️ [Workflow Guide](docs/projects/first-bird/workflow-guide.md)** - Usage instructions
- **⚙️ [Workflow README](workflows/first-bird/README.md)** - Technical workflow details

### **🔄 Current Status: Архитектурная подготовка**
```
📊 First Bird Progress:        ████████░░  80% (workflows созданы, архитектурные изменения в progress)
🧪 Testing Integration:        ██████░░░░  60% ✅ (Test Webhook - Test Execution approach в разработке)
🚀 Production Readiness:       ████░░░░░░  40% (pending новый testing approach)
```

- **⚠️ ТЕКУЩАЯ ФАЗА:** Архитектурное обновление testing framework (Issue #26)
- **🧪 Active Issue:** [#26 - Test Webhook - Test Execution подход](https://github.com/dabalakirev/n8n-workflows-ai/issues/26)
- **🎯 Цель:** Подготовка к simplified testing architecture перед final validation

---

## 🛠️ Платформенные Инструменты

### 🧪 **Testing Framework - Test Webhook - Test Execution** *(✅ АРХИТЕКТУРНО ГОТОВ)*
- **Подход:** ✅ **Simplified Direct Testing** - parent workflows тестируются через dedicated test webhooks
- **Архитектура:** Parent workflow → естественное выполнение → Child workflows → мониторинг результатов
- **Преимущества:** Упрощенная архитектура, естественное выполнение, лучший debugging
- **Status:** ✅ **Protocol-level готов** - implementation в planning phase

### 🏷️ **Release Management System** *(✅ OPERATIONAL - Professional Versioning)*
- **Status:** ✅ **FULLY OPERATIONAL** - Ready for first release v1.2.0
- **GitHub Action:** `.github/workflows/create-release.yml` - Complete automation
- **Versioning:** Semantic versioning с professional release notes
- **Artifacts:** Automated workflow + documentation packaging

### 🚀 **GitHub Actions Pipeline**
- **Workflow Validation:** JSON structure и n8n schema validation
- **Project-Centric Validation:** Multi-project structure compliance
- **Issue Automation:** Labels, milestones, lifecycle management
- **Quality Gates:** Automated testing перед production deployment

### 📚 **Documentation System**
- **AI Agent Protocols** - Structured development workflows
- **✅ Testing Strategy** - Updated с Test Webhook - Test Execution подходом
- **MCP CI/CD Deployment Protocol** - Comprehensive development lifecycle procedures
- **Development Guides** - Best practices и procedures
- **Security Standards** - Credential management и data protection

---

## 🏗️ Project-Centric Архитектура

### **Project Structure:**
```
workflows/
├── first-bird/             # Financial Data Automation project [АРХИТЕКТУРНАЯ ПОДГОТОВКА]
│   ├── dev/                # DEV workflows - готовы для test webhook integration
│   │   ├── ai-deepseek-dev.json      (Manual + будущий Test Webhook)
│   │   └── fmp-router-dev.json       (Manual + Execute Workflow)
│   ├── prod/               # PROD workflows (1 trigger each)
│   │   ├── ai-deepseek-prod.json     (Manual only) [FUTURE]
│   │   └── fmp-router-prod.json      (Manual only) [FUTURE]
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
│   ├── testing-strategy.md          # ✅ Updated с новым подходом
│   └── ai-agent-roles-protocols.md  # ✅ Updated с testing integration
└── projects/               # Project-specific documentation  
    └── first-bird/         # First Bird project docs
        ├── README.md       # Project overview
        ├── api-reference.md # FMP API documentation
        └── workflow-guide.md # Usage guide
```

### **Multi-Environment Support:**
- **DEV Environment** - Development и testing (2 triggers: Manual + Test Webhook для parent)
- **PROD Environment** - Production deployments (1 trigger: Manual только)
- ✅ **Test Framework** - ✅ **ГОТОВ** simplified testing architecture через test webhooks
- ✅ **Release Management** - ✅ **OPERATIONAL** professional versioning и deployment

### **Platform Navigation:**
- **📋 [Workflows Overview](workflows/README.md)** - Platform workflow architecture
- **🐦 [First Bird Project](workflows/first-bird/README.md)** - Project workflow details  
- **📚 [Platform Protocols](docs/)** - Development guidelines и procedures
- **✅ [Testing Strategy](docs/testing-strategy.md)** - New Test Webhook - Test Execution подход
- **🗺️ [Platform Roadmap](docs/roadmap.md)** - Development timeline и milestones

---

## 🚀 Начало Работы

### **Для AI Agents:**
1. **Read AI Agent Execution Protocol** - обязательный workflow для всех assignments
2. **Study AI Agent Roles & Protocols** - понимание SDLC roles и processes с new testing approach
3. **Изучить все platform protocols** в `docs/` directory
4. **Проверить Platform Roadmap** для текущих приоритетов и milestone status
5. **Verify platform status** через `n8n_health_check`
6. ✅ **Use Test Webhook Approach** - simplified testing для всех workflow changes
7. ✅ **Follow Release Procedures** - use professional release management
8. **Follow 5-step execution flow** для каждого assignment
9. **ВАЖНО:** Изучить backup и security requirements перед major changes

### **Для Developers:**
1. Clone repository и изучить project-centric structure
2. Изучить **[Platform Roadmap](docs/roadmap.md)** для понимания архитектуры
3. Изучить **[First Bird Project](docs/projects/first-bird/README.md)** как пример
4. Импортировать project workflows из `workflows/first-bird/` в n8n
5. ✅ **Подготовиться к Test Webhook integration** в parent workflows
6. ✅ **Use Release System** для professional versioning
7. Следовать **[Security Best Practices](docs/security-best-practices.md)** для credentials
8. Следовать **[Backup Essentials](docs/backup-essentials.md)** перед major changes

### **Для Новых Проектов:**
1. Изучить **[Platform Architecture](workflows/README.md)** и project structure
2. Создать new project папку в `workflows/[project-name]/`
3. Следовать project structure template: `dev/`, `prod/`, `README.md`
4. Создать project documentation в `docs/projects/[project-name]/`
5. ✅ **Plan Test Webhook integration** - simplified testing framework
6. ✅ **Plan release versioning** - use automated release system
7. Deploy в PROD environment следуя установленным procedures

---

## 🧪 Testing Framework Платформы

### ✅ **Test Webhook - Test Execution Подход - АРХИТЕКТУРНО ГОТОВ**

#### **Основная концепция:**
- **Упрощенное тестирование:** Parent workflows тестируются напрямую через dedicated test webhooks
- **Естественное выполнение:** Child workflows выполняются естественно в процессе parent execution
- **Мониторинг результатов:** Отслеживание parent и child workflow results после trigger
- **Исключение сложности:** Отказ от centralized orchestration в пользу direct testing

#### **Архитектурные преимущества:**
```
✅ Упрощение - исключение complex orchestration layer
✅ Естественность - тестирование actual production execution patterns  
✅ Maintenance - reduced infrastructure complexity
✅ Debugging - direct parent workflow issue identification
✅ Scalability - easy addition новых projects без orchestrator modifications
```

#### **Testing Flow:**
```
Test Request → Parent Workflow Test Webhook → Parent выполняется → Child Workflows выполняются естественно → Мониторинг результатов
```

### 📊 **Testing Data Formats:**

**Input Format для Parent Workflow Test Webhook:**
```json
{
  "testType": "full|quick|specific",
  "parentWorkflow": "ai-deepseek", 
  "testData": {
    "input": "test financial query",
    "sessionId": "test-session-123"
  },
  "monitoring": {
    "trackChildExecution": true,
    "validateResults": true,
    "timeout": "60s"
  }
}
```

**Output Format:**
```json
{
  "testExecution": {
    "executionId": "exec-test-12345",
    "status": "success|failure",
    "parentWorkflow": {
      "name": "ai-deepseek",
      "status": "completed",
      "duration": "42.1s"
    },
    "childWorkflows": [
      {
        "name": "fmp-router",
        "status": "completed", 
        "callCount": 1
      }
    ]
  }
}
```

### **Migration от Previous Approach:**
- **⚠️ Legacy Test Orchestrator** будет deprecated после implementation нового подхода
- **✅ Improved Architecture** с focus на simplicity и natural workflow execution
- **✅ Better Debugging** через direct parent workflow testing
- **📚 Documentation Updated** с новой methodology

---

## 🔧 Технологии Платформы

- **n8n** - Core automation platform
- **GitHub** - Version control, project management, и CI/CD
- **GitHub Actions** - Automated pipeline и multi-project quality gates
- **GitHub Issues** - Structured task и change management
- **MCP (Model Context Protocol)** - AI agent platform integration
- ✅ **Test Webhook Framework** - ✅ **АРХИТЕКТУРНО ГОТОВ** Simplified workflow testing approach
- ✅ **Release Management** - ✅ **OPERATIONAL** Automated GitHub Releases & Tags

---

## 🤝 Правила Разработки

### **Для всех Участников Платформы:**
1. **Следовать Platform Protocols** - все установленные процедуры обязательны
2. **Project-Centric Structure** - новые проекты следуют установленной архитектуре
3. **No Changes Without Issues** - structured change management required
4. **Следовать Platform Roadmap** - выравнивание с milestone priorities
5. **Security First** - обязательные security practices (см. [Security Best Practices](docs/security-best-practices.md))
6. **Backup Before Major Changes** - защита данных required (см. [Backup Essentials](docs/backup-essentials.md))
7. ✅ **Simplified Testing** - все изменения должны пройти Test Webhook validation
8. ✅ **Professional Releases** - использовать automated release system для versioning
9. **Documentation Integration** - все project решения должны быть задокументированы

### **Для AI Agents:**
1. **Follow AI Agent Execution Protocol** - обязательно для каждого assignment
2. **Use Appropriate AI Agent Role** - согласно [AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)
3. **Project Context Awareness** - понимать project-specific requirements
4. **Platform Integration** - следовать universal protocols
5. **Issue Management** - создавать и обновлять Issues для всех планируемых изменений
6. **Documentation Updates** - поддерживать project и platform documentation
7. ✅ **Test Webhook Approach** - использовать simplified testing для validation
8. ✅ **Release Management** - следовать professional versioning procedures

---

## 🎯 Будущие Проекты

Платформа спроектирована для scalability и готова поддерживать множественные automation проекты:

- **✅ Project-Centric Architecture** - Repository structure поддерживает unlimited projects
- ✅ **Simplified Testing Framework** - ✅ **АРХИТЕКТУРНО ГОТОВ** Test Webhook approach работает с любыми parent-child workflows
- ✅ **Professional Release Management** - ✅ **OPERATIONAL** automated versioning для всех projects
- **✅ Reusable Protocols** - AI Agent и development procedures применимы ко всем проектам
- **✅ Scalable CI/CD** - GitHub Actions pipeline поддерживает multi-project validation
- **✅ Documentation Templates** - Установленные паттерны для new project documentation

### **Potential Future Projects:**
- **E-commerce Automation** (Shopify/WooCommerce APIs)
- **Social Media Management** (Twitter/LinkedIn automation)
- **IoT Data Processing** (sensor data workflows)
- **Content Management** (CMS/blogging automation)

*Все future projects будут автоматически supported simplified Test Webhook approach и professional release system!*

**⚠️ Note:** Новые проекты рекомендуется создавать после completion архитектурных changes (Issue #26) для validation новой testing methodology.

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
- ✅ **Testing Support**: ✅ [Testing Strategy](docs/testing-strategy.md) с Test Webhook - Test Execution подходом
- ✅ **Release Support**: Professional release management system

---

## 🌐 Языковая Политика Проекта

### **📚 Основной Язык: Русский**
Вся документация, комментарии, описания issues и коммуникация должны быть на русском языке для максимального понимания и доступности среди русскоязычной команды.

### **🔥 Англицизмы Приветствуются**
Мы используем англицизмы согласно следующей политике: активно применяем технические термины, устоявшиеся концепции, устойчивые выражения, а также выражения, которые претендуют стать устойчивыми - но избегаем превращения обычных слов в англицизмы без необходимости.

**В профессиональном контексте поощряется использование:**
- **Technical Terms**: workflows, CI/CD, testing framework, deployment
- **Development Terms**: commit, merge, pull request, issue, repository
- **Platform Terms**: scalability, automation, integration, webhook
- **Business Terms**: roadmap, milestones, deliverables, best practices

---

## 📄 Лицензия

**Friends Only License v1.0** 🤝

Данный проект работает под эксклюзивными условиями лицензии "Только для друзей":

### **Разрешённые Пользователи:**
- **dabalakirev** (создатель проекта) ✅
- **Друзья dabalakirev** (explicitly approved individuals) ✅
- **AI Agents работающие с dabalakirev** (при правильной конфигурации) 🤖

### **🎯 Friend Definition:**
*"Friend" - это человек, которого dabalakirev искренне пригласил бы на кофе, помог бы debug код в 2 утра, или доверил бы пароль от WiFi.* ☕

**Для licensing inquiries или проверки friend status, обращайтесь к dabalakirev напрямую.**

---

## 🏆 **Platform Achievements**

### ✅ **Major Milestones Completed**
- ✅ **v1.2 Simplified Testing Framework** - АРХИТЕКТУРНО ГОТОВ (August 30, 2025)
- ✅ **Test Webhook - Test Execution подход** - Protocol-level implementation complete
- ✅ **Platform-Wide Simplified Testing** - natural parent-child workflow testing
- ✅ **Professional Test Architecture** - elimination of complex orchestration
- ✅ **GitHub Releases & Tags System** - professional versioning & deployment ready
- ✅ **Automated Release Management** - comprehensive GitHub Actions workflow

### 🔄 **Current Focus: Architecture Implementation**
- **🎯 Active Goal:** Complete Test Webhook - Test Execution architecture implementation
- **📋 Issue #26:** [Test Webhook - Test Execution подход в протоколы](https://github.com/dabalakirev/n8n-workflows-ai/issues/26)
- **🧪 Testing Phase:** Архитектурные изменения на protocol level
- **🚀 Target:** Simplified testing approach для First Bird project validation

### 🚀 **Ready for First Official Release**
**v1.2.0 "Simplified Testing Framework"** готов к deployment как first official release платформы, demonstrating:
- Simplified testing capability through Test Webhook approach
- Professional release management system  
- Enterprise-grade development protocols
- AI-powered automation development standards
- Scalable multi-project platform architecture

---

**Эта платформа демонстрирует современную AI-powered automation разработку с project-centric architecture, structured protocols, comprehensive documentation, ✅ SIMPLIFIED testing framework через Test Webhook - Test Execution подход, ✅ PROFESSIONAL release management system и scalable multi-project support.**

*Updated: August 30, 2025 - Архитектурное обновление testing framework | Test Webhook - Test Execution подход готов на protocol level | Platform готов для v1.2.0 Simplified Testing Framework Release*