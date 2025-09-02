# New Project Creation Procedure

**Version:** 1.1  
**Status:** READY  
**Target:** Product Owners, AI Agents, Developers

---

## 🎯 Purpose

Обеспечить стандартизированную процедуру создания новых проектов на платформе с полным покрытием всех necessary компонентов для successful implementation.

**Key Principle:** "Nothing Forgotten, Nothing Redundant"

---

## 📚 Phase 0: Documentation Hierarchy - ОБЯЗАТЕЛЬНЫЕ УРОВНИ

**КРИТИЧЕСКИ ВАЖНО:** Все проекты ДОЛЖНЫ пройти трехуровневую систему документации перед началом разработки.

### 📝 **1) Бриф (идея)**
Здесь должна описана сама идея на простом не техническом языке. Требования: она должна быть понятной, последовательной, не противоречивой и потенциально технически реализуемой на n8n. Должны быть упомянуты все источники данных и есть ли доступ к ним.

**✅ Критерии готовности:**
- [ ] Идея изложена понятным языком без технических терминов
- [ ] Логика последовательна и не содержит противоречий
- [ ] Все источники данных перечислены с указанием доступности
- [ ] Реализуемость на n8n платформе подтверждена

### 🔧 **2) Технический бриф**
Этот документ должен раскрывать все технические детали, необходимые для реализации идеи, содержать последовательный сценарий обработки данных, техническую логику этого сценария, описывать все внешние инструменты, которыми мы будем пользоваться, а также четко, технически описывать подробно как именно мы будем работать с этими инструментами. Вместе с тем этот документ не должен предлагать саму архитектуру узлов и workflow n8n. Документ должен быть провалидирован прежде всего на то, "ничего ли мы не забыли" с технической точки зрения, начиная разработку.

**✅ Критерии готовности:**
- [ ] Полный сценарий обработки данных описан
- [ ] Все внешние инструменты и их использование детализированы
- [ ] Техническая логика проработана без пропусков
- [ ] НЕ содержит конкретной n8n архитектуры
- [ ] Валидация "ничего не забыли" пройдена

### 🏗️ **3) Архитектурное решение**
Этот документ предлагает конкретное архитектурное решение в виде конкретной структуры workflow и их узлов. Для каждого узла он должен обосновывать смысл и оптимальность. Необходима сверка с документацией n8n - будет ли работать этот узел так, как мы планируем, со ссылкой на документацию n8n. Предлагать возможные fallback и обходные пути, если предложенная часть схемы не работает. Документ должен быть провалидирован на то, что решение оптимально и не избыточно, соответствует документации n8n, надежно и без сомнений реализуемо. Если есть сомнения - описать в чем и пути обходных решений.

**✅ Критерии готовности:**
- [ ] Конкретная структура workflow с обоснованием каждого узла
- [ ] Ссылки на n8n документацию для каждого узла
- [ ] Fallback сценарии для проблемных участков
- [ ] Оптимальность и отсутствие избыточности подтверждены
- [ ] Все сомнения описаны с путями решения

### 🔄 **CI/CD Integration с Documentation Levels**

**Sequential Gates Approach:**
```
Level 1: Бриф → Feeds into → Phase 1: Requirement Analysis
Level 2: Технический бриф → Feeds into → Phase 2: Project Architecture  
Level 3: Архитектурное решение → Ready for → Phase 3: Implementation
```

**STOP RULES:**
- 🛑 **Level 1 не пройден** → НЕ переходить к техническому анализу
- 🛑 **Level 2 не пройден** → НЕ начинать архитектурное планирование  
- 🛑 **Level 3 не пройден** → НЕ начинать implementation

---

## 📋 Phase 1: Requirement Analysis & Validation

### 🔍 **Requirement Completeness Validation**
**(Enhanced с Documentation Level 1 & 2 validation)**

**ОБЯЗАТЕЛЬНАЯ процедура перед началом любого проекта:**

