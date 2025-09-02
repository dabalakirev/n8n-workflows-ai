# Incremental Testing Protocol - Compact

## 🎯 Principle: "Build Small, Test Often"

**Prevent complex debugging** через progressive node-by-node development с immediate validation.

## 🔄 Development Flow

### **1-3 Node Iterations:**
```
Plan (1-3 nodes) → Build → Test via Webhook → Validate → Extend → Repeat
```

### **Mandatory Steps:**
1. **Plan** maximum 1-3 nodes для next increment
2. **Build** nodes с basic configuration  
3. **Test** via parent workflow webhook
4. **Validate** results и data flow correctness
5. **Extend** с next 1-3 nodes only after validation passes

## 🧪 Test Integration

### **Use Existing Test Webhook Strategy:**
- **Parent workflow webhook** supports partial execution testing
- **Test parameters** structure для incremental scenarios:
  ```
  testType=incremental&increment=1&testData.nodeGroup=auth-nodes
  ```
- **Progressive validation** through webhook responses

### **MCP Tools Integration:**
- Use `n8n_trigger_webhook_workflow()` для each increment
- **URL encoding** for increment-specific test data
- **Response validation** для each development iteration

## ✅ Success Criteria

### **Per Increment:**
- ✅ **Nodes execute successfully** без errors
- ✅ **Data flow validated** между nodes в increment  
- ✅ **Expected output format** matches requirements
- ✅ **Integration points work** с existing workflow parts

### **Failure Actions:**
- ❌ **Don't extend** until current increment passes
- 🔧 **Debug small scope** (1-3 nodes only)  
- ⚡ **Fast iteration** on small increment
- ✅ **Validate fix** before proceeding

## 🛠️ Implementation Pattern

### **Typical Workflow Development:**
```
Increment 1: Trigger + Basic Logic (1-3 nodes) → Test → Validate
Increment 2: API Call + Response Processing (1-3 nodes) → Test → Validate  
Increment 3: Data Transformation + Validation (1-3 nodes) → Test → Validate
Increment 4: Output + Error Handling (1-3 nodes) → Test → Validate
```

### **Testing Each Increment:**
- **Webhook URL:** Parent workflow с test trigger
- **Test Data:** Increment-specific validation data
- **Validation:** Check increment output + integration points
- **Continue:** Only after successful validation

## 🚨 Anti-Patterns

### **❌ Don't Do:**
- Build 10+ nodes без intermediate testing
- Skip validation because "it looks right"
- Test только final complete workflow
- Debug complex multi-node scenarios

### **✅ Always Do:**
- Maximum 1-3 nodes per iteration
- Test via parent workflow webhook после each increment
- Validate data flow и node interactions
- Fix issues в small scope before extending

## 🔗 Integration

**Related Protocols:**
- **[Testing Strategy](testing-strategy.md)** - Complete workflow testing
- **[MCP Webhook Testing Guide](mcp-webhook-testing-guide.md)** - Technical implementation
- **[AI Agent Execution Protocol](ai-agent-execution-protocol.md)** - Development process integration

**Tools Required:**
- Parent workflow с Test Webhook trigger
- MCP webhook testing tools
- Progressive test data structures

---

**Key Principle:** Catch issues early в small scope rather than debug complex workflows later.