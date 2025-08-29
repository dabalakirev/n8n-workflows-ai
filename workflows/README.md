# 📝 n8n Workflows - Project-Centric Architecture

**Project-Centric Workflow Management** для n8n-workflows-ai platform  
**Structure**: Project → Environment (DEV/PROD) → Workflows

## 🏗️ **Workflow Directory Structure**

```
workflows/
├── first-bird/             # Financial Data Automation project
│   ├── dev/                # DEV workflows (2 triggers each)
│   │   ├── ai-deepseek-dev.json      (Manual + Execute Workflow)
│   │   └── fmp-router-dev.json       (Manual + Execute Workflow) 
│   ├── prod/               # PROD workflows (1 trigger each)
│   │   ├── ai-deepseek-prod.json     (Manual only) [FUTURE]
│   │   └── fmp-router-prod.json      (Manual only) [FUTURE]
│   └── README.md           # Project-specific workflow documentation
├── [future-project]/       # Template для новых проектов
│   ├── dev/                # DEV environment для проекта
│   ├── prod/               # PROD environment для проекта  
│   └── README.md           # Project workflow documentation
└── README.md              # Этот файл - workflow architecture guide
```

## 🎯 **Project-Centric Workflow Benefits**

### **Project Isolation**
- **Clear Separation** - каждый проект в своей папке с dedicated workflows
- **Independent Development** - different domains, APIs, и business logic
- **Project-Specific Documentation** - tailored guides и technical references
- **Environment Management** - DEV/PROD separation per project

### **Environment Management**
- **DEV Environment** - Development и testing workflows
  - **Dual Triggers**: Manual (testing) + Execute Workflow (automation)
  - **Test Integration**: Compatible с Universal Test Orchestrator
  - **Rapid Iteration**: Fast development и debugging cycle
  
- **PROD Environment** - Production deployment workflows  
  - **Single Trigger**: Manual only для production stability
  - **Production Ready**: Optimized for reliability и performance
  - **Controlled Access**: Limited triggers для production safety

### **Universal Tools Integration**
- **Test Orchestrator Compatibility** - all DEV workflows testable
- **GitHub Actions Validation** - automatic structure compliance checking  
- **Release Management Integration** - workflows packaged for versioning
- **Documentation Standards** - consistent project documentation patterns

## 🚀 **Current Workflow Projects**

### 🐦 **First Bird (Active Development)**
**Domain:** Financial Data Automation  
**API Integration:** Financial Modeling Prep API  
**AI Processing:** DeepSeek language model for market analysis  
**Status:** DEV workflows operational, PROD deployment pending  

**Workflow Components:**
- **AI Deepseek** - Financial query analysis с AI language model
- **FMP API Router** - Universal API endpoint routing для financial data
- **Test Integration** - Full Test Orchestrator compatibility

**Technical Documentation:** [workflows/first-bird/README.md](first-bird/README.md)

### 🔮 **Future Project Templates**
Ready-to-use structure для new automation projects:
- **E-commerce Automation** (Shopify/WooCommerce APIs)  
- **Social Media Management** (Twitter/LinkedIn APIs)
- **IoT Data Processing** (sensor data workflows)
- **Content Management** (CMS/blogging automation)

## 🧪 **Universal Testing Integration**

### **Test Orchestrator Workflow Compatibility**
- **DEV Workflows**: Designed for automated testing через Execute Workflow triggers
- **Testing Framework**: Universal Test Orchestrator (ID: `ElnSprIVyJXKlkl3`) tests any project
- **Multi-Project Support**: Single testing tool serves all workflow projects
- **Automated Quality Gates**: CI/CD integration ready через testing framework

### **Testing Workflow Standards**
All project workflows follow these testing standards:
- **DEV Dual Triggers**: Manual (development) + Execute Workflow (automation)
- **PROD Single Trigger**: Manual only для production stability  
- **Test Data Compatibility**: Structured input/output для automated validation
- **Error Handling**: Consistent error reporting across all workflows

## 🔐 **Workflow Security & Standards**

