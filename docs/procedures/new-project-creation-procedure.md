# New Project Creation Procedure

**Version:** 1.0  
**Status:** READY  
**Target:** Product Owners, AI Agents, Developers

---

## 🎯 Purpose

Обеспечить стандартизированную процедуру создания новых проектов на платформе с полным покрытием всех necessary компонентов для successful implementation.

**Key Principle:** "Nothing Forgotten, Nothing Redundant"

---

## 📋 Phase 1: Requirement Analysis & Validation

### 🔍 **Requirement Completeness Validation**

**ОБЯЗАТЕЛЬНАЯ процедура перед началом любого проекта:**

#### **1.1 Product Owner Input Analysis**
**Checklist вводных данных:**
- [ ] **Business Objective** - четко определена цель проекта
- [ ] **Success Criteria** - measurable outcomes
- [ ] **Input Data Sources** - откуда поступают данные
- [ ] **Output Requirements** - что должно быть на выходе
- [ ] **Integration Points** - с какими системами интегрироваться
- [ ] **Performance Expectations** - SLA, throughput, response time
- [ ] **Security Requirements** - data sensitivity

#### **1.2 Sufficiency Validation**
**Проверка BEFORE начала разработки:**
```markdown
## ❓ Missing Information Checklist
- [ ] Неясные business rules?
- [ ] Отсутствующие API specifications?
- [ ] Неопределенные data formats?
- [ ] Unclear error handling expectations?
- [ ] Missing credential requirements?
- [ ] Undefined integration boundaries?
```

**STOP RULE:** НЕ продолжать без complete requirements

### 🔍 **Dependencies Analysis**
- **External Services** - APIs, databases, third-party tools
- **Platform Dependencies** - existing workflows, shared resources
- **Credential Dependencies** - authentication requirements
- **Data Dependencies** - input sources, data quality expectations

### ⚙️ **Technical Requirements Assessment**
- **API Endpoints** - documentation, rate limits, authentication
- **Database Requirements** - schemas, connections, permissions  
- **Credentials Mapping** - what credentials needed where
- **External Tools** - integrations requirements

---

## 🏗️ Phase 2: Project Architecture

### ⚙️ **Workflow Architecture Planning**

#### **2.1 Workflow Architecture Design**
**Определение структуры:**
- **Single Workflow** - если проект простой и самодостаточный
- **Multiple Workflows** - если требуется разделение логики:
  ```
  Parent Workflow (Orchestrator):
  ├── Main Business Logic
  ├── Error Handling & Validation
  ├── Test Webhook Support ⚠️ MANDATORY
  └── Child Workflow Orchestration (if needed)

  Child Workflows (Specialized):
  ├── Specific Domain Logic
  ├── External API Integration
  └── Data Processing Tasks
  ```
- **Principle:** Architecture должна соответствовать business requirements, НЕ forced patterns

#### **2.2 Data Flow Architecture**
- **Input → Processing → Output** flow design
- **Error propagation** strategy
- **Data validation** points
- **State management** approach

### 🔌 **Node Selection Strategy**

#### **2.3 Node Selection Principles**
**Выбор nodes исходя из project requirements:**
- **Analyze business logic** → select appropriate processing nodes
- **Check data sources** → select optimal input/trigger nodes  
- **Plan integrations** → select connectivity nodes
- **Consider complexity** → balance functionality vs simplicity

**General Guidelines:**
- **Use latest node versions** - check n8n documentation
- **Prefer stable nodes** - avoid experimental features
- **Optimize for performance** - choose efficient node combinations
- **Plan for maintainability** - clear, understandable configurations

### 🔄 **Execution Flow Validation**

#### **2.4 Flow Safety Checklist**
- [ ] **No circular dependencies** между workflows
- [ ] **Clear error termination** paths
- [ ] **Resource cleanup** after execution
- [ ] **Timeout handling** для long-running processes

### 📈 **Performance Considerations**

#### **2.5 Scalability Planning**
- **Data Volume** - expected throughput
- **Response Time** - SLA requirements  
- **Resource Optimization** - efficient node usage
- **Caching Strategy** - где appropriate

---

## 🛠️ Phase 3: Implementation Setup

### 📁 **Project Structure Creation**

