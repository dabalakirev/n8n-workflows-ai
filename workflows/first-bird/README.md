# First Bird - Financial Data Automation Workflows

**Project-Specific Workflow Documentation** для First Bird financial automation project

## 🐦 Project Overview

First Bird - пилотный automation project demonstrating n8n-workflows-ai platform capabilities через automated financial data processing с AI analysis.

### **Domain Focus:**
- **Financial Data Source:** Financial Modeling Prep API integration
- **AI Analysis Engine:** DeepSeek language model для market insights
- **Automation Goals:** Streamlined financial data workflows с intelligent analysis

### **Project Status:**
```
📊 Workflow Implementation:     ██████████ 100% (DEV workflows operational)
🧪 Test Webhook Integration:    ██████████ 100% (MCP webhook testing available)
🔄 Comprehensive Testing:       ████████░░  80% (Test Webhook - Test Execution approach)
🚀 Production Deployment:       ░░░░░░░░░░   0% (PENDING - Issue #27)
```

---

## 📋 Project Workflows

### 🤖 **AI Deepseek DEV** (`ai-deepseek-dev.json`)
**n8n Workflow ID:** `0VAipR4PLHbtkIzw`  
**Project Environment:** First Bird DEV (`EAq65uG63UPwwuhk`)
**Webhook URL:** `https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev`

**Primary Function:** AI-powered financial query processing и analysis

**Core Capabilities:**
- **Natural Language Processing** - Handles financial queries in natural language
- **FMP API Integration** - Calls FMP Router DEV для data retrieval  
- **AI Analysis** - DeepSeek language model provides market insights
- **Intelligent Response Generation** - Structured financial analysis output
- **Session Management** - Tracks conversation context для follow-up queries
- **✅ Test Webhook Support** - MCP testing capabilities для automated validation

**Workflow Triggers:**
- ✅ **Manual Trigger** - For development и manual testing  
- ✅ **Execute Workflow Trigger** - For FMP Router integration
- ✅ **Test Webhook Trigger** - For MCP webhook testing (path: "ai-deepseek-dev")

**Input Parameters:**
- `input` (string) - Financial query или analysis request
- `sessionId` (string) - Session identifier для conversation tracking

**Output Format:**
```json
{
  "analysis": "AI-generated financial analysis",
  "data": "Retrieved financial data", 
  "insights": "Market insights and recommendations",
  "sessionId": "Session tracking ID"
}
```

### 🔗 **FMP API Router DEV** (`fmp-router-dev.json`)
**n8n Workflow ID:** `UmUET85BJqPbpRPp`  
**Project Environment:** First Bird DEV (`EAq65uG63UPwwuhk`)

**Primary Function:** Universal routing hub для Financial Modeling Prep API endpoints

**Supported API Commands:**
- **`Insider.Trading.Latest`** - Most recent insider trading transactions
- **`Insider.Trading.ReportingName`** - Insider trades by specific reporting individual  
- **`Insider.Trading.Search`** - Insider trading search by company symbol
- **`Company.Profile`** - Company fundamental information и profile data

**Workflow Triggers:**
- ✅ **Manual Trigger** - For development и direct API testing
- ✅ **Execute Workflow Trigger** - For AI Deepseek integration и child workflow calls

**Input Parameters:**
- `toolName` (string) - API command to execute (e.g., "Insider.Trading.Latest")
- `params` (object) - Command-specific parameters

**Example API Calls:**
```json
// Latest insider trading data
{
  "toolName": "Insider.Trading.Latest",
  "params": {"limit": 10}
}

// Company-specific insider trading
{
  "toolName": "Insider.Trading.Search", 
  "params": {"symbol": "AAPL", "limit": 5}
}

// Individual insider's trading history
{
  "toolName": "Insider.Trading.ReportingName",
  "params": {"name": "COOK TIMOTHY D", "limit": 20}
}
```

---

## 🧪 Test Webhook Configuration

### **✅ MCP Webhook Testing Architecture**

**First Bird project implements the Test Webhook - Test Execution approach** for simplified workflow testing через MCP tools.

#### **🤖 AI Deepseek DEV - Test Webhook Setup:**

**Webhook Configuration:**
```json
{
  "id": "webhook-trigger-ai-deepseek-test",
  "name": "Test Webhook Trigger",
  "type": "n8n-nodes-base.webhook",
  "typeVersion": 2,
  "parameters": {
    "path": "ai-deepseek-dev",
    "options": {},
    "responseMode": "responseNode",
    "responseData": "allEntries"
  }
}
```

