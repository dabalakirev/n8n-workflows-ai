# Workflow Usage Guide - First Bird Project

**Практическое руководство** по использованию First Bird workflows для financial data automation

## 🚀 Quick Start

### **1. Prerequisites**
- **n8n Cloud или Self-hosted** instance готов
- **FMP API Subscription** (Financial Modeling Prep)
- **DeepSeek API Access** для AI functionality

### **2. Credential Setup**
```
n8n Credentials Required:
├── DeepSeek API → "DeepSeek account"
└── FMP API Key → "FMP API Key" (Generic Credential)
```

### **3. Workflow Import**
```
Импортировать workflows в правильном порядке:
1. FMP API Router (first) - должен быть активен
2. AI Deepseek (second) - ссылается на Router
```

## 🏗️ Workflow Architecture

### **Data Flow Overview:**
```
User Query → AI Deepseek → FMP API Router → Financial API → Analysis → Response
```

### **Environment Separation:**
- **DEV:** Testing, debugging, development
- **PROD:** Production use, stable operations

## 🤖 AI Deepseek Workflow

### **Usage Patterns:**

#### **Simple Financial Questions:**
```json
Input: "Какие были последние сделки инсайдеров?"
Process: AI → FMP Router → Latest insider trades → Analysis
Output: "Последние 10 сделок инсайдеров: [data + insights]"
```

#### **Company-Specific Analysis:**
```json
Input: "Покажи профиль Apple и последние сделки инсайдеров по AAPL"
Process: AI → Multiple FMP calls → Company.Profile + Insider.Trading.Search
Output: "Apple Inc. (Consumer Electronics): [profile] + [insider data analysis]"
```

#### **Person-Specific Queries:**
```json
Input: "Что покупал Elon Musk в последнее время?"
Process: AI → FMP Router → ReportingName search → Analysis
Output: "[Elon Musk's recent transactions + AI insights]"
```

### **AI Capabilities:**
- **Natural Language Processing** financial queries
- **Multi-step Data Retrieval** через FMP Router
- **Intelligent Analysis** и contextual insights
- **Follow-up Questions** handling

### **Example Queries:**
```
"Найди компании с самыми активными покупками инсайдеров"
"Покажи профили топ-5 компаний из Technology сектора"  
"Какие директора активно покупали акции за последний месяц?"
"Сравни активность инсайдеров Apple и Microsoft"
```

## 🔗 FMP API Router Workflow

### **Direct API Usage:**

#### **Latest Insider Trades:**
```json
{
  "toolName": "Insider.Trading.Latest",
  "params": {
    "limit": 20,
    "page": 1
  }
}
```

#### **Company Profile:**
```json
{
  "toolName": "Company.Profile", 
  "params": {
    "symbol": "AAPL"
  }
}
```

#### **Insider by Name:**
```json
{
  "toolName": "Insider.Trading.ReportingName",
  "params": {
    "name": "Tim Cook"
  }
}
```

#### **Company Insider Activity:**
```json
{
  "toolName": "Insider.Trading.Search",
  "params": {
    "symbol": "MSFT",
    "limit": 50
  }
}
```

### **Router Features:**
- **Dynamic URL Construction** на базе routing table
- **Parameter Validation** и encoding
- **Automatic API Key Injection**
- **Error Handling** с meaningful messages

## 🧪 Testing Workflows

### **DEV Environment Testing:**

#### **Manual Testing:**
1. **Open DEV workflow** в n8n
2. **Use pinned test data** или modify inputs
3. **Execute manually** через Manual Trigger
4. **Review results** и verify expected behavior

#### **Automated Testing:**
1. **Test Orchestrator** triggers Execute Workflow Trigger
2. **Automated validation** response structure и content
3. **Performance monitoring** response times
4. **Error scenario testing** invalid inputs

### **Test Scenarios:**

#### **AI Deepseek Tests:**
```json
Test Cases:
├── "Latest insider trades analysis"
├── "AAPL company profile and insider activity"  
├── "Elon Musk trading history"
└── "Invalid company symbol handling"
```

