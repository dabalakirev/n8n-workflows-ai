# Workflow Usage Guide - First Bird Project

**Практическое руководство** по использованию First Bird workflows для финансовой автоматизации данных

## 🚀 Быстрый старт

### **1. Предварительные требования**
- **n8n Cloud или Self-hosted** instance готов
- **FMP API Subscription** (Financial Modeling Prep) активна
- **DeepSeek API Access** для AI functionality

### **2. Настройка Credentials**
```
Необходимые n8n Credentials:
├── DeepSeek API → "DeepSeek account"
└── FMP API Key → встроен в workflow (настроен)
```

### **3. Текущая структура (v1.2)**
```
First Bird DEV Project (n8n: EAq65uG63UPwwuhk):
├── 🤖 AI Deepseek DEV      (ID: 0VAipR4PLHbtkIzw)
├── 🔗 FMP API Router DEV   (ID: UmUET85BJqPbpRPp)
└── 🧪 Test Orchestrator    (ID: ElnSprIVyJXKlkl3)
```

## 🏗️ Архитектура Workflow

### **Основной поток данных:**
```
User Query → AI Deepseek DEV → FMP API Router DEV → Financial API → Analysis → Response
```

### **Testing поток:**
```
Test Request → Test Orchestrator → Execute Both Workflows → Generate Report → Results
```

### **Разделение сред:**
- **✅ DEV Environment:** Активный, testing, debugging, dual triggers
- **🔄 PROD Environment:** Планируется, single Manual trigger только

## 🤖 AI Deepseek DEV Workflow

### **Паттерны использования:**

#### **Простые финансовые вопросы:**
```json
Input: "Какие были последние сделки инсайдеров?"
Process: AI → FMP Router DEV → Latest insider trades → Analysis
Output: "Последние 10 сделок инсайдеров: [data + insights]"
```

#### **Анализ конкретной компании:**
```json
Input: "Покажи профиль Apple и последние сделки инсайдеров по AAPL"
Process: AI → Multiple FMP calls → Company.Profile + Insider.Trading.Search
Output: "Apple Inc. (Consumer Electronics): [profile] + [insider data analysis]"
```

#### **Персональные запросы:**
```json
Input: "Что покупал Elon Musk в последнее время?"
Process: AI → FMP Router DEV → ReportingName search → Analysis
Output: "[Elon Musk's recent transactions + AI insights]"
```

### **Возможности AI:**
- **Natural Language Processing** финансовых запросов
- **Multi-step Data Retrieval** через FMP Router DEV
- **Intelligent Analysis** и contextual insights
- **Follow-up Questions** handling
- **Integration** с Test Orchestrator для automated testing

### **Примеры запросов:**
```
"Найди компании с самыми активными покупками инсайдеров"
"Покажи профили топ-5 компаний из Technology сектора"  
"Какие директора активно покупали акции за последний месяц?"
"Сравни активность инсайдеров Apple и Microsoft"
```

### **Dual Triggers (DEV):**
- **Manual Trigger:** Для ручного тестирования и debugging
- **Execute Workflow Trigger:** Для Test Orchestrator integration

## 🔗 FMP API Router DEV Workflow

### **Прямое использование API:**

#### **Последние сделки инсайдеров:**
```json
{
  "toolName": "Insider.Trading.Latest",
  "params": {
    "limit": 20,
    "page": 1
  }
}
```

#### **Профиль компании:**
```json
{
  "toolName": "Company.Profile", 
  "params": {
    "symbol": "AAPL"
  }
}
```

#### **Поиск по инсайдеру:**
```json
{
  "toolName": "Insider.Trading.ReportingName",
  "params": {
    "name": "Tim Cook"
  }
}
```

#### **Активность инсайдеров компании:**
```json
{
  "toolName": "Insider.Trading.Search",
  "params": {
    "symbol": "MSFT",
    "limit": 50
  }
}
```

### **Функции Router:**
- **Динамическое построение URL** на базе routing table
- **Parameter Validation** и encoding
- **Автоматическое добавление API Key**
- **Error Handling** с meaningful messages
- **Dual Triggers** для manual и automated testing

## 🧪 Test Orchestrator Workflow

### **✅ Automated Testing Ready (v1.2)**

#### **Webhook Testing:**
```bash
# POST to Test Orchestrator
curl -X POST "https://n8n-instance/webhook/test-orchestrator" \
  -H "Content-Type: application/json" \
  -d '{
    "testSuite": "full",
    "testData": {
      "ai-deepseek": {
        "input": "Get latest insider trading data for AAPL",
        "sessionId": "test-123"
      },
      "fmp-router": {
        "toolName": "Insider.Trading.Latest",
        "params": {"limit": 5}
      }
    }
  }'
```

#### **Test Response Format:**
```json
{
  "executionId": "exec-1234567890",
  "overallStatus": "ALL_PASSED",
  "testResults": {
    "ai-deepseek": {"status": "pass", "output": "Success"},
    "fmp-router": {"status": "pass", "output": "Success"}
  },
  "summary": {"total": 2, "passed": 2, "failed": 0, "successRate": "100%"}
}
```

