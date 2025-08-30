# Testing Strategy - Test Webhook - Test Execution подход

## 🎯 Концепция тестирования платформы

**Test Webhook - Test Execution** - упрощенный подход к тестированию n8n workflows через прямое тестирование parent workflows с естественным выполнением child workflows.

## 🏗️ Архитектура тестирования

### **Основной принцип:**
- **Прямое тестирование:** Parent workflow тестируется напрямую через dedicated test webhook
- **Естественное выполнение:** Child workflows выполняются естественно в процессе parent workflow execution
- **Мониторинг результатов:** Отслеживание результатов после завершения parent trigger
- **Упрощенная архитектура:** Исключение сложной orchestration layer

### **Структура тестирования:**
```
Test Request ──→ Parent Workflow Test Webhook ──→ Parent выполняется ──→ Child Workflows выполняются естественно ──→ Мониторинг результатов
```

---

## 🌐 MCP Webhook Testing

**Model Context Protocol (MCP) Webhook Testing** - практический подход к тестированию n8n workflows через MCP tools с использованием webhook triggers для automation и validation.

### **📡 Webhook Discovery Process**

#### **Step 1: Get Workflow Details via MCP**
```javascript
// Используйте n8n MCP для получения workflow information
const workflowDetails = await n8n_get_workflow_details({
  id: "workflow_id"
});

// Проверьте response на webhook availability
if (workflowDetails.hasWebhookTrigger) {
  const webhookPath = workflowDetails.webhookPath; // e.g., "ai-deepseek-dev"
  const webhookUrl = `https://dm83.app.n8n.cloud/webhook/${webhookPath}`;
}
```

#### **Step 2: Webhook URL Construction**
```
Format: https://[n8n-instance]/webhook/[webhookPath]
Example: https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev
```

### **🧪 Webhook Execution Methods**

#### **✅ CORRECT: Use n8n MCP Tools**
```javascript
// ALWAYS use n8n_trigger_webhook_workflow для webhook testing
const testResult = await n8n_trigger_webhook_workflow({
  webhookUrl: "https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev",
  httpMethod: "GET",
  waitForResponse: true,
  data: {} // For POST requests
});

