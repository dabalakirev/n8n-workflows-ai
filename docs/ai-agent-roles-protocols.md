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
- **NEVER creates Issues** - works on assigned only
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
| **Developer** | ❌ NO | - | Works assigned only |
| **QA Engineer** | ✅ BUGS | [BUG], [TEST] | Problems found |
| **Technical Writer** | ✅ DOCS | [DOCS] | Missing docs |
| **DevOps Engineer** | ✅ INFRA | [ENHANCEMENT] | CI/CD, releases |

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