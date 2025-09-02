# New Project Creation Procedure

**Version:** 1.2  
**Status:** READY  
**Target:** Product Owners, AI Agents, Developers

---

## 🎯 Purpose

Обеспечить стандартизированную процедуру создания новых проектов на платформе с полным покрытием всех necessary компонентов для successful implementation.

**Key Principle:** "Nothing Forgotten, Nothing Redundant"

---

## 📚 Phase 0: Documentation Hierarchy - ОБЯЗАТЕЛЬНЫЕ УРОВНИ

**КРИТИЧЕСКИ ВАЖНО:** Все проекты ДОЛЖНЫ пройти трехуровневую систему документации перед началом разработки.

### 📝 **Level 1: Бриф (идея)**
**Что это:** Нетехническое описание проекта для понимания бизнес-цели

Здесь должна описана сама идея на простом не техническом языке. Требования: она должна быть понятной, последовательной, не противоречивой и потенциально технически реализуемой на n8n. Должны быть упомянуты все источники данных и есть ли доступ к ним.

**✅ Критерии готовности:**
- [ ] Идея изложена понятным языком без технических терминов
- [ ] Логика последовательна и не содержит противоречий
- [ ] Все источники данных перечислены с указанием доступности
- [ ] Реализуемость на n8n платформе подтверждена

### 🔧 **Level 2: Технический бриф**
**Что это:** Детальные технические требования БЕЗ конкретной архитектуры n8n

Этот документ должен раскрывать все технические детали, необходимые для реализации идеи, содержать последовательный сценарий обработки данных, техническую логику этого сценария, описывать все внешние инструменты, которыми мы будем пользоваться, а также четко, технически описывать подробно как именно мы будем работать с этими инструментами. Вместе с тем этот документ не должен предлагать саму архитектуру узлов и workflow n8n. Документ должен быть провалидирован прежде всего на то, "ничего ли мы не забыли" с технической точки зрения, начиная разработку.

**✅ Критерии готовности:**
- [ ] Полный сценарий обработки данных описан
- [ ] Все внешние инструменты и их использование детализированы
- [ ] Техническая логика проработана без пропусков
- [ ] НЕ содержит конкретной n8n архитектуры
- [ ] Валидация "ничего не забыли" пройдена

### 🏗️ **Level 3: Архитектурное решение**
**Что это:** Конкретная структура n8n workflows с обоснованием каждого узла

Этот документ предлагает конкретное архитектурное решение в виде конкретной структуры workflow и их узлов. Для каждого узла он должен обосновывать смысл и оптимальность. Необходима сверка с документацией n8n - будет ли работать этот узел так, как мы планируем, со ссылкой на документацию n8n. Предлагать возможные fallback и обходные пути, если предложенная часть схемы не работает. Документ должен быть провалидирован на то, что решение оптимально и не избыточно, соответствует документации n8n, надежно и без сомнений реализуемо. Если есть сомнения - описать в чем и пути обходных решений.

**✅ Критерии готовности:**
- [ ] Конкретная структура workflow с обоснованием каждого узла
- [ ] Ссылки на n8n документацию для каждого узла
- [ ] Fallback сценарии для проблемных участков
- [ ] Оптимальность и отсутствие избыточности подтверждены
- [ ] Все сомнения описаны с путями решения

### 🔄 **Sequential Validation Process**

**STOP RULES - обязательная последовательность:**
- 🛑 **Level 1 не пройден** → НЕ переходить к Level 2
- 🛑 **Level 2 не пройден** → НЕ переходить к Level 3  
- 🛑 **Level 3 не пройден** → НЕ начинать разработку

---

## 📋 Phase 1: Requirement Analysis
*Базируется на Level 1-2 документации*

### 🔍 **1.1 Business Requirements Validation**
**Source:** Level 1 документация должна предоставить:
- [ ] **Business Objective** - четко определена цель проекта
- [ ] **Success Criteria** - измеримые результаты
- [ ] **Input Data Sources** - источники данных с подтвержденным доступом
- [ ] **Output Requirements** - ожидаемые результаты

### ⚙️ **1.2 Technical Requirements Assessment**  
**Source:** Level 2 документация должна предоставить:
- [ ] **Data Processing Logic** - полный сценарий обработки
- [ ] **External APIs** - endpoints, authentication, rate limits
- [ ] **Credential Requirements** - все необходимые credentials
- [ ] **Integration Points** - детали интеграций

### ❓ **1.3 Completeness Check**
```markdown
Отсутствуют:
- [ ] Business rules?
- [ ] API specifications? 
- [ ] Data formats?
- [ ] Error handling expectations?
- [ ] Security requirements?
```

**GATE:** НЕ продолжать без полных Level 1-2 requirements

---

## 🏗️ Phase 2: Project Architecture  
*Базируется на Level 3 документации*

### 📐 **2.1 Workflow Structure Planning**
**Source:** Level 3 архитектурное решение определяет:

