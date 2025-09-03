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

## 🚨 **CRITICAL: Manual Activation Required**

**MCP CANNOT activate workflows** - human must activate in n8n UI after creation

**Process:**
1. **Create workflow via MCP** ✅
2. **Configure webhook node via MCP** ✅  
3. **ACTIVATE workflow manually** ⚠️ - **HUMAN REQUIRED**
4. **Test via MCP** ✅

**Without manual activation:** Webhook returns 404 "not registered" error

---

## 🚨 **CRITICAL: webhookId Field Requirement**

**⚠️ MANDATORY WEBHOOK CONFIGURATION - MOST CRITICAL REQUIREMENT**

**ALL webhook nodes MUST include `webhookId` field for n8n Cloud registration:**

### ✅ **CORRECT Webhook Node Configuration:**
```javascript
{
  "id": "webhook-node-id",
  "name": "Webhook Node", 
  "type": "n8n-nodes-base.webhook",
  "parameters": {
    "path": "webhook-path",
    "httpMethod": "GET",
    "responseMode": "responseNode"
  },
  "typeVersion": 2,
  "webhookId": "unique-webhook-identifier"  // ⭐ CRITICAL FIELD!
}
```

### ❌ **INCORRECT Configuration (CAUSES 404 ERRORS):**
```javascript
{
  "id": "webhook-node-id", 
  "name": "Webhook Node",
  "type": "n8n-nodes-base.webhook",
  "parameters": {
    "path": "webhook-path", 
    "httpMethod": "GET",
    "responseMode": "responseNode"
  },
  "typeVersion": 2
  // ❌ MISSING: "webhookId" field - webhook will NOT register!
}
```

**🔑 KEY RULES:**
- **webhookId MUST be unique** across all workflows
- **webhookId format:** alphanumeric + hyphens (e.g., "my-webhook-id-001")
- **Missing webhookId** = guaranteed 404 "not registered" error
- **Required for n8n Cloud** - self-hosted may not require

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
- **Use Code node with responseNode mode** → "No Respond to Webhook node" error
- **CONTINUE development without successful webhook testing** ⚠️
- **Omit webhookId field** → 404 "not registered" error ⚠️

**✅ ONLY METHOD:**
- Use `n8n_trigger_webhook_workflow()` MCP tool
- Use `n8n-nodes-base.respondToWebhook` node for responses
- **Always include webhookId field** в webhook nodes

## ⚡ 4-Step Testing Process

### 1. Create & Configure (WITH webhookId!)
```javascript
const workflow = await n8n_create_workflow({
  nodes: [{
    type: "n8n-nodes-base.webhook",
    parameters: {path: "test-webhook", httpMethod: "GET", responseMode: "responseNode"},
    webhookId: "test-webhook-unique-id"  // ⭐ CRITICAL FIELD!
  }, {
    type: "n8n-nodes-base.respondToWebhook", // ✅ CORRECT node type
    parameters: {respondWith: "json", responseBody: "{\"status\": \"success\"}"}
  }],
  connections: {"Test Webhook": {"main": [[{"node": "Respond to Webhook"}]]}}
});
```

### 2. Manual Activation (HUMAN REQUIRED)
**MCP cannot activate - human must activate in n8n UI**

### 3. Execute & Test
```javascript
const result = await n8n_trigger_webhook_workflow({
  webhookUrl: `https://dm83.app.n8n.cloud/webhook/${workflow.webhookPath}`,
  httpMethod: "GET",
  waitForResponse: true
});
```

### 4. Validate Response
```javascript
if (result.status === 200) {
  console.log("✅ Webhook test successful");
} else {
  throw new Error("🛑 HALT development - webhook test failed");
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
- ✅ Manual activation completed
- ✅ **webhookId field added** to all webhook nodes
- ✅ MCP webhook testing successful  
- ✅ 200 OK response received

## 📋 Required Parameters

| Parameter | Value | Purpose |
|-----------|-------|---------|
| `testType` | "full" | Test scope |
| `testData.input` | URL-encoded | Test input |
| `testData.sessionId` | unique ID | Session tracking |

## 🎯 Success Response Format
```json
{
  "status": 200,
  "data": {
    "message": "Webhook test successful",
    "testStatus": "PASS"
  }
}
```

## 🚨 Error Troubleshooting

| Error | Cause | Fix | Development Impact |
|-------|-------|-----|-------------------|
| 403 Forbidden | Used `web_fetch` | Use `n8n_trigger_webhook_workflow` | Continue after fix |
| 404 Not Found | Workflow not activated | **Manual activation required** | **HALT development** ⚠️ |
| 404 "not registered" | **Missing webhookId field** | **Add webhookId to webhook node** | **HALT development** ⚠️ |
| "No Respond to Webhook node" | Used Code node with responseNode mode | Use `respondToWebhook` node | **HALT development** ⚠️ |
| SERVER_ERROR | Workflow execution error | Debug with `n8n_get_execution` | **HALT development** ⚠️ |
| Malformed URL | No encoding | Use `URLSearchParams` | Continue after fix |
| Webhook not registered | Infrastructure issue | **INVESTIGATE n8n instance** | **HALT development** ⚠️ |

## 📝 Complete Working Example (WITH webhookId!)

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
  
  // 3. Execute (requires manual activation first!)
  const result = await n8n_trigger_webhook_workflow({
    webhookUrl: `${baseUrl}?${params.toString()}`,
    httpMethod: "GET", 
    waitForResponse: true
  });
  
  // 4. Validate + Development Gate
  if (result.status === 404) {
    if (result.data.message.includes("not registered")) {
      throw new Error("🛑 DEVELOPMENT GATE: Missing webhookId field in webhook node configuration");
    }
    throw new Error("🛑 DEVELOPMENT GATE: Manual activation required");
  }
  
  if (result.status === 200) {
    console.log("✅ Test passed - development may continue");
    return result;
  } else {
    throw new Error(`🛑 DEVELOPMENT GATE: Webhook test failed - ${result.error}`);
  }
}
```

## 💡 **Working vs Failed Configuration Comparison**

### ✅ **WORKING Configuration Example:**
```javascript
// Proven working webhook from successful workflow
{
  "id": "webhook-test",
  "name": "Test Webhook", 
  "type": "n8n-nodes-base.webhook",
  "parameters": {
    "path": "webhook-test-minimal",
    "httpMethod": "GET", 
    "responseMode": "responseNode"
  },
  "typeVersion": 2,
  "webhookId": "test-webhook-id-123"  // ✅ SUCCESS FACTOR!
}
```

### ❌ **FAILED Configuration Example:**
```javascript
// Configuration that caused 404 "not registered" errors
{
  "id": "test-webhook",
  "name": "Test Webhook",
  "type": "n8n-nodes-base.webhook", 
  "parameters": {
    "path": "insider-trades-test",
    "httpMethod": "GET",
    "responseMode": "responseNode"
  },
  "typeVersion": 2
  // ❌ MISSING: "webhookId" field - GUARANTEED FAILURE!
}
```

**Result:** Working webhook returns 200 OK, failed webhook returns 404 "not registered"

---

**Critical Protocol:** Webhook testing success is **mandatory gate** for all workflow development. Manual activation + **webhookId field** required.

**Usage:** Create workflow (WITH webhookId!) → Human activates → `await testWebhook("workflow-id", "test input")`