#### **3.1 Standard Directory Structure**
```
workflows/
└── [project-name]/
    ├── dev/                    # DEV environment workflows
    │   └── [workflow-files].json
    ├── prod/                   # PROD environment workflows  
    │   └── [workflow-files].json
    └── README.md              # Project documentation (ЕМКО!)

docs/
└── projects/
    └── [project-name]/
        └── README.md          # ЕДИНСТВЕННЫЙ файл - структурированный с содержанием
```

**Принцип документации:** **ЕМКОСТЬ БЕЗ ИЗБЫТОЧНОСТИ**
- Все в одном README с четкой структурой и ссылками
- Никаких дополнительных MD файлов
- Deployment процедуры - следовать existing CI/CD protocol

### 📚 **Documentation Templates**

#### **3.2 Project README Template**
```markdown
# [Project Name]

## 📋 Содержание
- [Business Objective](#business-objective)
- [Architecture](#architecture)  
- [API Integration](#api-integration)
- [Credentials](#credentials)
- [Testing](#testing)
- [Deployment Status](#deployment-status)

## Business Objective
[Clear business goal]

## Architecture
[Workflow structure description - single or multiple workflows]

## API Integration
**Endpoints:** [List with documentation]
**Authentication:** [Method and requirements]
**Rate Limits:** [Specifications]

## Credentials  
[Required credentials list - see section 3.3]

## Testing
**Test Webhook:** [URL pattern]
**Test Scenarios:** [Key test cases]

## Deployment Status
**DEV:** [Status]
**PROD:** [Status]
```

### 🔒 **Security & Credential Setup**

#### **3.3 Security Checklist**
- [ ] **Credential inventory** - все необходимые credentials определены
- [ ] **Data sensitivity** - classification и handling
- [ ] **Credential requirements** документированы в project README

#### **3.4 Credential Management Plan**
```markdown
## Required Credentials
1. **[Service Name]** - [Purpose]
   - Type: API Key/OAuth/Basic Auth
   - n8n Credential Name: [Name in n8n]
   - Usage: [Which workflows use it]

2. **[Database/API Name]** - [Purpose]
   - Connection Details: [Requirements]
   - Permissions: [Read/Write access needed]
```

**Note:** DEV/PROD используют same credentials - no separation needed

### 🧪 **Testing Strategy Implementation**

#### **3.5 Testing Protocol**
**Следовать стандартным протоколам тестирования:**
- **Test Webhook pattern** - согласно [MCP Webhook Testing Guide](../mcp-webhook-testing-guide.md)
- **Parent workflow** ОБЯЗАТЕЛЬНО должен поддерживать test webhooks
- **Standard testing procedures** применяются ко всем проектам

---

## 📋 Implementation Checklist

### **Pre-Implementation Validation:**
- [ ] **All requirements complete** (Phase 1 validation passed)
- [ ] **Architecture approved** (Phase 2 design confirmed)
- [ ] **Resources allocated** (credentials, access, dependencies)

### **During Implementation:**
- [ ] **Follow folder structure** exactly as specified
- [ ] **Create documentation** according to templates (ЕМКО!)
- [ ] **Implement Test Webhook pattern** if multiple workflows
- [ ] **Follow existing CI/CD protocol** для deployment

### **Post-Implementation:**
- [ ] **Documentation complete** и up-to-date
- [ ] **Testing procedures validated** через MCP tools
- [ ] **CI/CD deployment** готов following standard protocols

---

## 🎯 Success Criteria

**✅ Project считается properly created когда:**
- ✅ **Complete requirements** validated и documented
- ✅ **Standard structure** implemented
- ✅ **Documentation** created (ЕМКО, without redundancy)
- ✅ **Test Webhook pattern** working (if needed)
- ✅ **Security checklist** completed
- ✅ **Performance planning** documented

**❌ Project НЕ ready если:**
- ❌ Missing essential documentation
- ❌ Incomplete requirement analysis
- ❌ Security considerations ignored
- ❌ Performance not planned

---

## 📞 References

- **Platform Protocols:** [AI Agent Execution Protocol](../ai-agent-execution-protocol.md)
- **Testing Guide:** [MCP Webhook Testing Guide](../mcp-webhook-testing-guide.md)
- **Security Standards:** [Security Best Practices](../security-best-practices.md)
- **CI/CD Process:** [MCP CI/CD Deployment Protocol](../mcp-cicd-deployment-protocol.md)

---

**Created:** September 1, 2025  
**Author:** Technical Writer AI Agent  
**Review Required:** Product Owner approval before implementation