**Single Workflow:** Простые проекты с единой логикой
**Multiple Workflows:** Сложные проекты с разделением ответственности:
```
Parent Workflow (Main):
├── Business Logic Implementation
├── Error Handling & Validation  
├── Child Workflow Coordination
└── Results Aggregation

Child Workflows (Specialized):
├── Data Collection & Processing
├── External API Integration
└── Specific Domain Logic
```

### 🔧 **2.2 Node Selection Validation**
**Requirements:** Level 3 документация должна содержать:
- [ ] **Each node justified** - обоснование выбора каждого узла
- [ ] **n8n documentation links** - ссылки на официальную документацию
- [ ] **Configuration details** - точные настройки узлов
- [ ] **Fallback scenarios** - альтернативные решения

### 🔄 **2.3 Flow Validation**
- [ ] **Data flow logic** соответствует Level 2 сценарию
- [ ] **Error handling** покрывает все критические сценарии
- [ ] **Performance expectations** реалистичны
- [ ] **No circular dependencies** между workflows

**GATE:** Architecture должна полностью соответствовать Level 3 specifications

---

## 🛠️ Phase 3: Implementation Setup

### 📁 **3.1 Project Structure Creation**
```
workflows/[project-name]/
├── dev/                    # DEV workflows
├── prod/                   # PROD workflows  
└── README.md              # Project summary

docs/projects/[project-name]/
├── README.md              # Project overview
├── brief-idea.md          # Level 1: Бриф (идея)  
├── technical-brief.md     # Level 2: Технический бриф
└── architecture.md        # Level 3: Архитектурное решение
```

### 📚 **3.2 Documentation Templates**

#### **Project README Template:**
```markdown
# [Project Name]

## Documentation Levels
- **📝 Level 1:** [Бриф (идея)](brief-idea.md) - ✅ APPROVED
- **🔧 Level 2:** [Технический бриф](technical-brief.md) - ✅ APPROVED  
- **🏗️ Level 3:** [Архитектурное решение](architecture.md) - ✅ APPROVED

## Implementation Status
- **Documentation:** ✅ All levels completed
- **DEV:** [Current Status]
- **PROD:** [Current Status]

## Quick Reference
- **Business Goal:** [One-line summary from Level 1]
- **Tech Stack:** [Key technologies from Level 2]
- **Architecture:** [Workflow structure from Level 3]
```

### 🔒 **3.3 Security & Credentials**
**Source:** Level 2 technical specifications
```markdown
## Required Credentials
1. **[Service]** - [Purpose from Level 2]
   - Type: [Authentication method]
   - n8n Name: [Credential name]
   - Usage: [Workflows that use it]
```

### 🧪 **3.4 Testing Strategy**
**Based on:** Level 3 architecture specifications
- **Test scenarios** from Level 1 success criteria
- **Technical validation** against Level 2 logic
- **Architecture testing** per Level 3 design

---

## ✅ Implementation Checklist

### **Pre-Implementation:**
- [ ] **✅ Level 1 APPROVED** - Business idea validated
- [ ] **✅ Level 2 APPROVED** - Technical details complete  
- [ ] **✅ Level 3 APPROVED** - Architecture design ready
- [ ] **All documentation levels** accessible and complete

### **During Implementation:**
- [ ] **Follow Level 3 architecture** exactly as specified
- [ ] **Implement planned nodes** with n8n documentation compliance
- [ ] **Validate against Level 2** technical requirements
- [ ] **Test Level 1 success criteria** achievement

### **Post-Implementation:**
- [ ] **All documentation levels** archived and accessible
- [ ] **Testing complete** against all three levels
- [ ] **Performance matches** Level 2-3 expectations
- [ ] **Business objectives** from Level 1 achieved

---

## 🎯 Success Criteria

**✅ Project успешен когда:**
- ✅ **Sequential validation** пройдена через все levels
- ✅ **Implementation matches** Level 3 architecture 
- ✅ **Technical performance** соответствует Level 2 specs
- ✅ **Business objectives** из Level 1 достигнуты
- ✅ **Documentation complete** и accessible

**❌ Project НЕ готов если:**
- ❌ **Любой documentation level** missing или incomplete
- ❌ **Implementation diverges** от Level 3 architecture
- ❌ **Performance gap** относительно Level 2 requirements
- ❌ **Business goals unclear** или unmet

---

## 📞 References

- **Platform Protocols:** [AI Agent Execution Protocol](../ai-agent-execution-protocol.md)
- **Testing Guide:** [MCP Webhook Testing Guide](../mcp-webhook-testing-guide.md)
- **Security Standards:** [Security Best Practices](../security-best-practices.md)
- **CI/CD Process:** [MCP CI/CD Deployment Protocol](../mcp-cicd-deployment-protocol.md)

---

**Version History:**
- **v1.0:** Original procedure
- **v1.1:** Added Documentation Hierarchy  
- **v1.2:** Streamlined structure, removed webhook confusion, clarified Level definitions

**Author:** Technical Writer AI Agent  
**Review Required:** Product Owner approval before implementation