### **Security Standards**
- **No Hardcoded Secrets** - all credentials через n8n credential management
- **Environment Separation** - DEV/PROD credential isolation
- **Access Control** - trigger-based workflow access management
- **Security Scanning** - automated validation через GitHub Actions

### **Quality Standards**
- **JSON Syntax Validation** - automated structure checking
- **Trigger Count Compliance** - DEV=2 triggers, PROD=1 trigger enforcement
- **Schema Validation** - n8n workflow schema compliance
- **Documentation Requirements** - mandatory project README files

## 📊 **Workflow Management**

### **Development Workflow**
1. **Create Project Folder** в `workflows/[project-name]/`
2. **Follow Environment Structure** - создать `dev/` и `prod/` папки
3. **Implement DEV Workflows** с dual triggers (Manual + Execute Workflow)
4. **Create Project Documentation** в project README.md
5. **Test Integration** через Universal Test Orchestrator
6. **PROD Deployment** после successful DEV validation

### **Automated Validation Pipeline**
```yaml
GitHub Actions Validation:
├── JSON Structure Check       # All workflow files syntax validation
├── Trigger Compliance        # DEV=2, PROD=1 trigger verification  
├── Security Scanning         # Credential и secret validation
├── Schema Validation         # n8n workflow schema compliance
└── Documentation Check       # Required README files verification
```

## 🎯 **New Project Workflow Template**

### **Minimum Project Requirements:**
```
workflows/your-project/
├── dev/                    # DEV environment workflows
│   └── [workflow-name]-dev.json    # Dual triggers: Manual + Execute Workflow
├── prod/                   # PROD environment workflows (future)
│   └── [workflow-name]-prod.json   # Single trigger: Manual only  
└── README.md              # Project workflow documentation
```

### **Required Project Documentation:**
- **Project Overview** - domain, purpose, workflow scope  
- **Workflow Descriptions** - detailed functionality для each workflow
- **Configuration Guide** - required credentials, settings, dependencies
- **Testing Procedures** - DEV testing scenarios и validation steps
- **Integration Details** - Test Orchestrator compatibility и usage

### **Development Standards:**
- **Naming Convention**: `[workflow-name]-[environment].json`
- **Trigger Standards**: DEV workflows=2 triggers, PROD workflows=1 trigger
- **Test Compatibility**: All DEV workflows must support Execute Workflow triggers
- **Documentation**: Project README must document all workflows и their usage

## 🔗 **Platform Integration Points**

### **Universal Platform Tools**
- **Test Orchestrator** (ID: `ElnSprIVyJXKlkl3`) - platform-level testing для all projects
- **GitHub Actions Pipeline** - automated validation для all project structures  
- **Release Management** - automated workflow packaging и versioning
- **Documentation System** - consistent project documentation standards

### **Cross-Project Workflow Benefits**
- **Pattern Reuse** - successful workflow patterns available для new projects
- **Testing Infrastructure** - shared Test Orchestrator serves all projects
- **Quality Standards** - universal validation rules applied to all workflows
- **Knowledge Sharing** - project documentation patterns и best practices

### **Workflow Scalability**
- **Unlimited Projects** - directory structure supports any number of projects
- **Independent Scaling** - each project scales independently
- **Universal Testing** - single Test Orchestrator handles all project workflows
- **Consistent Standards** - same quality и security standards across all projects

---

## 📚 **Related Documentation**

- **Platform Overview**: [../README.md](../README.md) - General platform capabilities и features
- **Platform Roadmap**: [../docs/roadmap.md](../docs/roadmap.md) - Development milestones и progress
- **Testing Strategy**: [../docs/testing-strategy.md](../docs/testing-strategy.md) - Universal testing protocols
- **AI Agent Protocols**: [../docs/ai-agent-roles-protocols.md](../docs/ai-agent-roles-protocols.md) - Development procedures
- **First Bird Project**: [first-bird/README.md](first-bird/README.md) - Active project technical details

---

**This workflow architecture enables unlimited automation projects on a unified platform with shared testing infrastructure, consistent quality standards, и universal development protocols.**

*Updated: August 30, 2025 - Documentation Refactoring & Architecture Optimization*