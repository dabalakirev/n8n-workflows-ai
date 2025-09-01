# MCP Webhook Testing Guide - Compact

## 🏗️ Webhook Architecture

**Test Webhook** = узел внутри Parent Workflow (НЕ отдельный workflow)
- Parent содержит Webhook узел + основную логику  
- Child workflows выполняются естественно от Parent

## 🚨 Critical Rules

**❌ NEVER DO:**
- Use `web_fetch` for webhooks → 403 Forbidden
- Hardcode URLs → Use dynamic discovery
- Skip URL encoding → Use `URLSearchParams`

**✅ ONLY METHOD:**
- Use `n8n_trigger_webhook_workflow()` MCP tool

## ⚡ 3-Step Testing Process

### 1. Discovery
```javascript
const workflow = await n8n_get_workflow_details({id: "workflow-id"});
if (!workflow.hasWebhookTrigger) throw new Error("No webhook");
const url = `https://dm83.app.n8n.cloud/webhook/${workflow.webhookPath}`;
```

### 2. Execute
```javascript
// GET with parameters
const params = new URLSearchParams({
  testType: "full",
  "testData.input": testInput,
  "testData.sessionId": `test-${Date.now()}`
});

const result = await n8n_trigger_webhook_workflow({
  webhookUrl: `${url}?${params.toString()}`,
  httpMethod: "GET",
  waitForResponse: true
});
```

### 3. Validate
```javascript
if (result.testExecution?.status !== "success") {
  throw new Error(`Test failed: ${result.testExecution?.error?.message}`);
}
```

## 📋 Required Parameters

| Parameter | Value | Purpose |
|-----------|-------|---------|
| `testType` | "full" | Test scope |
| `testData.input` | URL-encoded | Test input |
| `testData.sessionId` | unique ID | Session tracking |

## 🎯 Success Response Format
```json
{
  "testExecution": {
    "status": "success",
    "executionId": "exec-123",
    "testResults": {
      "aiResponse": "...",
      "childWorkflows": [{"name": "...", "status": "completed"}]
    }
  }
}
```

## 🚨 Error Troubleshooting

| Error | Cause | Fix |
|-------|-------|-----|
| 403 Forbidden | Used `web_fetch` | Use `n8n_trigger_webhook_workflow` |
| 404 Not Found | Wrong URL | Check `workflow.webhookPath` |
| Malformed URL | No encoding | Use `URLSearchParams` |
| No test data | Missing params | Add required parameters |

## 📝 Complete Working Example

```javascript
async function testWebhook(workflowId, testInput) {
  // 1. Get webhook URL
  const workflow = await n8n_get_workflow_details({id: workflowId});
  if (!workflow.hasWebhookTrigger) throw new Error("No webhook support");
  
  // 2. Build request
  const baseUrl = `https://dm83.app.n8n.cloud/webhook/${workflow.webhookPath}`;
  const params = new URLSearchParams({
    testType: "full",
    parentWorkflow: workflow.name,
    "testData.input": testInput,
    "testData.sessionId": `test-${Date.now()}`
  });
  
  // 3. Execute
  const result = await n8n_trigger_webhook_workflow({
    webhookUrl: `${baseUrl}?${params.toString()}`,
    httpMethod: "GET", 
    waitForResponse: true
  });
  
  // 4. Validate
  if (result.testExecution?.status === "success") {
    console.log("✅ Test passed");
    return result;
  } else {
    throw new Error(`❌ Test failed: ${result.testExecution?.error?.message}`);
  }
}
```

---
**Usage:** `await testWebhook("workflow-id", "Your test input")`