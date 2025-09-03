# MCP Webhook Testing Guide - Compact

## 🚨 **CRITICAL CI/CD RULE - NO EXCEPTIONS**

### ⚠️ **MANDATORY WEBHOOK TESTING GATE**

**🛑 NEVER CONTINUE development if webhook testing FAILS**

**Policy:**
- ✅ **Webhook test PASS** → continue development  
- ❌ **Webhook test FAIL** → **HALT all development activities**
- 🚫 **No workarounds** - no alternative validation methods
- 🚫 **No "temporary skips"** - webhook testing is mandatory gate

**Protocol Violation Consequences:**
- **Immediate rollback** of all development work
- **Delete workflows** created without webhook validation  
- **Remove documentation** of unsuccessful implementations
- **Block Issue progression** until webhook testing resolved

**Enforcement:** This rule applies to ALL workflow development - no exceptions for "simple" workflows or "quick fixes".

---

## 🏗️ Webhook Architecture

**Test Webhook** = узел внутри Parent Workflow (НЕ отдельный workflow)
- Parent содержит Webhook узел + основную логику  
- Child workflows выполняются естественно от Parent

## 🚨 Critical Rules

**❌ NEVER DO:**
- Use `web_fetch` for webhooks → 403 Forbidden
- Hardcode URLs → Use dynamic discovery
- Skip URL encoding → Use `URLSearchParams`
- **CONTINUE development without successful webhook testing** ⚠️ **NEW**

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

// ⚠️ NEW: If webhook testing fails - HALT development
if (result.status === 404 || result.data?.code === 404) {
  throw new Error("CRITICAL: Webhook testing failed - development must be halted");
}
```

## 🚫 **Development Gate Enforcement**

### **If Webhook Testing Fails:**
1. **IMMEDIATE HALT** - stop all development activities
2. **ROLLBACK CHANGES** - delete unsuccessful workflows  
3. **REMOVE ARTIFACTS** - delete implementation logs/documentation
4. **UPDATE ISSUE** - mark as blocked by webhook testing failure
5. **INVESTIGATE ROOT CAUSE** - resolve webhook infrastructure before continuing

### **No Development Activities Until:**
- ✅ Webhook registration working
- ✅ MCP webhook testing successful  
- ✅ Complete 3-step testing process validated

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

| Error | Cause | Fix | Development Impact |
|-------|-------|-----|-------------------|
| 403 Forbidden | Used `web_fetch` | Use `n8n_trigger_webhook_workflow` | Continue after fix |
| 404 Not Found | Wrong URL | Check `workflow.webhookPath` | **HALT development** ⚠️ |
| Malformed URL | No encoding | Use `URLSearchParams` | Continue after fix |
| No test data | Missing params | Add required parameters | Continue after fix |
| Webhook not registered | Infrastructure issue | **INVESTIGATE n8n instance** | **HALT development** ⚠️ |

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
  
  // 4. Validate + Development Gate
  if (result.status === 404 || result.data?.code === 404) {
    throw new Error("🛑 DEVELOPMENT GATE: Webhook testing failed - must halt all development");
  }
  
  if (result.testExecution?.status === "success") {
    console.log("✅ Test passed - development may continue");
    return result;
  } else {
    throw new Error(`❌ Test failed: ${result.testExecution?.error?.message}`);
  }
}
```

---

**Critical Protocol:** Webhook testing success is **mandatory gate** for all workflow development. No exceptions.

**Usage:** `await testWebhook("workflow-id", "Your test input")`