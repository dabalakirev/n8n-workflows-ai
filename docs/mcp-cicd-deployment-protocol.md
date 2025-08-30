# MCP CI/CD Deployment Protocol - Compact

## 🎯 Purpose
Complete CI/CD process for n8n workflow development using MCP-first approach with role-based responsibilities.

---

## 🏗️ **Phase 1: Architecture Design**
### **🎭 Role:** 🏗️ Solution Architect

**Trigger:** New requirements, architecture changes

#### **Required Actions (Sequential):**
1. **Requirements Analysis** - Analyze user requirements and constraints
2. **Technical Planning** - Design workflow architecture and MCP approach  
3. **MCP Assessment** - Review `n8n_create_workflow`, `n8n_update_full_workflow`, identify UI needs
4. **Issues Creation** - Create [FEATURE]/[ENHANCEMENT] Issues with success criteria

#### **Architecture Review Protocol:**
```
Developer Escalation: "❌ Architecture Insufficient - [Problem]"
→ Solution Architect Review → Update → Continue Development
```

**✅ Exit Criteria:** Issues created, architecture documented, MCP approach defined

---

## 💻 **Phase 2: MCP-First Development** 
### **🎭 Role:** 💻 Developer

**Trigger:** Issue assigned, architecture approved

#### **Required Actions (Sequential):**
1. **Current State Analysis**
   ```bash
   n8n_list_workflows → identify existing
   n8n_get_workflow_details(id) → examine structure
   ```

2. **MCP Implementation**
   ```bash
   n8n_create_workflow({name, nodes, connections})
   # OR
   n8n_update_full_workflow(id, {nodes, connections})
   ```

3. **DEV Triggers Setup** - **CRITICAL**: Dual triggers required
   ```javascript
   const devNodes = [
     {id: "manual-trigger", type: "n8n-nodes-base.manualTrigger"},
     {id: "execute-workflow-trigger", type: "n8n-nodes-base.executeWorkflowTrigger"}
   ]
   ```

4. **GitHub Sync**
   ```bash
   github-mcp:create_or_update_file({
     path: "workflows/project/dev/workflow-dev.json",
     content: workflowJSON
   })
   ```

#### **🚨 UI Escalation Protocol:**
When MCP cannot perform operation:
1. Document limitation
2. Create detailed instructions: "🔴 MANUAL UI ACTION REQUIRED - Issue #N"  
3. Add label "🔴 manual-ui-required"
4. Wait for confirmation, then continue

**✅ Exit Criteria:** Workflow implemented, dual triggers configured, GitHub synced

---

## 🧪 **Phase 3: MCP-Based Testing**
### **🎭 Role:** 🧪 QA Engineer

**Trigger:** Development completed

#### **Required Actions (Sequential):**
1. **Test Execution**
   ```bash
   n8n_trigger_webhook_workflow({
     webhookUrl: "/webhook/test-orchestrator",
     data: {
       testSuite: "full",
       workflows: ["target-workflow"],
       testData: {...}
     }
   })
   ```

2. **Results Analysis**
   ```bash
   n8n_get_execution(executionId) → analyze results
   n8n_list_executions(workflowId) → check history
   ```

3. **Bug Reporting** (if issues found)
   ```bash
   github-mcp:create_issue({
     title: "[BUG] Description",
     labels: ["🐛 bug", "🧪 testing"]
   })
   ```

#### **Testing Success Criteria:**
- [ ] Functionality Tests: 100% pass rate
- [ ] Performance Tests: Within limits
- [ ] Error Handling: Validated
- [ ] Integration: Cross-workflow verified

**✅ Exit Criteria:** All tests passed, no critical bugs, quality sign-off provided

---

## 🚀 **Phase 4: Production Deployment**
### **🎭 Role:** 🚀 DevOps Engineer

**Trigger:** Testing completed successfully

#### **Required Actions (Sequential):**
1. **Pre-Deployment Validation**
   ```bash
   n8n_validate_workflow(devWorkflowId)
   n8n_list_executions(devWorkflowId, {status: "success"})
   ```

2. **PROD Workflow Creation** - **CRITICAL**: Single trigger only
   ```bash
   const prodConfig = {
     ...devConfig,
     name: name.replace("-dev", "-prod"),
     nodes: devConfig.nodes.filter(node => 
       node.type !== "n8n-nodes-base.executeWorkflowTrigger"
     ) // Remove Execute Workflow trigger - MANUAL ONLY
   }
   n8n_create_workflow(prodConfig)
   ```