#### **1.1 Product Owner Input Analysis**
**Checklist вводных данных (должен соответствовать Level 1-2 документации):**
- [ ] **Business Objective** - четко определена цель проекта ✅ Level 1
- [ ] **Success Criteria** - measurable outcomes ✅ Level 1
- [ ] **Input Data Sources** - откуда поступают данные ✅ Level 1
- [ ] **Output Requirements** - что должно быть на выходе ✅ Level 2
- [ ] **Integration Points** - с какими системами интегрироваться ✅ Level 2
- [ ] **Performance Expectations** - SLA, throughput, response time ✅ Level 2
- [ ] **Security Requirements** - data sensitivity ✅ Level 2

#### **1.2 Sufficiency Validation**
**Проверка BEFORE начала разработки (должна соответствовать Level 2):**
```markdown
## ❓ Missing Information Checklist
- [ ] Неясные business rules?
- [ ] Отсутствующие API specifications?
- [ ] Неопределенные data formats?
- [ ] Unclear error handling expectations?
- [ ] Missing credential requirements?
- [ ] Undefined integration boundaries?
```

**STOP RULE:** НЕ продолжать без complete requirements + validated Level 1-2 documentation

### 🔍 **Dependencies Analysis**
- **External Services** - APIs, databases, third-party tools ✅ из Level 2
- **Platform Dependencies** - existing workflows, shared resources
- **Credential Dependencies** - authentication requirements ✅ из Level 2
- **Data Dependencies** - input sources, data quality expectations ✅ из Level 1-2

### ⚙️ **Technical Requirements Assessment**
- **API Endpoints** - documentation, rate limits, authentication ✅ из Level 2
- **Database Requirements** - schemas, connections, permissions ✅ из Level 2  
- **Credentials Mapping** - what credentials needed where ✅ из Level 2
- **External Tools** - integrations requirements ✅ из Level 2

---

## 🏗️ Phase 2: Project Architecture
**(Enhanced с Level 3 Архитектурное решение validation)**

### ⚙️ **Workflow Architecture Planning**

#### **2.1 Workflow Architecture Design**
**Определение структуры (должно соответствовать Level 3 документации):**
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
- **Principle:** Architecture должна соответствовать business requirements + Level 3 design

#### **2.2 Data Flow Architecture**
- **Input → Processing → Output** flow design ✅ из Level 3
- **Error propagation** strategy ✅ из Level 3
- **Data validation** points ✅ из Level 3
- **State management** approach ✅ из Level 3

### 🔌 **Node Selection Strategy**

#### **2.3 Node Selection Principles**
**Выбор nodes исходя из Level 3 архитектурного решения:**
- **Follow Level 3 node specifications** с n8n documentation validation
- **Verify каждый узел** против n8n documentation (required в Level 3)
- **Implement fallback strategies** согласно Level 3 planning
- **Optimize for performance** - balance functionality vs simplicity

**Level 3 Integration Requirements:**
- **Each node justified** according to Level 3 documentation
- **n8n documentation links** verified and accessible
- **Fallback scenarios** planned and documented
- **No redundancy** confirmed in architecture

### 🔄 **Execution Flow Validation**

#### **2.4 Flow Safety Checklist (Enhanced с Level 3 validation)**
- [ ] **No circular dependencies** между workflows ✅ проверено в Level 3
- [ ] **Clear error termination** paths ✅ из Level 3 fallback scenarios
- [ ] **Resource cleanup** after execution ✅ planned в Level 3
- [ ] **Timeout handling** для long-running processes ✅ из Level 3

### 📈 **Performance Considerations**

#### **2.5 Scalability Planning (из Level 2-3 документации)**
- **Data Volume** - expected throughput ✅ из Level 2
- **Response Time** - SLA requirements ✅ из Level 2  
- **Resource Optimization** - efficient node usage ✅ из Level 3
- **Caching Strategy** - где appropriate ✅ из Level 3

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
        ├── README.md              # ЕДИНСТВЕННЫЙ файл - структурированный
        ├── brief-idea.md          # Level 1: Бриф (идея)
        ├── technical-brief.md     # Level 2: Технический бриф
        └── architecture.md        # Level 3: Архитектурное решение
```

**Принцип документации:** **STRUCTURED LEVELS + ЕМКОСТЬ**
- **Level 1-3 documents** - отдельные файлы для каждого уровня
- **Project README** - summary + links к levels
- Deployment процедуры - следовать existing CI/CD protocol

### 📚 **Documentation Templates**

#### **3.2 Project README Template (Enhanced)**
```markdown
# [Project Name]

