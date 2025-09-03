# Simplified MCP CI/CD Protocol

## ⚠️ ОБЯЗАТЕЛЬНЫЙ ПРОТОКОЛ
Упрощенный CI/CD процесс для n8n workflow разработки с unified Developer-Tester ролью и incremental подходом.

## 🎯 Цель
Streamlined разработка n8n workflows через MCP с built-in testing и architecture validation.

---

## 📚 Documentation Dependencies

### **🔧 ОБЯЗАТЕЛЬНЫЕ ПЛАТФОРМЕННЫЕ ПРОТОКОЛЫ:**
- **[AI Agent Execution Protocol](docs/ai-agent-execution-protocol.md)** - 5-step workflow для всех задач
- **[AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)** - Role definitions (Developer роль)
- **[MCP Webhook Testing Guide](docs/mcp-webhook-testing-guide.md)** - Testing procedures
- **[GitHub Issues Protocol](docs/github-issues-protocol.md)** - Issue management

### **📋 PROJECT-SPECIFIC ДОКУМЕНТАЦИЯ:**
- **Architecture Overview** - `docs/projects/[project]/architecture.md`
  - **⚠️ ВАЖНО:** Из architecture.md найти нужный блок и читать ТОЛЬКО его
  - НЕ загружать всю архитектуру в context одновременно
- **Credentials Reference** - `docs/projects/[project]/credentials-reference.md`

### **🔍 n8n PLATFORM DOCUMENTATION:**
- **n8n Node Documentation** - через MCP `get_node_documentation(nodeType)`
- **Validate configuration** - `validate_node_operation(nodeType, config)`

---

## 🎭 Developer-Tester Role

### **UNIFIED RESPONSIBILITIES:**
- **Verify architecture** против n8n documentation перед началом
- **Develop minimal node groups** (1-3 nodes max)
- **Test each group** immediately после creation
- **Document progress** в Issue comments

---

## 🚨 Architecture Issue Escalation

**ЕСЛИ обнаружены проблемы в architecture:**

1. **🛑 STOP Development** - документировать проблему в Issue
2. **📝 Request Approval** для изменения architecture
3. **⏳ Wait for Approval** перед продолжением
4. **✅ Update Architecture** после одобрения

**Issue Comment Format:**
```markdown
## ⚠️ ARCHITECTURE ISSUE
**Problem:** [technical issue]
**Proposed Solution:** [brief description]
**Requesting approval** to proceed
```

---

## 🔄 3-Step Development Cycle

### **MANDATORY DEVELOPMENT WORKFLOW:**

#### **Step 1: n8n Development (MCP Tools)**
- **Develop workflows** непосредственно на n8n instance через MCP
- **Start from current state** - ориентируясь на активный Issue и записи в нем
- **Create minimal node groups** (1-3 nodes max)
- **Test via webhook** immediately после каждой группы

#### **Step 2: GitHub Sync**
- **Export workflow JSON** из n8n после успешного тестирования
- **Sync DEV files** в `workflows/[project]/dev/` папку на GitHub
- **Create/Update workflow files** с descriptive названиями
- **Commit changes** с clear commit message

#### **Step 3: Issue Progress Update**
- **Update Issue comments** с progress status
- **Document achievements** - что именно completed
- **Note next steps** - план для following iteration
- **Fix any issues** if discovered durante sync

### **REPEAT CYCLE:**
**Повторять 3-step цикл до тех пор, пока проект не будет готов к PROD deployment**

---

## 📝 Development Journal

**ОБЯЗАТЕЛЬНО документировать в Issue comments:**

**Session Start:**
```markdown
🚀 **Development Session**
Target: [node group]
Plan: [brief plan]
Current n8n State: [описание текущего состояния]
```

**After GitHub Sync:**
```markdown
✅ **Progress Update - Synced to GitHub**  
Completed: [achievements]
Files Updated: workflows/[project]/dev/[files]
Next: [next steps]
Notes: [important details]
```

**Issues Found:**
```markdown
⚠️ **Problem Found**
Issue: [description] 
Solution: [what you did]
GitHub Status: [synced/pending sync]
```

---

## 📁 GitHub Sync Procedures

### **File Organization:**
```
workflows/[project]/
├── dev/                    # DEV workflows (active development)
│   ├── main-workflow.json  # Primary workflow file
│   └── [additional-files]  # Support files if needed
└── prod/                   # PROD workflows (after deployment)
```

### **Sync Process:**
1. **Export from n8n** - через MCP tools get workflow JSON
2. **Update dev files** - replace/create workflow files в dev/ folder
3. **Commit changes** - descriptive message с progress indication
4. **Update Issue** - confirm sync completed

### **Commit Message Format:**
```
[PROJECT] Block X development - [brief description]

- Added nodes: [list]
- Testing status: [passed/in progress]
- Next: [next development step]
```

---

## 🚨 Critical Rules

- **NO architecture changes без approval**
- **ALWAYS follow 3-step cycle**: n8n Dev → GitHub Sync → Issue Update
- **Test each node group** immediately на n8n
- **Sync to GitHub** only after successful testing
- **Document progress** в Issue comments after each sync
- **Read ONLY нужный architecture block**
- **Clean temporary nodes** after testing (keep input webhook)

---

*Protocol ensures systematic n8n workflow development с built-in quality controls, GitHub synchronization, и streamlined developer experience.*