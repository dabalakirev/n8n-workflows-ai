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
    └── 🐦 First Bird (current)   # Financial data automation [TEST WEBHOOK INTEGRATION]
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
- **🔖 Ready for Release:** v1.2.1 "MCP Webhook Testing Documentation"
- **🚀 Release System:** ✅ Automated GitHub Actions workflow 
- **📦 Artifacts:** Automated workflow + documentation packaging
- **🏷️ Git Tags:** Professional semantic versioning

#### **🎯 Versioning Strategy:**
```
v1.2.1 - "MCP Webhook Testing Documentation" (READY - Enhanced Testing Support)
v1.3.0 - "First Bird Complete" (Final project validation & production deployment)  
v1.4.0 - "Multi-Project Platform" (Advanced features & scaling)
v2.0.0 - "Enterprise Platform" (Breaking changes & major evolution)
```

#### **🚀 How to Create Release:**
```bash
# Using GitHub Actions (Manual Trigger)
# Navigate to: Actions → 🏷️ Create Release → Run workflow
# Input: version (v1.2.1), type (stable), name (MCP Webhook Testing Documentation)

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
- **⚙️ [Workflow README](workflows/first-bird/README.md)** - Technical workflow details с test webhook configuration

### **🔄 Current Status: Test Webhook Integration Complete**
```
📊 First Bird Progress:        ██████████ 100% (workflows созданы и configured)
🧪 Testing Integration:        ██████████ 100% ✅ (Test Webhook - Test Execution approach documented)
🚀 Production Readiness:       ████████░░  80% (pending technical implementation - Issue #27)
```

- **✅ ТЕКУЩАЯ ФАЗА:** Test Webhook - Test Execution documentation complete (Issue #28)
- **🧪 Active Issue:** [#27 - First Bird Project Completion](https://github.com/dabalakirev/n8n-workflows-ai/issues/27)
- **🎯 Цель:** Technical implementation webhook testing для production validation

---

## 🛠️ Платформенные Инструменты

### 🧪 **Testing Framework - Test Webhook - Test Execution** *(✅ DOCUMENTATION COMPLETE)*
- **Подход:** ✅ **Simplified Direct Testing** - parent workflows тестируются через dedicated test webhooks
- **Архитектура:** Parent workflow → естественное выполнение → Child workflows → мониторинг результатов
- **Преимущества:** Упрощенная архитектура, естественное выполнение, лучший debugging
- **Status:** ✅ **Documentation Complete** - comprehensive MCP webhook testing guide available

### 🏷️ **Release Management System** *(✅ OPERATIONAL - Professional Versioning)*
- **Status:** ✅ **FULLY OPERATIONAL** - Ready for release v1.2.1
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
- **✅ MCP Webhook Testing Guide** - Comprehensive step-by-step testing procedures
- **MCP CI/CD Deployment Protocol** - Comprehensive development lifecycle procedures
- **Development Guides** - Best practices и procedures
- **Security Standards** - Credential management и data protection

---

## 🏗️ Project-Centric Архитектура

### **Project Structure:**
```
workflows/
├── first-bird/             # Financial Data Automation project [TEST WEBHOOK INTEGRATION COMPLETE]
│   ├── dev/                # DEV workflows - ready для test webhook testing
│   │   ├── ai-deepseek-dev.json      (Manual + Test Webhook)
│   │   └── fmp-router-dev.json       (Manual + Execute Workflow)
│   ├── prod/               # PROD workflows (1 trigger each)
│   │   ├── ai-deepseek-prod.json     (Manual only) [FUTURE]
│   │   └── fmp-router-prod.json      (Manual only) [FUTURE]
│   └── README.md           # Project-specific workflow documentation с test webhook examples
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
│   ├── testing-strategy.md          # ✅ Updated с MCP webhook testing
│   ├── ai-agent-roles-protocols.md  # ✅ Updated с webhook testing integration
│   └── mcp-webhook-testing-guide.md # ✅ NEW - Comprehensive MCP testing guide
└── projects/               # Project-specific documentation  
    └── first-bird/         # First Bird project docs
        ├── README.md       # Project overview
        ├── api-reference.md # FMP API documentation
        └── workflow-guide.md # Usage guide
```

### **Multi-Environment Support:**
- **DEV Environment** - Development и testing (2 triggers: Manual + Test Webhook для parent)
- **PROD Environment** - Production deployments (1 trigger: Manual только)
- ✅ **Test Framework** - ✅ **DOCUMENTATION COMPLETE** simplified testing architecture
- ✅ **Release Management** - ✅ **OPERATIONAL** professional versioning и deployment

### **Platform Navigation:**
- **📋 [Workflows Overview](workflows/README.md)** - Platform workflow architecture
- **🐦 [First Bird Project](workflows/first-bird/README.md)** - Project workflow details с test webhook configuration  
- **📚 [Platform Protocols](docs/)** - Development guidelines и procedures
- **✅ [Testing Strategy](docs/testing-strategy.md)** - MCP Webhook Testing integration
- **✅ [MCP Webhook Testing Guide](docs/mcp-webhook-testing-guide.md)** - Comprehensive testing procedures
- **🗺️ [Platform Roadmap](docs/roadmap.md)** - Development timeline и milestones

---

## 🚀 Начало Работы

### **Для AI Agents:**
1. **Read AI Agent Execution Protocol** - обязательный workflow для всех assignments
2. **Study AI Agent Roles & Protocols** - понимание SDLC roles и processes с webhook testing approach
3. **Изучить все platform protocols** в `docs/` directory
4. **✅ Study MCP Webhook Testing Guide** - comprehensive testing procedures
5. **Проверить Platform Roadmap** для текущих приоритетов и milestone status
6. **Verify platform status** через `n8n_health_check`
7. ✅ **Use Test Webhook Approach** - MCP webhook testing для всех workflow validation
8. ✅ **Follow Release Procedures** - use professional release management
9. **Follow 5-step execution flow** для каждого assignment
10. **ВАЖНО:** Изучить backup и security requirements перед major changes

### **Для Developers:**
1. Clone repository и изучить project-centric structure
2. Изучить **[Platform Roadmap](docs/roadmap.md)** для понимания архитектуры
3. Изучить **[First Bird Project](docs/projects/first-bird/README.md)** как пример
4. Импортировать project workflows из `workflows/first-bird/` в n8n
5. ✅ **Study MCP Webhook Testing** - learn testing procedures through [MCP Guide](docs/mcp-webhook-testing-guide.md)
6. ✅ **Use Release System** для professional versioning
7. Следовать **[Security Best Practices](docs/security-best-practices.md)** для credentials
8. Следовать **[Backup Essentials](docs/backup-essentials.md)** перед major changes

### **Для Новых Проектов:**
1. Изучить **[Platform Architecture](workflows/README.md)** и project structure
2. Создать new project папку в `workflows/[project-name]/`
3. Следовать project structure template: `dev/`, `prod/`, `README.md`
4. Создать project documentation в `docs/projects/[project-name]/`
5. ✅ **Plan Test Webhook integration** - use [MCP Testing Guide](docs/mcp-webhook-testing-guide.md)
6. ✅ **Plan release versioning** - use automated release system
7. Deploy в PROD environment следуя установленным procedures

---

## 🧪 Testing Framework Платформы

### ✅ **Test Webhook - Test Execution Подход - DOCUMENTATION COMPLETE**

#### **Основная концепция:**
- **Упрощенное тестирование:** Parent workflows тестируются напрямую через dedicated test webhooks
- **Естественное выполнение:** Child workflows выполняются естественно в процессе parent execution
- **Мониторинг результатов:** Отслеживание parent и child workflow results после trigger
- **MCP Integration:** Direct testing через n8n MCP tools без external dependencies

#### **Архитектурные преимущества:**
```
✅ Упрощение - исключение complex orchestration layer
✅ Естественность - тестирование actual production execution patterns  
✅ Maintenance - reduced infrastructure complexity
✅ Debugging - direct parent workflow issue identification
✅ Scalability - easy addition новых projects без orchestrator modifications
✅ MCP Native - testing через Model Context Protocol tools
```

#### **Testing Flow:**
```
MCP Webhook Discovery → Test Data Preparation → Parent Webhook Execution → Child Workflows Natural Execution → Result Monitoring → Validation
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

### **✅ Complete Testing Documentation:**
- **✅ [Testing Strategy](docs/testing-strategy.md#-mcp-webhook-testing)** - Platform testing overview с MCP integration
- **✅ [MCP Webhook Testing Guide](docs/mcp-webhook-testing-guide.md)** - Comprehensive 26KB+ step-by-step guide
- **✅ [AI Agent Webhook Protocols](docs/ai-agent-roles-protocols.md#-webhook-testing-protocol-для-ai-agents)** - Role-specific testing procedures
- **✅ [First Bird Test Configuration](workflows/first-bird/README.md#-test-webhook-configuration)** - Working project examples

---

## 🔧 Технологии Платформы

- **n8n** - Core automation platform
- **GitHub** - Version control, project management, и CI/CD
- **GitHub Actions** - Automated pipeline и multi-project quality gates
- **GitHub Issues** - Structured task и change management
- **MCP (Model Context Protocol)** - AI agent platform integration
- ✅ **Test Webhook Framework** - ✅ **DOCUMENTATION COMPLETE** MCP-native workflow testing
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
7. ✅ **MCP Webhook Testing** - все изменения должны пройти Test Webhook validation через MCP tools
8. ✅ **Professional Releases** - использовать automated release system для versioning
9. **Documentation Integration** - все project решения должны быть задокументированы

### **Для AI Agents:**
1. **Follow AI Agent Execution Protocol** - обязательно для каждого assignment
2. **Use Appropriate AI Agent Role** - согласно [AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)
3. **Project Context Awareness** - понимать project-specific requirements
4. **Platform Integration** - следовать universal protocols
5. **Issue Management** - создавать и обновлять Issues для всех планируемых изменений
6. **Documentation Updates** - поддерживать project и platform documentation
7. ✅ **MCP Webhook Testing** - использовать n8n MCP tools для webhook validation
8. ✅ **Release Management** - следовать professional versioning procedures

---

## 🎯 Будущие Проекты

Платформа спроектирована для scalability и готова поддерживать множественные automation проекты:

- **✅ Project-Centric Architecture** - Repository structure поддерживает unlimited projects
- ✅ **MCP Webhook Testing Framework** - ✅ **DOCUMENTATION COMPLETE** работает с любыми parent-child workflows
- ✅ **Professional Release Management** - ✅ **OPERATIONAL** automated versioning для всех projects
- **✅ Reusable Protocols** - AI Agent и development procedures применимы ко всем проектам
- **✅ Scalable CI/CD** - GitHub Actions pipeline поддерживает multi-project validation
- **✅ Documentation Templates** - Comprehensive patterns для new project documentation

### **Potential Future Projects:**
- **E-commerce Automation** (Shopify/WooCommerce APIs)
- **Social Media Management** (Twitter/LinkedIn automation)
- **IoT Data Processing** (sensor data workflows)
- **Content Management** (CMS/blogging automation)

*Все future projects будут автоматически supported MCP webhook testing approach и professional release system!*

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
- ✅ **Testing Support**: ✅ [Testing Strategy](docs/testing-strategy.md) с MCP webhook testing
- ✅ **MCP Testing Guide**: ✅ [Comprehensive Testing Procedures](docs/mcp-webhook-testing-guide.md)
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
- ✅ **v1.2.1 MCP Webhook Testing Documentation** - COMPLETE (August 30, 2025)
- ✅ **Test Webhook - Test Execution подход** - Complete documentation coverage
- ✅ **MCP Testing Integration** - Comprehensive guide и AI agent protocols
- ✅ **Professional Test Architecture** - MCP-native testing approach
- ✅ **GitHub Releases & Tags System** - professional versioning & deployment ready
- ✅ **Automated Release Management** - comprehensive GitHub Actions workflow

### 🔄 **Current Focus: Technical Implementation**
- **🎯 Active Goal:** Complete First Bird project через Test Webhook technical implementation
- **📋 Issue #27:** [First Bird Project Completion](https://github.com/dabalakirev/n8n-workflows-ai/issues/27)
- **🧪 Implementation Phase:** Technical webhook testing integration в n8n workflows
- **🚀 Target:** Production-ready First Bird project с validated testing approach

### 🚀 **Ready for Enhanced Release**
**v1.2.1 "MCP Webhook Testing Documentation"** готов к deployment, demonstrating:
- Comprehensive MCP webhook testing documentation
- Complete AI agent testing protocols
- Working configuration templates  
- Professional testing procedures
- Platform-wide testing integration

---

**Эта платформа демонстрирует современную AI-powered automation разработку с project-centric architecture, structured protocols, ✅ COMPREHENSIVE testing documentation через MCP Webhook - Test Execution подход, ✅ PROFESSIONAL release management system и scalable multi-project support.**

*Updated: August 30, 2025 - MCP Webhook Testing Documentation Complete | Comprehensive testing guide available | First Bird project ready для technical implementation*