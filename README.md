# n8n-workflows-ai

![GitHub Issues](https://img.shields.io/github/issues/dabalakirev/n8n-workflows-ai)
![Platform Status](https://img.shields.io/badge/platform-v1.1--foundation-orange)
![License](https://img.shields.io/badge/license-Friends%20Only-purple)

**AI-Powered Automation Platform** для разработки n8n workflows с test-driven development и современными DevOps практиками

## 📋 Содержание
- [🎯 Обзор Платформы](#-обзор-платформы)
- [🐦 Текущий Проект: "First Bird"](#-текущий-проект-first-bird)
- [🛠️ Платформенные Инструменты](#️-платформенные-инструменты)
- [🗺️ Platform Roadmap](#️-platform-roadmap)
- [🏗️ Архитектура и Environment Structure](#️-архитектура-и-environment-structure)
- [🚀 Getting Started](#-getting-started)
- [🧪 Platform Testing Framework](#-platform-testing-framework)
- [🔧 Platform Technologies](#-platform-technologies)
- [🤝 Platform Development Rules](#-platform-development-rules)
- [🎯 Future Projects](#-future-projects)
- [📞 Platform Support](#-platform-support)
- [🌐 Языковая Политика Проекта](#-языковая-политика-проекта)
- [📄 Лицензия](#-лицензия)

## 🎯 Обзор Платформы

**n8n-workflows-ai** - это универсальная платформа для создания, тестирования и управления n8n automation проектами с использованием AI agents и structured development protocols.

### 🏗️ **Platform Architecture**

```
n8n-workflows-ai Platform
├── 🤖 AI Agent Protocols          # Structured development с AI
├── 🧪 Testing Framework           # Universal Test Orchestrator
├── 🚀 CI/CD Pipeline             # GitHub Actions automation
├── 📚 Documentation System       # Comprehensive guides & protocols
└── 📁 Projects                   # Individual automation projects
    └── 🐦 First Bird (current)   # Financial data automation
```

### ⚡ **Platform Capabilities**

- **AI-Assisted Development** с structured roles и protocols
- **Universal Testing Framework** через Test Orchestrator
- **Multi-Project Support** с DEV/PROD environment separation
- **Automated CI/CD** через GitHub Actions
- **Comprehensive Documentation** с protocols и best practices
- **Scalable Architecture** готовая для новых automation projects

---

## 🐦 Текущий Проект: "First Bird"

**Financial Data Automation** - пилотный проект демонстрирующий platform capabilities

### **Project Scope:**
- **Data Source:** Financial Modeling Prep API
- **AI Analysis:** Market insights и financial data processing
- **Automation Goals:** Streamlined financial data workflows

### **Project Workflows:**
- **🤖 AI Deepseek** - Financial data analysis с AI language model
- **🔗 FMP API Router** - Financial Modeling Prep API routing и data transformation

### **Project Status:**
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
- **Scope:** Platform-level tool, не project-specific
- **Capabilities:** Execute workflow testing, result aggregation, comprehensive reporting
- **Usage:** Работает со всеми projects созданными на platform

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

## 🗺️ Platform Roadmap

### 📅 **Current Status: Milestone v1.1 - Documentation & Infrastructure**
```
v1.1 Documentation & Infrastructure:  ██████████ 90% (platform foundation)
v1.2 Testing Framework:               ████░░░░░░ 40% (Test Orchestrator готов)
v1.3 Advanced Features:               ░░░░░░░░░░  0% (multi-project scaling)

Overall Platform Progress:            ███████░░░ 75%
```

### 🎯 **Platform Milestones:**
- **🏗️ v1.1 - Platform Foundation** (Сентябрь 2025) - *Documentation & Infrastructure*
  - Complete AI Agent protocols и development procedures
  - Optimize GitHub environment для productivity
  - Establish release и version management systems
  
- **🧪 v1.2 - Testing Framework** (Октябрь-Ноябрь 2025) - *Universal Testing Infrastructure*
  - Activate Test Orchestrator для automated testing
  - Integrate testing с CI/CD pipeline
  - Establish quality gates для deployment
  
- **🚀 v1.3 - Multi-Project Platform** (Декабрь 2025) - *Scaling & Advanced Features*
  - Multi-project support и management
  - Performance optimization suite
  - Enterprise integrations и features

📖 **[Detailed Platform Roadmap →](docs/roadmap.md)**

---

## 🏗️ Архитектура и Environment Structure

### **Multi-Environment Support:**
- **DEV Environment** - Development и testing (2 triggers: Manual + Execute Workflow)
- **PROD Environment** - Production deployments (1 trigger: Manual только)
- **Test Framework** - Automated quality assurance через Test Orchestrator

### **Repository Structure:**
```
├── workflows/           # Project workflow implementations
│   ├── dev/            # DEV versions с testing triggers
│   └── prod/           # PROD versions (production-ready)
├── docs/               # Platform documentation и protocols
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

## 🚀 Getting Started

### **Для AI Agents:**
1. **Read AI Agent Execution Protocol** - mandatory workflow для всех assignments
2. **Study AI Agent Roles & Protocols** - понимание SDLC roles и processes
3. **Review all platform protocols** в `docs/` directory
4. **Check Platform Roadmap** для current priorities и milestone status
5. **Verify platform status** через `n8n_health_check`
6. **Follow 5-step execution flow** для каждого assignment
7. **ВАЖНО:** Review backup и security requirements перед major changes

### **Для Developers:**
1. Clone repository и explore platform structure
2. Study **[Platform Roadmap](docs/roadmap.md)** для architecture understanding
3. Import project workflows в n8n DEV/PROD environments
4. Configure development environment следуя platform protocols
5. Follow **[Security Best Practices](docs/security-best-practices.md)** для credentials
6. Follow **[Backup Essentials](docs/backup-essentials.md)** перед major changes

### **Для New Projects:**
1. Study platform architecture и existing project structure
2. Create project-specific workflows в DEV environment
3. Follow platform testing procedures с Test Orchestrator
4. Use platform documentation templates и protocols
5. Deploy в PROD environment следуя established procedures

---

## 🧪 Platform Testing Framework

### ✅ **Universal Test Orchestrator:**
- **Capability:** Tests ЛЮБЫЕ n8n workflows созданные на platform
- **Architecture:** Platform-level tool обслуживающий все projects
- **Integration:** Работает с DEV environments (dual triggers: Manual + Execute Workflow)
- **Automation:** Integrated с GitHub Actions для automated testing
- **Scalability:** Готов тестировать multiple projects по мере роста platform

### 📊 **Testing Methodology:**
- **DEV Workflows:** Dual triggers позволяют manual и automated testing
- **PROD Workflows:** Single manual trigger для production stability
- **Quality Gates:** Automated testing блокирует defective deployments
- **Test Coverage:** Target 100% automation критических workflow paths

---

## 🔧 Platform Technologies

- **n8n** - Core automation platform
- **GitHub** - Version control, project management, и CI/CD
- **GitHub Actions** - Automated pipeline и quality gates
- **GitHub Issues** - Structured task и change management
- **MCP (Model Context Protocol)** - AI agent platform integration
- **Test Orchestrator** - Universal workflow testing framework

---

## 📊 Platform Metrics

- **Current Projects**: 1 (First Bird - financial automation)
- **Platform Tools**: Test Orchestrator, GitHub Actions, Documentation System
- **Active Issues**: 11 platform и project issues (смотри на [GitHub Issues](../../issues))
- **Automation Coverage**: Target 100% DEV workflows (в development)
- **Architecture**: Multi-environment с controlled DEV → PROD migration
- **Documentation**: Comprehensive coverage всех platform processes

---

## 🤝 Platform Development Rules

### **Для всех Platform Contributors:**
1. **Follow Platform Protocols** - все established procedures обязательны
2. **No Changes Without Issues** - structured change management required
3. **Follow Platform Roadmap** - align с milestone priorities
4. **Security First** - mandatory security practices (см. [Security Best Practices](docs/security-best-practices.md))
5. **Backup Before Major Changes** - data protection required (см. [Backup Essentials](docs/backup-essentials.md))
6. **Universal Testing** - все changes должны pass Test Orchestrator validation
7. **Documentation Integration** - все architectural decisions должны быть documented
8. **Protocol Compliance** - established workflows должны быть followed

### **Для AI Agents:**
1. **Follow AI Agent Execution Protocol** - mandatory для каждого assignment
2. **Use Appropriate AI Agent Role** - согласно [AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)
3. **Context Integration** - читать platform documentation перед началом work
4. **Roadmap Awareness** - check current priorities и milestones
5. **Issue Management** - создавать и update Issues для всех planned changes
6. **Documentation Updates** - maintain platform documentation с changes
7. **Security and Backup Compliance** - verify requirements согласно protocols

---

## 🎯 Future Projects

Platform спроектирована для scalability и готова support additional automation projects:

- **Multi-Project Architecture** - Repository structure supports project separation
- **Universal Testing Framework** - Test Orchestrator работает с любыми n8n workflows
- **Reusable Protocols** - AI Agent и development procedures применимы ко всем projects
- **Scalable CI/CD** - GitHub Actions pipeline адаптируется к multiple projects
- **Documentation Templates** - Established patterns для new project documentation

---

## 📞 Platform Support

- **Issues**: Use GitHub Issues с standardized templates
- **Documentation**: Comprehensive guides в `docs/` directory
- **Roadmap**: Current development status в [docs/roadmap.md](docs/roadmap.md)
- **AI Agent Support**: Follow AI Agent Execution Protocol и Context Handoff Protocol
- **Security Support**: Security guidelines в [docs/security-best-practices.md](docs/security-best-practices.md)
- **Backup Support**: Recovery procedures в [docs/backup-essentials.md](docs/backup-essentials.md)

---

## 🌐 Языковая Политика Проекта

### **🇷🇺 Основной Язык: Русский**
Все documentation, comments, issue descriptions и communication должны быть на русском языке для максимального понимания и accessibility среди русскоязычной команды.

### **🔥 Англицизмы Горячо Приветствуются!**
В профессиональном контексте активно поощряется использование:
- **Technical Terms**: workflows, CI/CD, testing framework, deployment
- **Development Terms**: commit, merge, pull request, issue, repository
- **Platform Terms**: scalability, automation, integration, orchestrator
- **Business Terms**: roadmap, milestones, deliverables, stakeholder

### **🎯 **Translation Policy****
Специфические термины и concepts могут переводиться на английский для международной совместимости:
- **Friend Definition** вместо "Определение Друга"
- **Platform Architecture** alongside "Архитектура Платформы" 
- **Quality Gates** вместо "Шлюзы Качества"

### **✅ Best Practices:**
- Основной текст на русском с professional англицизмами
- Technical термины остаются на английском
- Code comments предпочтительно на английском
- Issue titles могут содержать английские technical terms

---

## 📄 Лицензия

**Friends Only License v1.0** 🤝

Данный проект работает под эксклюзивными условиями лицензии "Только для друзей":

### **Разрешённые Пользователи:**
- **dabalakirev** (создатель проекта) ✅
- **Друзья dabalakirev** (explicitly approved individuals) ✅
- **AI Agents работающие с dabalakirev** (при правильной конфигурации) 🤖

### **Usage Rights:**
- **Full access:** Создавать, изменять, использовать и deploy что угодно
- **Learning purposes:** Изучать code, documentation и architecture
- **Private use:** Запускать workflows для personal/friend projects
- **Collaboration:** Работать вместе с dabalakirev над improvements

### **Ограничения:**
- ❌ **Commercial use** не-друзьями строго prohibited
- ❌ **Public redistribution** без explicit permission
- ❌ **Corporate usage** неизвестными entities forbidden
- ❌ **Reverse engineering** для competitive purposes banned

### **🎯 **Friend Definition**:**
*"Friend" - это человек, которого dabalakirev искренне пригласил бы на coffee, помог бы debug code в 2 AM, или доверил бы WiFi password.* ☕

### **Consequences при Violation:**
Unauthorized usage приведёт к disappointed looks, sad emojis и potential exclusion из future coffee invitations. 😔

**Для licensing inquiries или friend status verification, contact dabalakirev directly.**

---

**Эта платформа демонстрирует современную AI-powered automation разработку со structured protocols, comprehensive security practices, universal testing framework, reliable backup procedures и scalable multi-project architecture.**