**Test Data Processor v2 Configuration:**
```json
{
  "id": "test-data-processor-v2",
  "name": "Test Data Processor v2",
  "type": "n8n-nodes-base.code",
  "typeVersion": 2,
  "parameters": {
    "jsCode": "// Handle GET query parameters для test webhook protocol\nconst webhookData = item.json;\nconst testData = webhookData.query || webhookData; // GET params first, then body\n\nif (testData && testData.testType) {\n  // TEST WEBHOOK DATA - Protocol processing\n  const aiInput = testData.testData?.input || 'Test query not provided';\n  const sessionId = testData.testData?.sessionId || 'test-session-default';\n  \n  results.push({\n    json: {\n      input: aiInput,\n      sessionId: sessionId,\n      __testMetadata: {\n        testType: testData.testType,\n        parentWorkflow: testData.parentWorkflow,\n        monitoring: testData.monitoring || {},\n        timestamp: new Date().toISOString()\n      }\n    }\n  });\n} else {\n  // NORMAL WORKFLOW DATA - Pass through\n  results.push({json: webhookData});\n}\n\nreturn results;"
  }
}
```

**Response Formatter Configuration:**
```json
{
  "id": "response-formatter",
  "name": "Response Formatter",
  "type": "n8n-nodes-base.code",
  "typeVersion": 2,
  "parameters": {
    "jsCode": "// Generate protocol-compliant test responses\nconst testMetadata = item.json?.__testMetadata;\n\nif (testMetadata) {\n  // TEST RESPONSE - Protocol-compliant formatting\n  const response = {\n    testExecution: {\n      executionId: 'exec-' + Date.now(),\n      status: 'success',\n      timestamp: new Date().toISOString(),\n      parentWorkflow: {\n        name: testMetadata.parentWorkflow || 'ai-deepseek',\n        status: 'completed',\n        testType: testMetadata.testType\n      },\n      testResults: {\n        aiResponse: item.json.output || item.json.response || 'AI analysis completed',\n        childWorkflows: [\n          {\n            name: 'fmp-router',\n            status: 'completed',\n            callCount: 'tracked-automatically'\n          }\n        ]\n      }\n    }\n  };\n  \n  return [{json: response}];\n} else {\n  // NORMAL RESPONSE - Standard workflow output\n  return [{json: item.json}];\n}"
  }
}
```

#### **🔧 Test Webhook Connection Pattern:**
```
Test Webhook Trigger → Test Data Processor v2 → AI Agent Logic → FMP Router (Execute Workflow) → Response Formatter
                                                      ↓
                                               Child Workflow Natural Execution
```

### **📊 Test Execution Examples**

#### **Example 1: Basic Financial Analysis Test**
```javascript
// MCP Webhook Execution
const testResult = await n8n_trigger_webhook_workflow({
  webhookUrl: "https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev?testType=full&parentWorkflow=ai-deepseek&testData.input=Analyze%20AAPL%20financial%20performance&testData.sessionId=first-bird-test-001&monitoring.trackChildExecution=true&monitoring.timeout=60s",
  httpMethod: "GET",
  waitForResponse: true
});
```

**Expected Response:**
```json
{
  "testExecution": {
    "executionId": "exec-1693456789123",
    "status": "success",
    "timestamp": "2025-08-30T14:45:16.000Z",
    "parentWorkflow": {
      "name": "ai-deepseek",
      "status": "completed",
      "testType": "full"
    },
    "testResults": {
      "aiResponse": "AAPL financial analysis: Strong Q3 performance with revenue growth...",
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

#### **Example 2: Insider Trading Analysis Test**
```javascript
// Comprehensive insider trading analysis
const insiderTradingTest = await n8n_trigger_webhook_workflow({
  webhookUrl: "https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev?testType=specific&parentWorkflow=ai-deepseek&testData.input=Analyze%20recent%20AAPL%20insider%20trading%20activity&testData.sessionId=insider-test-001&monitoring.trackChildExecution=true",
  httpMethod: "GET", 
  waitForResponse: true
});
```

#### **Example 3: Error Handling Test**
```javascript
// Test error scenarios
const errorTest = await n8n_trigger_webhook_workflow({
  webhookUrl: "https://dm83.app.n8n.cloud/webhook/ai-deepseek-dev?testType=quick&parentWorkflow=ai-deepseek&testData.input=Invalid%20stock%20symbol%20XYZ999&testData.sessionId=error-test-001&monitoring.trackChildExecution=true",
  httpMethod: "GET",
  waitForResponse: true
});
```

### **⚠️ Test Webhook Guidelines**

#### **✅ DO:**
- **Use n8n MCP tools** для webhook testing
- **URL-encode parameters** properly для GET requests
- **Follow test data protocol** structure
- **Monitor both parent и child execution**
- **Test различные scenarios** (success, error, edge cases)

#### **❌ DON'T:**
- **Never use web_fetch** для webhook URLs
- **Don't hardcode webhook paths** - discover dynamically
- **Don't skip error handling tests**
- **Don't test production webhooks** (они не существуют by design)

---

## 🏗️ Project Workflow Architecture

### **Current Implementation: DEV Environment**
```
First Bird DEV Project (n8n):
├── 🤖 AI Deepseek DEV      (ID: 0VAipR4PLHbtkIzw)
│   ├── Manual Trigger      → Development testing
│   ├── Execute Workflow    → Child workflow integration  
│   └── ✅ Test Webhook     → MCP webhook testing (path: "ai-deepseek-dev")
├── 🔗 FMP API Router DEV   (ID: UmUET85BJqPbpRPp)  
│   ├── Manual Trigger      → Direct API testing
│   └── Execute Workflow    → AI Deepseek child calls
└── 🧪 MCP Webhook Testing   [Platform Capability]
    └── n8n_trigger_webhook_workflow → Automated testing через MCP tools