#### **FMP Router Tests:**
```json
Test Cases:
├── Each supported endpoint individually
├── Parameter validation (required/optional)
├── Error scenarios (invalid API key, symbol)
└── Response time performance
```

## 🔧 Configuration Management

### **Environment-Specific Settings:**

#### **DEV Configuration:**
- **Dual Triggers:** Manual + Execute Workflow
- **Test Data:** Pinned data для quick testing
- **Debug Mode:** Verbose logging enabled
- **Rate Limits:** Conservative для testing

#### **PROD Configuration:**  
- **Single Trigger:** Manual only для stability
- **Real Data:** Live API responses
- **Optimized:** Performance-focused settings
- **Monitoring:** Error tracking enabled

### **Credential Management:**
```
Environment Separation:
├── DEV Credentials → Development API keys (limited)
└── PROD Credentials → Production API keys (full access)
```

## 📊 Performance Optimization

### **Response Time Targets:**
- **Simple Queries:** < 3 seconds
- **Complex Analysis:** < 7 seconds  
- **API Router:** < 2 seconds per call
- **Error Scenarios:** < 1 second

### **Optimization Strategies:**
- **Parameter Validation** early в workflow
- **Efficient API Calls** minimize unnecessary requests  
- **Error Handling** quick failure recovery
- **Caching** (future enhancement)

## ⚠️ Troubleshooting

### **Common Issues:**

#### **"Invalid API key" Error:**
```
Solution:
1. Check FMP API Key credential в n8n
2. Verify API key active в FMP dashboard
3. Confirm credential name matches workflow
```

#### **"Command not found" Error:**
```
Solution:
1. Check toolName spelling в request
2. Verify routing table has command
3. Review supported commands list
```

#### **Slow Response Times:**
```
Solution:
1. Check FMP API rate limits
2. Monitor n8n execution resources
3. Optimize query parameters (limit, page)
4. Consider API plan upgrade
```

#### **AI Agent Not Responding:**
```
Solution:
1. Verify DeepSeek API credential
2. Check AI Agent configuration
3. Review tool integration setup
4. Test FMP Router independently
```

### **Debug Procedures:**
1. **Test components separately** (AI vs Router)
2. **Review execution logs** в n8n
3. **Validate credentials** are accessible
4. **Check API service status** для external services

## 🔐 Security Best Practices

### **Credential Security:**
- **Never expose** API keys в logs или responses
- **Regular rotation** of API credentials
- **Monitor usage** для unexpected patterns
- **Access controls** production credentials

### **Data Security:**
- **Temporary processing** financial data not stored
- **Secure transmission** HTTPS only
- **Error logging** excludes sensitive information
- **User privacy** queries not permanently logged

## 📈 Usage Analytics

### **Monitoring Metrics:**
- **Query Success Rate** >95% target
- **Average Response Time** performance tracking
- **Error Frequency** patterns analysis
- **API Usage** cost monitoring

### **Performance Reports:**
- **Weekly Usage** summary reports
- **Error Analysis** trend identification  
- **Cost Tracking** API subscription optimization
- **User Satisfaction** query quality assessment

## 🚀 Production Deployment

### **Pre-Production Checklist:**
- [ ] **All DEV tests** passing successfully
- [ ] **Production credentials** configured и tested
- [ ] **PROD workflows** imported и activated
- [ ] **Monitoring setup** alerts configured
- [ ] **Documentation** updated для production use
- [ ] **Backup procedures** in place

### **Go-Live Process:**
1. **Final DEV validation** all scenarios working
2. **PROD credential setup** verified access
3. **Workflow import** PROD versions deployed
4. **Smoke testing** basic functionality confirmed
5. **User training** provided если necessary
6. **Monitoring activated** alerts operational

---

**Этот guide обеспечивает complete coverage использования First Bird workflows от setup до production deployment.**

*Last Updated: August 2025 - Project-Centric Architecture Implementation*