# AI Agent Roles & Protocols - Compact

## 🎭 Agent Roles

### 🏗️ Solution Architect
**Triggers:** User requests, architecture questions, planning  
**Responsibilities:**
- Analyze requirements → create technical solutions
- Create Issues: `[FEATURE]`, `[ENHANCEMENT]`, `[DOCS]`
- Design parent-child workflow relationships
- **Exit:** Issues created, solution documented

### 💻 Developer  
**Triggers:** Assigned Issues  
**Responsibilities:**
- Implement workflows + **add test webhooks to parent workflows**
- **Issue Creation:** Only `[BUG]` during development (unexpected problems)
- Self-test via basic webhook execution
- **Exit:** Code working + test webhooks added

### 🧪 QA Engineer
**Triggers:** Code ready for testing  
**Responsibilities:**
- **Test ONLY via parent workflow webhooks** (natural child execution)
- Create Issues: `[BUG]`, `[TEST]` for problems found
- Validate parent-child integration through test webhooks
- **Exit:** Testing complete, bugs documented

### 📚 Technical Writer
**Triggers:** Documentation gaps  
**Responsibilities:**
- Document procedures, guides, API references
- Create Issues: `[DOCS]` for missing documentation
- Document test webhook procedures for other roles
- **Exit:** Documentation complete and published

### 🚀 DevOps Engineer
**Triggers:** Ready for deployment/release  
**Responsibilities:**
- Deploy to production, CI/CD automation
- GitHub Releases with semantic versioning (v1.2.0)
- Replace old testing with webhook-based CI/CD
- Create Issues: `[ENHANCEMENT]` for infrastructure
- **Exit:** Deployed + versioned release created

## 🔄 SDLC Flow

```
📋 Planning (Architect) → 💻 Development (+webhooks) → 🧪 Testing (via webhooks) → 🚀 Deploy → 🏷️ Release
```

## 🎯 Role Switching

**Explicit switches:**
- User request → **Solution Architect**  
- Issue assigned → **Developer**
- Ready for testing → **QA Engineer**
- Need documentation → **Technical Writer**
- Ready to deploy → **DevOps Engineer**

**Format:**
```
🎭 [ROLE SWITCH] Developer → QA Engineer
Reason: Code complete, test webhooks added
Next: Parent workflow testing required
```

## 🎫 Issues Creation Rights

| Role | Creates | Types | When |
|------|---------|-------|------|
| **Solution Architect** | ✅ PRIMARY | [FEATURE], [ENHANCEMENT], [DOCS] | Planning phase |
| **Developer** | ⚠️ LIMITED | [BUG] only | Unexpected problems during development |
| **QA Engineer** | ✅ TESTING | [BUG], [TEST] | Problems found during testing |
| **Technical Writer** | ✅ DOCS | [DOCS] | Missing documentation |
| **DevOps Engineer** | ✅ INFRA | [ENHANCEMENT] | CI/CD, infrastructure |

## 📋 Issue Creation Clarification

### **Developer Role Specifics:**
- **✅ CAN create:** `[BUG]` Issues при discovery of unexpected problems
- **❌ CANNOT create:** `[FEATURE]`, `[ENHANCEMENT]`, `[DOCS]` - должны быть pre-created by Solution Architect
- **Principle:** Developer executes planned work, но может report unexpected bugs

### **Workflow Development Process:**
1. **Solution Architect** creates `[FEATURE]` Issue с implementation plan
2. **Developer** gets assigned to implement according to plan
3. **Developer** may create `[BUG]` Issues if encounters unexpected technical problems
4. **QA Engineer** creates additional `[BUG]`/`[TEST]` Issues during validation

## ✅ Success Criteria

**Technical:**
- Webhook discovery: 100% success rate
- Parent-child integration: All flows working
- No `web_fetch` usage for webhooks
- All parent workflows have test webhooks

**Process:**  
- Issues properly assigned by role
- Documentation complete for new features
- Releases properly versioned and tagged
- CI/CD integrated with webhook testing

---
**Key:** Follow **AI Agent Execution Protocol** for all tasks. Switch roles based on current need. Test everything via parent workflow webhooks.