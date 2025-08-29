# 📝 n8n Workflows - Project-Centric Architecture

**Platform**: n8n-workflows-ai универсальная автоматизация с AI  
**Архитектура**: Project → Environment (DEV/PROD) → Workflows

## 🏗️ **Project-Centric Structure**

```
workflows/
├── first-bird/             # Financial Data Automation project
│   ├── dev/                # DEV workflows (2 triggers each)
│   │   ├── ai-deepseek-dev.json      (Manual + Execute Workflow)
│   │   └── fmp-router-dev.json       (Manual + Execute Workflow) 
│   ├── prod/               # PROD workflows (1 trigger each)
│   │   ├── ai-deepseek-prod.json     (Manual only)
│   │   └── fmp-router-prod.json      (Manual only)
│   └── README.md           # Project-specific documentation
├── [future-project]/       # Template для новых проектов
│   ├── dev/                # DEV environment для проекта
│   ├── prod/               # PROD environment для проекта  
│   └── README.md           # Project documentation
└── README.md              # Этот файл - platform workflows guide
```

## 🎯 **Platform Architecture Benefits**

### **Scalability**
- **Multiple Projects** поддерживаются одной платформой
- **Consistent Structure** для всех automation проектов  
- **Reusable Testing** через universal Test Orchestrator
- **Shared Infrastructure** GitHub Actions, protocols, tools

### **Project Isolation**
- **Clear Separation** каждый проект в своей папке
- **Independent Development** different domains/APIs/workflows
- **Project-Specific Documentation** tailored guides и references
- **Environment Management** DEV/PROD по проекту

### **Universal Tools Integration**
- **Test Orchestrator** работает с любыми project workflows
- **GitHub Actions** automatically validates все project structures  
- **Platform Documentation** protocols применимы ко всем проектам
- **AI Agent Protocols** universal processes для любых projects

## 🚀 **Current Projects**

### 🐦 **First Bird (Active)**
**Domain:** Financial Data Automation  
**API:** Financial Modeling Prep  
**Workflows:** AI Deepseek + FMP API Router  
**Status:** Production-ready, platform-compliant

**Документация:** `workflows/first-bird/README.md`

### 🔮 **Future Projects**
Платформа готова поддерживать дополнительные проекты:
- **E-commerce Automation** (Shopify/WooCommerce APIs)  
- **Social Media Management** (Twitter/LinkedIn APIs)
- **IoT Data Processing** (sensor data automation)
- **Content Management** (CMS/blogging workflows)

## 🧪 **Universal Testing Framework**

### **Test Orchestrator Integration**
- **Любой проект** может тестироваться через platform Test Orchestrator
- **DEV Workflows** имеют Execute Workflow Triggers для automation
- **PROD Workflows** содержат только Manual Triggers для stability
- **Automated Quality Gates** через GitHub Actions pipeline

### **Multi-Project Testing**  
- **Project-Agnostic** testing procedures
- **Scalable Test Coverage** для растущего количества проектов
- **Universal Test Reports** aggregated insights across projects
- **Consistent Quality Standards** применяются ко всем projects

## 🔐 **Security & Standards**

### **Platform-Wide Security**
- **No Hardcoded Secrets** в любых project workflows
- **Credential References** через n8n credentials management
- **Security Scanning** автоматизированное через GitHub Actions
- **Consistent Security Practices** across all projects

### **Quality Standards**
- **JSON Syntax Validation** для всех workflow files
- **Trigger Count Verification** (DEV=2, PROD=1) для каждого проекта
- **Structure Compliance** автоматические checks
- **Documentation Standards** consistent project documentation

## 📊 **Platform Management**

### **GitHub Actions Pipeline**
```yaml
Automated Validation:
├── JSON structure validation     # Все project workflows
├── Security scanning            # Platform-wide security  
├── Trigger compliance          # DEV/PROD standards
└── Multi-project verification  # Architecture consistency
```

### **Development Workflow**
1. **Создать project папку** в `workflows/[project-name]/`
2. **Следовать DEV/PROD structure** для environment consistency
3. **Создать project README** с specific documentation
4. **Configure Testing** через Test Orchestrator integration
5. **Production Deployment** следуя platform protocols

## 🎯 **New Project Template**

### **Minimum Project Structure:**
```
workflows/your-project/
├── dev/                    # DEV workflows
│   └── [workflow-name]-dev.json
├── prod/                   # PROD workflows  
│   └── [workflow-name]-prod.json
└── README.md              # Project documentation
```

### **Required Documentation:**
- **Project Overview** - domain, purpose, scope  
- **Workflow Descriptions** - each workflow's functionality
- **Configuration Requirements** - credentials, settings
- **Testing Strategy** - DEV testing procedures
- **Integration Points** - platform tool usage

## 🔗 **Platform Integration**

### **Universal Tools**
- **Test Orchestrator:** `platform-level testing для всех projects`
- **GitHub Actions:** `automated validation каждого project`  
- **Documentation System:** `consistent standards across projects`
- **AI Agent Protocols:** `structured development для всех projects`

### **Cross-Project Benefits**
- **Knowledge Sharing** между проектами через shared documentation
- **Pattern Reuse** successful architecture patterns available globally
- **Resource Optimization** shared testing infrastructure и CI/CD
- **Community Growth** project templates для faster onboarding

---

**Эта архитектура поддерживает unlimited проекты на единой платформе с shared infrastructure, universal testing, и consistent quality standards.**

*Updated: August 2025 - Issue #21 Project-Centric Architecture Implementation*