### **Test Scenarios:**

#### **Automated Test Cases:**
```json
Test Suite Coverage:
├── "AI Deepseek DEV" → Financial query analysis
├── "FMP Router DEV" → API endpoint functionality  
├── "Integration Flow" → AI → Router → Response
└── "Error Handling" → Invalid inputs и API errors
```

## 🔧 Configuration Management

### **Current Configuration (DEV):**
- **Environment:** First Bird DEV Project
- **Dual Triggers:** Manual + Execute Workflow для всех workflows
- **API Keys:** Configured и working
- **Testing:** Fully automated через Test Orchestrator
- **Monitoring:** n8n execution logs + test reports

### **Future Configuration (PROD):**
- **Environment:** First Bird PROD Project (planned)
- **Single Trigger:** Manual only для stability
- **Production Keys:** Separate credentials для PROD
- **Monitoring:** Enhanced error tracking

### **Credential Setup:**
```
Current Status:
├── ✅ DeepSeek API → Configured в AI Deepseek DEV
├── ✅ FMP API Key → Configured в FMP Router DEV
└── ✅ Test Orchestrator → Webhook активен
```

## 📊 Performance Optimization

### **Response Time Targets:**
- **Simple Queries:** < 3 секунды
- **Complex Analysis:** < 7 секунд  
- **API Router:** < 2 секунды per call
- **Test Suite:** < 30 секунд full execution

### **Optimization Strategies:**
- **Parameter Validation** early в workflow
- **Efficient API Calls** minimize unnecessary requests  
- **Error Handling** quick failure recovery
- **Test Automation** reduce manual testing time

## ⚠️ Troubleshooting

### **Распространенные проблемы:**

#### **"Invalid API key" Error:**
```
Решение:
1. Проверить FMP API Key в workflow configuration
2. Verify API key активен в FMP dashboard
3. Confirm workflow has correct API key reference
```

#### **"Command not found" Error:**
```
Решение:
1. Check toolName spelling в request
2. Verify routing table содержит command
3. Review supported commands list в API reference
```

#### **Test Orchestrator не отвечает:**
```
Решение:
1. Verify webhook активен в n8n
2. Check Test Orchestrator workflow активирован
3. Test individual workflows manually first
4. Review webhook URL configuration
```

#### **AI Agent не отвечает:**
```
Решение:
1. Verify DeepSeek API credential
2. Check AI Agent configuration
3. Test FMP Router DEV independently
4. Review tool integration setup
```

### **Debug Procedures:**
1. **Test components separately** (AI vs Router vs Orchestrator)
2. **Review execution logs** в n8n
3. **Validate Test Orchestrator** через webhook call
4. **Check API service status** для external services

## 🔐 Лучшие практики безопасности

### **Credential Security:**
- **Никогда не expose** API keys в logs или responses
- **Regular rotation** of API credentials планируется
- **Monitor usage** для unexpected patterns
- **Environment isolation** DEV vs future PROD

### **Data Security:**
- **Temporary processing** - financial data не stored
- **Secure transmission** - HTTPS только
- **Error logging** excludes sensitive information
- **Test data** - используются safe, non-sensitive examples

## 📈 Usage Analytics

### **Текущий мониторинг:**
- **Test Success Rate** - через Test Orchestrator reports
- **Manual Execution** - через n8n execution logs
- **API Usage** - FMP API call tracking
- **Error Patterns** - analysis через execution history

### **Performance Reports:**
- **Test Results** - automated test suite outcomes
- **Response Times** - execution duration tracking  
- **Error Analysis** - trend identification
- **Integration Status** - AI + Router + Testing health

## 🚀 Production Deployment Plan

### **Pre-Production Checklist:**
- [x] **DEV Environment** полностью функциональный
- [x] **Testing Framework** operational через Test Orchestrator
- [x] **Documentation** comprehensive и up-to-date
- [ ] **PROD Project Creation** в n8n
- [ ] **PROD Workflows** migrated и optimized
- [ ] **Production Monitoring** setup

### **Deployment Process (Future):**
1. **Создать First Bird PROD project** в n8n
2. **Import optimized workflows** (single triggers)
3. **Configure production credentials**
4. **Smoke testing** basic functionality
5. **Documentation updates** для production use
6. **Monitoring activation** alerts operational

## 🎯 Current Status Summary

### **✅ Ready и Operational:**
- **DEV Workflows** - Fully functional
- **Testing Framework** - Automated через Test Orchestrator
- **API Integration** - Working с Financial Modeling Prep
- **Documentation** - Complete и up-to-date

### **🔄 Next Steps:**
- **PROD Environment** creation
- **DEV → PROD Migration** с optimizations
- **Enhanced Monitoring** для production use

---

**Этот guide отражает текущее состояние First Bird project с полным Testing Framework v1.2 и готовностью к PROD развертыванию.**

*Последнее обновление: Август 2025 - v1.2 Testing Framework Active*