# n8n-workflows-ai

**AI-Powered Automation Platform** для разработки n8n workflows с test-driven development и современными DevOps практиками

## 🎯 Platform Overview

**n8n-workflows-ai** - это универсальная платформа для создания, тестирования и управления n8n automation проектами с использованием AI агентов и structured development protocols.

### 🏗️ **Platform Architecture**

```
n8n-workflows-ai Platform
├── 🤖 AI Agent Protocols          # Structured development with AI
├── 🧪 Testing Framework           # Universal Test Orchestrator
├── 🚀 CI/CD Pipeline             # GitHub Actions automation
├── 📚 Documentation System       # Comprehensive guides & protocols
└── 📁 Projects                   # Individual automation projects
    └── 🐦 First Bird (current)   # Financial data automation
```

### ⚡ **Platform Capabilities**

- **AI-Assisted Development** with structured roles and protocols
- **Universal Testing Framework** via Test Orchestrator
- **Multi-Project Support** with DEV/PROD environment separation
- **Automated CI/CD** through GitHub Actions
- **Comprehensive Documentation** with protocols and best practices
- **Scalable Architecture** ready for new automation projects

---

## 🐦 Current Project: "First Bird"

**Financial Data Automation** - pilot project demonstrating platform capabilities

### **Project Scope:**
- **Data Source:** Financial Modeling Prep API
- **AI Analysis:** Market insights and financial data processing
- **Automation Goals:** Streamlined financial data workflows

### **Project Workflows:**
- **🤖 AI Deepseek** - Financial data analysis with AI language model
- **🔗 FMP API Router** - Financial Modeling Prep API routing and data transformation

### **Project Status:**
```
📊 First Bird Progress:        ██████████ 100% (workflows implemented)
🧪 Testing Integration:        ████████░░  80% (Test Orchestrator ready)
📚 Documentation:              ████████░░  80% (protocols & guides complete)
🚀 Production Readiness:       ███████░░░  70% (ready for deployment)
```

---

## 🛠️ Platform Tools

### 🧪 **Test Orchestrator** *(Universal Testing Tool)*
- **Purpose:** Automated testing for ANY n8n workflows
- **Scope:** Platform-level tool, not project-specific
- **Capabilities:** Execute workflow testing, result aggregation, comprehensive reporting
- **Usage:** Works with all projects created on the platform

### 🚀 **GitHub Actions Pipeline**
- **Workflow Validation:** JSON structure and n8n schema validation
- **Issue Automation:** Labels, milestones, lifecycle management
- **Release Management:** Automated versioning and deployment
- **Quality Gates:** Automated testing before production deployment

### 📚 **Documentation System**
- **AI Agent Protocols** - Structured development workflows
- **Development Guides** - Best practices and procedures
- **Security Standards** - Credential management and data protection
- **Testing Procedures** - Quality assurance processes

---

## 🗺️ Platform Roadmap

### 📅 **Current Status: Milestone v1.1 - Documentation & Infrastructure**
```
v1.1 Documentation & Infrastructure:  ██████████ 90% (platform foundation)
v1.2 Testing Framework:               ████░░░░░░ 40% (Test Orchestrator ready)
v1.3 Advanced Features:               ░░░░░░░░░░  0% (multi-project scaling)

Overall Platform Progress:            ███████░░░ 75%
```

### 🎯 **Platform Milestones:**
- **🏗️ v1.1 - Platform Foundation** (Sept 2025) - *Documentation & Infrastructure*
  - Complete AI Agent protocols and development procedures
  - Optimize GitHub environment for productivity
  - Establish release and version management systems
  
- **🧪 v1.2 - Testing Framework** (Oct-Nov 2025) - *Universal Testing Infrastructure*
  - Activate Test Orchestrator for automated testing
  - Integrate testing with CI/CD pipeline
  - Establish quality gates for deployment
  
- **🚀 v1.3 - Multi-Project Platform** (Dec 2025) - *Scaling & Advanced Features*
  - Multi-project support and management
  - Performance optimization suite
  - Enterprise integrations and features

📖 **[Detailed Platform Roadmap →](docs/roadmap.md)**

---

## 🏗️ Architecture & Environment Structure

### **Multi-Environment Support:**
- **DEV Environment** - Development and testing (2 triggers: Manual + Execute Workflow)
- **PROD Environment** - Production deployments (1 trigger: Manual only)
- **Test Framework** - Automated quality assurance via Test Orchestrator

### **Repository Structure:**
```
├── workflows/           # Project workflow implementations
│   ├── dev/            # DEV versions with testing triggers
│   └── prod/           # PROD versions (production-ready)
├── docs/               # Platform documentation and protocols
│   ├── roadmap.md                       # Platform development roadmap
│   ├── ai-agent-execution-protocol.md   # AI Agent structured workflows
│   ├── ai-agent-roles-protocols.md     # AI Agent roles in SDLC
│   ├── context-handoff-protocol.md     # AI context transfer procedures
│   ├── testing-strategy.md             # Platform testing methodology
│   ├── github-issues-protocol.md       # Issue management procedures
│   ├── backup-essentials.md            # Data protection procedures
│   └── security-best-practices.md      # Security standards & guidelines
└── .github/
    ├── workflows/      # GitHub Actions (CI/CD automation)
    └── ISSUE_TEMPLATE/ # Standardized issue templates
```