3. **Production Validation**
   ```bash
   n8n_get_workflow_details(prodId) → confirm single manual trigger
   n8n_validate_workflow(prodId)
   ```

4. **GitHub PROD Sync**
   ```bash
   github-mcp:create_or_update_file({
     path: "workflows/project/prod/workflow-prod.json",
     content: prodJSON
   })
   ```

**🔒 Production Security:** Single manual trigger only, separate credentials, limited access

**✅ Exit Criteria:** PROD workflow created, single trigger confirmed, GitHub synced

---

## 🏷️ **Phase 5: Release Management**
### **🎭 Role:** 🚀 DevOps Engineer (Release Mode)

**Trigger:** Production deployment successful

#### **Required Actions (Sequential):**
1. **Release Preparation**
   ```bash
   github-mcp:list_issues({state: "closed", milestone: "v1.3.0"})
   ```

2. **Semantic Versioning**
   ```bash
   next_version = calculate_semantic_version(current, changes)
   ```

3. **GitHub Release Creation**
   ```bash
   github-mcp:create_release({
     tag_name: next_version,
     name: `${version} - Release Name`,
     body: generate_release_notes()
   })
   ```

4. **Release Announcement**
   ```bash
   github-mcp:create_issue({
     title: `🎉 Release ${version}`,
     labels: ["🎉 release", "📢 announcement"]
   })
   ```

**✅ Exit Criteria:** Release created, tags applied, artifacts uploaded, announcement published

---

## 📚 **Phase 6: Documentation**
### **🎭 Role:** 📚 Technical Writer

**Trigger:** Throughout all phases, final updates after release

#### **Required Actions:**
1. **Workflow Documentation**
   ```bash
   github-mcp:create_or_update_file({
     path: "workflows/project/README.md",
     content: updated_docs
   })
   ```

2. **Integration Updates** - API reference, configuration guides, troubleshooting
3. **Cross-Reference Management** - Update navigation and links

**✅ Exit Criteria:** All documentation updated, cross-references validated

---

## 🔄 **Critical Protocols**

### **Role Switching Format:**
```
🎭 [ROLE SWITCH] Current → Next
Reason: Phase completed/Issue status
Context: Specific project details
```

### **Escalation Triggers:**
- **Architecture Review:** Developer comments "❌ Architecture Insufficient"
- **UI Action:** MCP limitation requires manual intervention
- **Quality Gate:** Automated validation failures

### **Quality Gates (Must Pass):**
- JSON Schema Validation (automated)
- Test Orchestrator Validation (comprehensive)  
- Architecture Review (manual)
- Security Review (production)

---

## 📋 **Phase Checklist Summary**

| Phase | Role | Key Actions | Exit Criteria |
|-------|------|-------------|---------------|
| **1. Architecture** | 🏗️ Architect | Requirements → Planning → Assessment → Issues | Issues created, documented |
| **2. Development** | 💻 Developer | Analysis → Implementation → Triggers → Sync | Dual triggers, GitHub synced |
| **3. Testing** | 🧪 QA Engineer | Execute → Analyze → Report | Tests passed, quality sign-off |
| **4. Deployment** | 🚀 DevOps | Validate → Create PROD → Confirm → Sync | Single trigger, PROD ready |
| **5. Release** | 🚀 DevOps | Prepare → Version → Create → Announce | Release published |
| **6. Documentation** | 📚 Technical Writer | Update docs → References → Validate | Documentation current |

---

## 🚨 **Critical Success Requirements**

1. **Follow Sequential Order** - Complete each phase before next
2. **DEV = Dual Triggers** - Manual + Execute Workflow (for testing)  
3. **PROD = Single Trigger** - Manual only (security requirement)
4. **MCP First** - Use MCP commands, escalate to UI only when necessary
5. **GitHub Sync** - Always sync workflow JSON to repository
6. **Quality Gates** - All validations must pass before next phase
7. **Role Switching** - Declare switches with context
8. **Documentation** - Update throughout, finalize after release

**🎯 Success Metric:** Complete CI/CD cycle from requirements to production deployment with professional release management.

*This protocol ensures systematic workflow development with proper role separation, MCP automation, and production-ready deployments.*