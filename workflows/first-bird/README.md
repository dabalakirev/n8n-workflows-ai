# First Bird - Financial Data Automation

**Пилотный проект демонстрирующий возможности n8n-workflows-ai платформы.**

## 🐦 Project Overview
- **Domain**: Financial Data Processing с AI analysis
- **Data Source**: Financial Modeling Prep API
- **AI Engine**: DeepSeek language model
- **Status**: DEV workflows ✅ Complete, PROD deployment pending

## 📋 Project Workflows

### 🤖 AI Deepseek DEV (`ai-deepseek-dev.json`)
- **ID**: `0VAipR4PLHbtkIzw`
- **Function**: AI-powered financial query processing
- **Webhook**: `https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev`
- **Triggers**: Manual + Execute Workflow + Test Webhook

### 🔗 FMP API Router DEV (`fmp-router-dev.json`)
- **ID**: `UmUET85BJqPbpRPp` 
- **Function**: Financial Modeling Prep API routing hub
- **Commands**: Insider.Trading.Latest, Company.Profile и другие
- **Triggers**: Manual + Execute Workflow

## 🧪 Testing

### Test Webhook Architecture
**AI Deepseek** имеет test webhook для MCP testing:
```javascript
// MCP Test Execution
n8n_trigger_webhook_workflow({
  webhookUrl: "https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev?testType=full&testData.input=Analyze%20AAPL&testData.sessionId=test-001",
  httpMethod: "GET"
});
```

**Test Scenarios:**
- Financial analysis testing
- API integration validation  
- Error handling verification

## 🏗️ Architecture

### Current DEV Environment
```
AI Deepseek DEV ──calls──→ FMP Router DEV
       ↑                          ↑
   Test Webhook             Execute Workflow
```

### Planned PROD Environment  
```
AI Deepseek PROD ──calls──→ FMP Router PROD
       ↑                           ↑
  Manual Only              Manual Only
```

## 🔧 Configuration
- **DeepSeek API Key** ✅ Configured
- **FMP API Key** ✅ Configured
- **Required Nodes**: @n8n/n8n-nodes-langchain, n8n-nodes-base

## 🎯 Next Steps
1. **Test Webhook Validation** - Comprehensive MCP testing
2. **PROD Deployment** - Single-trigger production versions
3. **Documentation Update** - Production procedures

## 📊 Performance
- **AI Response**: 3-7 seconds
- **API Response**: 1-3 seconds
- **End-to-end**: 5-12 seconds
- **Test Execution**: <45 seconds

*Refer to platform documentation in docs/ для detailed protocols и testing procedures.*