---

## 🚀 Getting Started

### **For AI Agents:**
1. **Read AI Agent Execution Protocol** - mandatory workflow for all assignments
2. **Study AI Agent Roles & Protocols** - understand SDLC roles and processes
3. **Review all platform protocols** in `docs/` directory
4. **Check Platform Roadmap** for current priorities and milestone status
5. **Verify platform status** through `n8n_health_check`
6. **Follow 5-step execution flow** for every assignment
7. **IMPORTANT:** Review backup and security requirements before major changes

### **For Developers:**
1. Clone repository and explore platform structure
2. Study **[Platform Roadmap](docs/roadmap.md)** for architecture understanding
3. Import project workflows into n8n DEV/PROD environments
4. Configure development environment following platform protocols
5. Follow **[Security Best Practices](docs/security-best-practices.md)** for credentials
6. Follow **[Backup Essentials](docs/backup-essentials.md)** before major changes

### **For New Projects:**
1. Study platform architecture and existing project structure
2. Create project-specific workflows in DEV environment
3. Follow platform testing procedures with Test Orchestrator
4. Use platform documentation templates and protocols
5. Deploy to PROD environment following established procedures

---

## 🧪 Platform Testing Framework

### ✅ **Universal Test Orchestrator:**
- **Capability:** Tests ANY n8n workflows created on the platform
- **Architecture:** Platform-level tool serving all projects
- **Integration:** Works with DEV environments (dual triggers: Manual + Execute Workflow)
- **Automation:** Integrated with GitHub Actions for automated testing
- **Scalability:** Ready to test multiple projects as platform grows

### 📊 **Testing Methodology:**
- **DEV Workflows:** Dual triggers enable both manual and automated testing
- **PROD Workflows:** Single manual trigger for production stability
- **Quality Gates:** Automated testing blocks defective deployments
- **Test Coverage:** Target 100% automation of critical workflow paths

---

## 🔧 Platform Technologies

- **n8n** - Core automation platform
- **GitHub** - Version control, project management, and CI/CD
- **GitHub Actions** - Automated pipeline and quality gates
- **GitHub Issues** - Structured task and change management
- **MCP (Model Context Protocol)** - AI agent platform integration
- **Test Orchestrator** - Universal workflow testing framework

---

## 📊 Platform Metrics

- **Current Projects**: 1 (First Bird - financial automation)
- **Platform Tools**: Test Orchestrator, GitHub Actions, Documentation System
- **Active Issues**: 11 platform and project issues (view on [GitHub Issues](../../issues))
- **Automation Coverage**: Target 100% DEV workflows (in development)
- **Architecture**: Multi-environment with controlled DEV → PROD migration
- **Documentation**: Comprehensive coverage of all platform processes

---

## 🤝 Platform Development Rules

### **For All Platform Contributors:**
1. **Follow Platform Protocols** - all established procedures are mandatory
2. **No Changes Without Issues** - structured change management required
3. **Follow Platform Roadmap** - align with milestone priorities
4. **Security First** - mandatory security practices (see [Security Best Practices](docs/security-best-practices.md))
5. **Backup Before Major Changes** - data protection required (see [Backup Essentials](docs/backup-essentials.md))
6. **Universal Testing** - all changes must pass Test Orchestrator validation
7. **Documentation Integration** - all architectural decisions must be documented
8. **Protocol Compliance** - established workflows must be followed

### **For AI Agents:**
1. **Follow AI Agent Execution Protocol** - mandatory for every assignment
2. **Use Appropriate AI Agent Role** - according to [AI Agent Roles & Protocols](docs/ai-agent-roles-protocols.md)
3. **Context Integration** - read platform documentation before starting work
4. **Roadmap Awareness** - check current priorities and milestones
5. **Issue Management** - create and update Issues for all planned changes
6. **Documentation Updates** - maintain platform documentation with changes
7. **Security and Backup Compliance** - verify requirements according to protocols

---

## 🎯 Future Projects

The platform is designed for scalability and ready to support additional automation projects:

- **Multi-Project Architecture** - Repository structure supports project separation
- **Universal Testing Framework** - Test Orchestrator works with any n8n workflows
- **Reusable Protocols** - AI Agent and development procedures apply to all projects
- **Scalable CI/CD** - GitHub Actions pipeline adapts to multiple projects
- **Documentation Templates** - Established patterns for new project documentation

---

## 📞 Platform Support

- **Issues**: Use GitHub Issues with standardized templates
- **Documentation**: Comprehensive guides in `docs/` directory
- **Roadmap**: Current development status in [docs/roadmap.md](docs/roadmap.md)
- **AI Agent Support**: Follow AI Agent Execution Protocol and Context Handoff Protocol
- **Security Support**: Security guidelines in [docs/security-best-practices.md](docs/security-best-practices.md)
- **Backup Support**: Recovery procedures in [docs/backup-essentials.md](docs/backup-essentials.md)

---

**This platform demonstrates modern AI-powered automation development with structured protocols, comprehensive security practices, universal testing framework, reliable backup procedures, and scalable multi-project architecture.**