// For GET parameters, include in URL:
const testWithParams = await n8n_trigger_webhook_workflow({
  webhookUrl: "https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev?testType=full&testData.input=Test%20Query",
  httpMethod: "GET", 
  waitForResponse: true
});
```

#### **❌ NEVER: Use web_fetch for webhooks**
```javascript
// ❌ DON'T DO THIS - web_fetch cannot access n8n webhook URLs
// await web_fetch({url: "https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev"});
// Results in 403/permissions errors
```

### **📊 MCP Test Data Format**

#### **GET Request Parameters Structure:**
```
https://[instance]/webhook/[path]?testType=full&parentWorkflow=workflow-name&testData.input=Test%20Query&testData.sessionId=session-id&monitoring.trackChildExecution=true&monitoring.timeout=60s
```

**Parameter Specifications:**
- `testType`: "full" | "quick" | "specific"
- `parentWorkflow`: Workflow identifier для tracking
- `testData.input`: URL-encoded test input string
- `testData.sessionId`: Test session identifier
- `monitoring.trackChildExecution`: "true" | "false" 
- `monitoring.timeout`: "60s" (or desired timeout)

#### **Expected MCP Response Format:**
```json
{
  "testExecution": {
    "executionId": "exec-123456789",
    "status": "success",
    "timestamp": "2025-08-30T14:20:16.000Z",
    "parentWorkflow": {
      "name": "ai-deepseek",
      "status": "completed",
      "testType": "full"
    },
    "testResults": {
      "aiResponse": "Generated response text",
      "childWorkflows": [
        {
          "name": "fmp-router",
          "status": "completed",
          "callCount": "tracked-automatically"
        }
      ]
    }
  }
}
```

### **⚠️ CRITICAL MCP Testing Guidelines для AI Agents**

#### **DO's:**
- ✅ **ALWAYS use n8n MCP tools** для webhook discovery и execution
- ✅ **Use n8n_get_workflow_details** для finding webhook URLs
- ✅ **Use n8n_trigger_webhook_workflow** для webhook execution
- ✅ **URL-encode parameters** properly для GET requests
- ✅ **Wait for response** с waitForResponse: true для complete testing

#### **DON'Ts:**
- ❌ **NEVER use web_fetch** для n8n webhook URLs (permissions restrictions)
- ❌ **Don't assume webhook availability** без checking workflow details
- ❌ **Don't hardcode webhook URLs** - always discover динамически
- ❌ **Don't skip parameter encoding** для special characters
- ❌ **Don't test production webhooks** (they don't exist by security design)

### **🔧 MCP Webhook Testing Troubleshooting**

#### **Common Issues и Solutions:**

**Issue: "Webhook URL not found"**
- **Cause:** Workflow не имеет webhook trigger или incorrect ID
- **Solution:** Use n8n_get_workflow_details для verification webhook availability
- **Prevention:** Always check hasWebhookTrigger boolean в response

**Issue: "403 Permission Denied"**
- **Cause:** Using web_fetch instead of n8n MCP tools
- **Solution:** Replace web_fetch с n8n_trigger_webhook_workflow
- **Prevention:** Follow MCP tool guidelines strictly

**Issue: "Invalid test data format"**
- **Cause:** Incorrect parameter encoding или missing required fields
- **Solution:** Use proper URL encoding и verify test data structure
- **Prevention:** Follow established parameter specifications

**Issue: "Timeout during execution"**
- **Cause:** Workflow complexity или API dependencies delays
- **Solution:** Increase timeout parameter или check workflow performance
- **Prevention:** Use realistic timeout values (60s+) для complex workflows

### **📈 MCP Testing Best Practices**

#### **For AI Agent Development:**
1. **Always discover webhooks динамически** через n8n_get_workflow_details
2. **Use consistent parameter naming** согласно established protocol
3. **Implement proper error handling** для webhook execution failures
4. **Monitor parent-child execution patterns** для comprehensive validation
5. **Document test scenarios** для reproducible testing

#### **For Platform Integration:**
1. **Integrate MCP webhook testing** в CI/CD pipelines
2. **Create reusable test templates** для different project types
3. **Establish baseline performance metrics** для webhook execution times
4. **Implement automated validation** result analysis
5. **Maintain webhook configuration templates** для new projects

### **🎯 MCP Testing Success Indicators**

- **Webhook Discovery**: 100% success rate в finding available webhooks
- **Execution Reliability**: Consistent webhook execution через MCP tools
- **Response Validation**: Proper test response format compliance
- **Error Handling**: Graceful handling edge cases и failures
- **Performance**: < 60 seconds для complete parent-child test execution

---

## 🔧 Архитектура parent-child workflows

### **Parent Workflow структура (пример: AI Deepseek DEV):**
```
┌─────────────────────────────────────────────────┐
│              Parent Workflow                    │
│                                                 │
│  Manual Trigger ──┐                             │
│                   ├──→ [Parent Logic] ──→ Call  │──→ Output
│  Test Webhook ────┘                     Child   │
│  Trigger                                        │
│                                                 │
│  Естественно вызывает Child Workflows           │
└─────────────────────────────────────────────────┘
```

### **Child Workflow структура (пример: FMP Router DEV):**
```
┌─────────────────────────────────────────────────┐
│              Child Workflow                     │
│                                                 │
│  Manual Trigger ──┐                             │
│                   ├──→ [Child Logic] ──→        │──→ Output  
│  Execute Workflow │                             │
│  Trigger ──────────┘                            │
│      ↑                                          │
│      │ Вызывается Parent Workflow естественно   │
└─────────────────────────────────────────────────┘
```

---

## 🌐 Процесс тестирования

### **1. Test Webhook конфигурация:**
```javascript
// Parent Workflow test webhook accepts:
{
  "testType": "full|quick|specific",
  "parentWorkflow": "ai-deepseek",
  "testData": {
    "input": "test financial query",
    "sessionId": "test-session-123",
    "expectedChildCalls": ["fmp-router"]
  },
  "monitoring": {
    "trackChildExecution": true,
    "validateResults": true,
    "timeout": "60s"
  }
}
```

### **2. Testing flow:**
```
AI Agent/CI ──→ POST Test Data ──→ Parent Webhook ──→ Parent Executes ──→ Child Executes ──→ Monitor Results ──→ Validate ──→ Report
```

### **3. Result monitoring:**
- **Parent execution tracking** - мониторинг выполнения parent workflow
- **Child execution detection** - отслеживание вызовов child workflows
- **Data flow validation** - проверка передачи данных между workflows
- **Error handling verification** - тестирование обработки ошибок

---

## 📊 Testing data formats

### **Test Input Format:**
```json
{
  "project": "first-bird",
  "testSuite": "full|quick|specific",
  "parentWorkflow": {
    "name": "ai-deepseek",
    "testData": {
      "input": "analyze AAPL financial performance",
      "sessionId": "test-session-001"
    }
  },
  "validation": {
    "expectChildCalls": ["fmp-router"],
    "validateResponse": true,
    "checkErrorHandling": true
  }
}
```

### **Test Output Format:**
```json
{
  "testExecution": {
    "executionId": "exec-test-12345",
    "status": "success|failure",
    "duration": "45.2s",
    "parentWorkflow": {
      "name": "ai-deepseek",
      "status": "completed",
      "duration": "42.1s"
    },
    "childWorkflows": [
      {
        "name": "fmp-router", 
        "status": "completed",
        "duration": "3.1s",
        "callCount": 1
      }
    ],
    "dataFlow": {
      "parentToChild": "validated",
      "childToParent": "validated"
    },
    "validation": {
      "expectedChildCalls": "passed",
      "responseValidation": "passed",
      "errorHandling": "not_tested"
    }
  }
}
```

---

## 🏗️ Project Environment Structure

### **DEV Environment (тестируемая среда):**
- **Parent Workflow Triggers**: 2 (Manual + Test Webhook)
- **Child Workflow Triggers**: 2 (Manual + Execute Workflow) 
- **Testing Integration**: ✅ Готово для прямого тестирования
- **Webhook URLs**: Доступны для test automation

### **PROD Environment (production среда):**
- **Parent Workflow Triggers**: 1 (Manual only)
- **Child Workflow Triggers**: 1 (Manual only)
- **Testing Integration**: ❌ Недоступно (by design)
- **Security**: Production workflows не имеют test endpoints

---

## 🔧 Implementation strategy

### **Parent Workflow setup:**
1. **Добавить Test Webhook Trigger** к parent workflow (например, AI Deepseek DEV)
2. **Сконфигурировать test data structure** для принятия тестовых данных
3. **Реализовать execution result logging** для мониторинга
4. **Обеспечить error handling** для тестовых сценариев

### **Child Workflow integration:**
1. **Поддерживать Execute Workflow trigger** в child workflows (например, FMP Router DEV)
2. **Обеспечить predictable response format** для parent workflow
3. **Реализовать proper error propagation** к parent workflow
4. **Валидировать data contracts** между parent и child

### **Testing automation:**
1. **CI/CD integration** - использование parent workflow test webhooks в GitHub Actions
2. **Test scenario management** - определение test cases для различных scenarios
3. **Result monitoring** - автоматическое отслеживание parent-child execution
4. **Quality gates** - блокирование deployment при failed tests

---

## ⚠️ Testing constraints и limitations

### **n8n API ограничения:**
- ❌ Невозможно активировать/деактивировать workflows программно
- ❌ Невозможно запускать Manual Trigger workflows напрямую
- ✅ **МОЖНО вызывать workflows через Execute Workflow nodes** (child workflows)
- ✅ **МОЖНО триггерить workflows через webhooks** (parent workflows с test webhooks)

### **Testing scope:**
- **✅ Полное тестирование** parent workflow logic через test webhooks
- **✅ Естественное тестирование** child workflow integration
- **✅ Валидация data flow** между parent и child workflows
- **⚠️ Manual Trigger logic** тестируется косвенно через shared logic
- **❌ Schedule triggers** не тестируются (platform limitation)

---

## 📝 Implementation checklist

### **Parent Workflow (например, AI Deepseek DEV):**
- [ ] **Test Webhook Trigger добавлен** с appropriate configuration
- [ ] **Test data structure определена** для различных test scenarios
- [ ] **Execution logging реализовано** для мониторинга результатов
- [ ] **Error handling протестировано** для edge cases
- [ ] **Child workflow calls validated** в тестовой среде

### **Child Workflow (например, FMP Router DEV):**
- [ ] **Execute Workflow trigger настроен** для parent calls
- [ ] **Response format standardized** для consistent integration
- [ ] **Error propagation реализовано** к parent workflow
- [ ] **Data contract validated** с parent workflow expectations

### **Testing Integration:**
- [ ] **CI/CD pipeline updated** для использования parent webhook testing
- [ ] **Test scenarios defined** для различных use cases
- [ ] **Monitoring solution configured** для tracking execution results
- [ ] **Quality gates implemented** для automated validation
- [ ] **Documentation updated** с new testing procedures

---

## 🎯 Success metrics

### **Testing effectiveness:**
- **Parent Workflow Coverage**: 100% logic coverage через test webhooks
- **Child Integration Validation**: Все child calls протестированы
- **Data Flow Accuracy**: Валидация передачи данных между workflows
- **Error Handling Coverage**: Тестирование различных error scenarios

### **Operational metrics:**
- **Test Execution Time**: < 60 секунд для полного parent-child test
- **Setup Complexity**: Простая конфигурация test webhooks vs сложная orchestration
- **Maintenance Overhead**: Минимальное maintenance vs centralized orchestrator
- **Scalability**: Легкое добавление новых projects без orchestrator changes

---

## 🔄 Migration от Test Orchestrator

### **Deprecation план:**
1. **Implement Test Webhook approach** в current workflows
2. **Validate new testing methodology** с comprehensive test scenarios  
3. **Update CI/CD integration** для использования new approach
4. **Phase out Test Orchestrator** после successful validation
5. **Archive legacy documentation** и update всех references

### **Benefits новой архитектуры:**
- **Упрощение:** Исключение complex orchestration layer
- **Естественность:** Тестирование actual production execution patterns
- **Maintenance:** Reduced infrastructure complexity
- **Debugging:** Direct parent workflow issue identification
- **Scalability:** Easy addition новых projects без orchestrator modifications

---

**Этот testing strategy представляает fundamental improvement в platform testing methodology, eliminates unnecessary complexity while improving testing effectiveness и maintainability через natural parent-child workflow execution patterns.**

### **📚 Связанная документация:**
- **[MCP Webhook Testing Guide](mcp-webhook-testing-guide.md)** - Comprehensive step-by-step guide
- **[AI Agent Roles & Protocols](ai-agent-roles-protocols.md)** - Webhook testing integration в AI workflows
- **[First Bird Project](../workflows/first-bird/README.md)** - Working webhook configuration examples