## 📋 Содержание
- [Documentation Levels](#documentation-levels)
- [Business Objective](#business-objective)
- [Architecture Summary](#architecture-summary)  
- [Implementation Status](#implementation-status)

## Documentation Levels
**📝 Level 1:** [Бриф (идея)](brief-idea.md) - ✅ APPROVED
**🔧 Level 2:** [Технический бриф](technical-brief.md) - ✅ APPROVED  
**🏗️ Level 3:** [Архитектурное решение](architecture.md) - ✅ APPROVED

## Business Objective
[Clear business goal - summary from Level 1]

## Architecture Summary
[Workflow structure - summary from Level 3]

## Implementation Status
**Documentation:** ✅ All levels completed
**DEV:** [Status]
**PROD:** [Status]
```

### 🔒 **Security & Credential Setup**

#### **3.3 Security Checklist (Enhanced с Level 2 validation)**
- [ ] **Credential inventory** - все credentials из Level 2 определены
- [ ] **Data sensitivity** - classification из Level 1-2 
- [ ] **Security requirements** из Level 2 implemented

#### **3.4 Credential Management Plan**
```markdown
## Required Credentials (из Level 2 Technical Brief)
1. **[Service Name]** - [Purpose from Level 2]
   - Type: API Key/OAuth/Basic Auth
   - n8n Credential Name: [Name in n8n]
   - Usage: [Which workflows - from Level 3]

2. **[Database/API Name]** - [Purpose from Level 2]
   - Connection Details: [Requirements from Level 2]
   - Permissions: [From Level 2 analysis]
```

### 🧪 **Testing Strategy Implementation**

#### **3.5 Testing Protocol (Level 3 architecture validation)**
**Следовать стандартным протоколам + Level 3 specifications:**
- **Test Webhook pattern** - согласно Level 3 architecture
- **Parent workflow testing** - validate Level 3 node selections
- **Fallback scenarios testing** - verify Level 3 backup plans

---

## 📋 Implementation Checklist (Enhanced)

### **Pre-Implementation Validation:**
- [ ] **✅ Level 1: Бриф approved** - идея validated
- [ ] **✅ Level 2: Technical Brief approved** - technical details complete
- [ ] **✅ Level 3: Architecture approved** - n8n implementation ready
- [ ] **All requirements complete** (Phase 1 validation passed)
- [ ] **Resources allocated** (credentials, access, dependencies)

### **During Implementation:**
- [ ] **Follow Level 3 architecture** exactly as specified
- [ ] **Implement planned nodes** с n8n documentation compliance
- [ ] **Test fallback scenarios** from Level 3
- [ ] **Follow existing CI/CD protocol** для deployment

### **Post-Implementation:**
- [ ] **Level 1-3 documentation** archived и accessible
- [ ] **Testing procedures validated** через MCP tools
- [ ] **Architecture performance** matches Level 2-3 expectations

---

## 🎯 Success Criteria (Enhanced)

**✅ Project считается properly created когда:**
- ✅ **Level 1-3 Documentation complete** и approved
- ✅ **Sequential validation passed** через все levels
- ✅ **n8n architecture matches** Level 3 specifications
- ✅ **Performance meets** Level 2 expectations
- ✅ **Standard structure** implemented
- ✅ **Test Webhook pattern** working (if needed)
- ✅ **Security checklist** completed

**❌ Project НЕ ready если:**
- ❌ **Any documentation level missing** или not approved
- ❌ **Level 3 architecture not validated** против n8n docs
- ❌ **Technical requirements incomplete** (Level 2 gaps)
- ❌ Performance not planned или tested

---

## 📞 References

- **Platform Protocols:** [AI Agent Execution Protocol](../ai-agent-execution-protocol.md)
- **Testing Guide:** [MCP Webhook Testing Guide](../mcp-webhook-testing-guide.md)
- **Security Standards:** [Security Best Practices](../security-best-practices.md)
- **CI/CD Process:** [MCP CI/CD Deployment Protocol](../mcp-cicd-deployment-protocol.md)

---

**Created:** September 1, 2025  
**Updated:** September 2, 2025 - Added Documentation Hierarchy  
**Author:** Technical Writer AI Agent  
**Review Required:** Product Owner approval before implementation