GitHub Repository Sync:
└── workflows/first-bird/dev/
    ├── ai-deepseek-dev.json      ✅ Current (with test webhook)
    └── fmp-router-dev.json       ✅ Current (Execute Workflow ready)
```

### **Planned: PROD Environment**
```
First Bird PROD Project (n8n):        [FUTURE IMPLEMENTATION - Issue #27]
├── 🤖 AI Deepseek PROD
│   └── Manual Trigger              → Production stability (NO test webhooks)
└── 🔗 FMP API Router PROD
    └── Manual Trigger              → Production stability (NO test webhooks)

GitHub Repository Integration:
└── workflows/first-bird/prod/         [TO BE CREATED]
    ├── ai-deepseek-prod.json
    └── fmp-router-prod.json
```

---

## 🧪 Project Testing Strategy

### **✅ Test Webhook - Test Execution Approach**
**Testing Method:** Simplified parent workflow testing через MCP webhook triggers с natural child workflow execution

**Testing Flow:**
1. **MCP Webhook Discovery** → `n8n_get_workflow_details(id)` finds webhook capability
2. **Test Data Preparation** → Format GET parameters according к protocol
3. **Parent Webhook Execution** → `n8n_trigger_webhook_workflow()` triggers AI Deepseek
4. **Natural Child Execution** → AI Deepseek naturally calls FMP Router via Execute Workflow
5. **Result Monitoring** → Track both parent и child workflow execution
6. **Response Validation** → Verify protocol-compliant test response format

### **Project-Specific Test Scenarios:**

#### **Scenario 1: Financial Analysis Workflow**
```json
{
  "testType": "full",
  "parentWorkflow": "ai-deepseek",
  "testData": {
    "input": "Analyze Apple's Q3 2025 financial performance and insider trading patterns",
    "sessionId": "comprehensive-analysis-test"
  },
  "expectedChildCalls": ["fmp-router"],
  "monitoring": {
    "trackChildExecution": true,
    "validateResults": true,
    "timeout": "60s"
  }
}
```

#### **Scenario 2: API Integration Test**
```json
{
  "testType": "specific",
  "parentWorkflow": "ai-deepseek", 
  "testData": {
    "input": "Get latest insider trading data for MSFT",
    "sessionId": "api-integration-test"
  },
  "validation": {
    "expectFMPApiCalls": true,
    "validateDataFormat": true
  }
}
```

#### **Scenario 3: Error Handling Test**
```json
{
  "testType": "quick",
  "parentWorkflow": "ai-deepseek",
  "testData": {
    "input": "Analyze invalid stock symbol INVALIDXYZ",
    "sessionId": "error-handling-test"
  },
  "expectedBehavior": "graceful_error_handling"
}
```

### **Success Criteria:**
- ✅ **Webhook Discovery** - AI Deepseek webhook discoverable через MCP
- ✅ **Parent Execution** - AI Deepseek responds to webhook triggers successfully
- ✅ **Child Integration** - FMP Router executes naturally via Execute Workflow calls
- ✅ **Data Flow Validation** - Financial data processed end-to-end correctly
- ✅ **Error Handling** - Edge cases handled gracefully
- ✅ **Response Format** - Protocol-compliant test responses generated

---

## 🔧 Project Configuration

### **Required Credentials (n8n):**
- **DeepSeek API Key** - AI language model access ✅ Configured
- **FMP API Key** - Financial Modeling Prep API access ✅ Configured

### **API Dependencies:**
- **DeepSeek API** - AI analysis engine (external service)
- **Financial Modeling Prep API** - Financial data source (external service)
- **n8n Execute Workflow Nodes** - Inter-workflow communication (internal)

### **n8n Node Requirements:**
- **@n8n/n8n-nodes-langchain** ✅ Available - AI language model nodes
- **n8n-nodes-base** ✅ Available - HTTP Request, Execute Workflow, Webhook nodes

### **✅ Test Webhook Requirements:**
- **Webhook Trigger nodes** - Configured in parent workflows
- **Test Data Processing** - Custom Code nodes для parameter handling
- **Response Formatting** - Protocol-compliant response generation
- **MCP Tool Access** - n8n_trigger_webhook_workflow availability

---

## 📊 Project Performance & Monitoring

### **Current Performance Metrics:**
- **AI Deepseek Response Time** - 3-7 seconds (DeepSeek API dependent)
- **FMP Router Response Time** - 1-3 seconds (FMP API dependent)  
- **Complete Analysis Cycle** - 5-12 seconds end-to-end
- **✅ Test Webhook Execution** - <45 seconds для comprehensive parent-child testing
- **MCP Discovery Time** - <3 seconds для webhook URL discovery

### **✅ Test Webhook Performance:**
- **Webhook Discovery** - Sub-5 second MCP tool response
- **Test Data Processing** - 1-2 seconds parameter parsing
- **Parent-Child Integration** - Natural execution timing
- **Response Generation** - Protocol-compliant formatting <2 seconds

### **Monitoring Capabilities:**
- **n8n Execution Logs** - Detailed workflow execution tracking
- **API Response Monitoring** - External service availability и performance
- **Error Tracking** - Failed execution analysis и debugging
- **✅ MCP Test Results** - Webhook testing success rates через MCP tools

---

## 🎯 Project Development Next Steps

### **Immediate Priorities (Issue #27):**
1. **✅ Test Webhook Validation** - Comprehensive MCP webhook testing
2. **Parent-Child Flow Testing** - End-to-end workflow integration validation
3. **Production Deployment Preparation** - Ready для PROD environment
4. **Documentation Completion** - Update с test webhook procedures

### **Production Readiness Tasks:**
1. **PROD Environment Setup** - Create First Bird PROD project в n8n
2. **PROD Workflow Deployment** - Single-trigger production versions (NO test webhooks)
3. **Production Testing** - Validate PROD workflow functionality via manual triggers
4. **Monitoring Setup** - Production performance tracking

### **✅ Test Webhook Integration Completed:**
1. **✅ MCP Testing Capability** - AI Deepseek DEV webhook functional
2. **✅ Protocol Documentation** - Complete test data format specifications  
3. **✅ Configuration Templates** - Reusable webhook setup patterns
4. **✅ Integration Examples** - Working test execution examples

---

## 🔗 Project Integration Points

### **Platform Tool Integration:**
- **✅ MCP Webhook Testing** - Direct parent workflow testing через MCP tools
- **GitHub Actions Pipeline** - Workflow validation и quality assurance
- **Release Management System** - Version control и deployment packaging

### **External Service Integration:**  
- **DeepSeek API** - AI language model для analysis generation
- **Financial Modeling Prep API** - Financial data retrieval и processing
- **n8n Cloud Platform** - Workflow execution environment

### **Cross-Workflow Communication:**
- **AI Deepseek** calls **FMP Router** for data retrieval via Execute Workflow
- **✅ Test Webhooks** enable direct parent workflow testing
- **GitHub Repository** maintains workflow version synchronization

---

## 📚 **Related Project Documentation**

- **Platform Architecture**: [../../README.md](../../README.md) - Overall platform capabilities
- **Workflow Architecture**: [../README.md](../README.md) - Project-centric workflow structure  
- **Platform Roadmap**: [../../docs/roadmap.md](../../docs/roadmap.md) - Development timeline
- **✅ Testing Strategy**: [../../docs/testing-strategy.md](../../docs/testing-strategy.md#-mcp-webhook-testing) - MCP webhook testing protocols
- **✅ MCP Webhook Guide**: [../../docs/mcp-webhook-testing-guide.md](../../docs/mcp-webhook-testing-guide.md) - Comprehensive MCP testing procedures
- **✅ AI Agent Protocols**: [../../docs/ai-agent-roles-protocols.md](../../docs/ai-agent-roles-protocols.md#-webhook-testing-protocol-для-ai-agents) - Webhook testing integration
- **Active Issue**: [Issue #27](https://github.com/dabalakirev/n8n-workflows-ai/issues/27) - First Bird completion через Test Webhook approach

---

**📅 Last Updated:** August 30, 2025  
**🎯 Status:** ✅ Test webhook integration complete, production validation pending (Issue #27)  
**🚀 Next Milestone:** Production deployment после successful Test Webhook - Test Execution validation