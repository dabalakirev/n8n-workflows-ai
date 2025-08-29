# Backup Essentials

## 🎯 Overview

Упрощенная backup стратегия для защиты критических данных проекта n8n workflows без enterprise-level избыточности. Фокус на практичность и manual procedures.

---

## 🔄 Pre-Change Workflow Backup

### Manual JSON Export Process

#### Экспорт ваших workflows:
1. **Откройте n8n workflow** в редакторе
2. **Нажмите Settings** (⚙️ в правом верхнем углу)
3. **Выберите "Download"** → сохранится как `.json` файл
4. **Переименуйте файл** с указанием версии и даты:
   ```
   my-workflow-v1.2-2025-08-29.json
   production-workflow-backup-2025-08-29.json
   ```

#### Backup всех активных workflows:
- **Экспортируйте ВСЕ workflows** в проекте перед major changes
- **Сохраняйте локально** в отдельную папку `workflow-backups/`
- **Commit в Git** backup файлы для версионного контроля

### Credentials Documentation Checklist

- [ ] **Список всех используемых credentials** в workflows
- [ ] **Документация credential names** (без sensitive data)
- [ ] **Тип каждого credential** (API Key, OAuth, Database, etc.)
- [ ] **Which workflows используют каждый credential**
- [ ] **Recovery contact info** для восстановления credentials

### GitHub Commit Verification

- [ ] **Все изменения committed** в Git перед backup
- [ ] **Working directory clean** (`git status` = чисто)
- [ ] **Current branch identified** для восстановления state
- [ ] **Tag important versions** для easy rollback

---

## 🛡️ Recovery Essentials

### Workflow Import Procedure

#### Восстановление из JSON backup:
1. **Откройте n8n** и перейдите в нужный проект
2. **Click "+" для создания workflow** или откройте существующий
3. **Settings → Import** → выберите backup `.json` файл
4. **Проверьте node connections** после импорта
5. **Verify all node configurations** корректно загружены

#### Если workflow не импортируется:
- **Проверьте n8n version compatibility** с backup
- **Убедитесь что все custom nodes** установлены
- **Import по частям** если workflow слишком сложный

### Credentials Restoration Steps

#### Manual credentials setup:
1. **Создайте новые credentials** в n8n Settings
2. **Используйте те же names** что были в backup documentation
3. **Восстановите API keys/tokens** из secure storage
4. **Test каждый credential** перед использованием в workflows
5. **Update workflow connections** к restored credentials

#### Credentials security:
- **Never commit credentials** в Git repository
- **Use environment variables** для sensitive data где возможно
- **Document credential recovery process** без actual values

### Functionality Verification

#### После восстановления workflow:
- [ ] **Manual trigger test** - запустите workflow вручную
- [ ] **Check all node outputs** корректные
- [ ] **Verify external API calls** работают
- [ ] **Test error handling** scenarios
- [ ] **Run Test Orchestrator** для automated validation (если доступен)

---

## ✅ Quick Backup Checklist

### Before Major Workflow Changes
- [ ] Export current workflow versions to JSON
- [ ] Document current credentials setup
- [ ] Commit all changes в Git repository
- [ ] Tag current version для easy reference
- [ ] Note down current n8n project settings

### Before Credential Updates
- [ ] Document existing credential names и types
- [ ] Export workflows using old credentials
- [ ] Test backup imports работают
- [ ] Prepare rollback plan если update fails
- [ ] Backup environment variables (names only)

### Before Environment Switches
- [ ] Full export всех workflows в current environment
- [ ] Document environment-specific configurations
- [ ] Backup project settings и permissions
- [ ] Note down webhook URLs и external integrations
- [ ] Create environment migration checklist

---

## 🔗 Integration with Project Tools

### Test Orchestrator Integration

**Test Orchestrator** - наш стандартный testing tool для workflow validation:
- **Use Test Orchestrator** для verification после восстановления
- **Include Test Orchestrator backup** в regular backup procedures
- **Test restored workflows** через Test Orchestrator перед production use
- **Maintain Test Orchestrator test scenarios** как part of backup strategy

### Security Best Practices Integration

Этот документ интегрируется с `security-best-practices.md`:
- **Never backup credentials** в plain text
- **Use secure credential storage** methods
- **Regular backup verification** procedures
- **Access control** для backup files

### Testing Strategy References

Integration с `testing-strategy.md`:
- **Test restored workflows** перед production deployment
- **Validate backup integrity** через automated tests
- **Include backup/restore procedures** в testing scenarios

---

## 🚨 Emergency Recovery Procedures

### Complete Project Loss Scenario

#### If entire n8n project lost:
1. **Clone repository** с latest backup files
2. **Setup new n8n instance** с same version
3. **Import workflows** из JSON backups по порядку
4. **Recreate credentials** используя backup documentation
5. **Test each workflow** step by step
6. **Run full Test Orchestrator suite** для validation

#### Recovery Priority Order:
1. **Critical production workflows** first
2. **Test Orchestrator** для validation capability
3. **Development workflows** last
4. **Verify all integrations** working

### GitHub Repository Recovery

#### If Git repository compromised:
- **GitHub automatically backups** repository data
- **Clone from GitHub** к local environment
- **All committed workflows** preserved in Git history
- **Use Git history** для point-in-time recovery
- **Restore from specific commit** if needed

---

## 📚 Additional Resources

### Related Documentation
- [AI Agent Execution Protocol](ai-agent-execution-protocol.md) - для structured backup procedures
- [GitHub Issues Protocol](github-issues-protocol.md) - для tracking backup-related issues
- [Testing Strategy](testing-strategy.md) - для backup validation procedures

### Git Workflow Integration
- **Use Git tags** для important workflow versions
- **Commit messages** должны включать backup context
- **Branch protection** помогает prevent accidental data loss

### Manual Backup Schedule
- **Before major changes** - always
- **Weekly routine backup** - recommended для active development
- **Before credential rotations** - critical
- **Before environment migrations** - essential

---

## 🎯 Key Principles

### Simplicity Over Complexity
- **Manual procedures** предпочтительнее automated systems
- **Simple checklists** лучше complex automation
- **Human verification** каждого backup step
- **Clear recovery procedures** без enterprise overhead

### GitHub as Primary Backup
- **Repository serves** как primary backup mechanism
- **All workflow JSON files** версioned в Git
- **Documentation changes** tracked through commits
- **Branch history** provides point-in-time recovery

### Focus on Critical Data Only
- **Workflow JSON files** - essential
- **Credentials documentation** (не sensitive data) - important  
- **Project structure** - useful
- **Everything else** - optional

---

*This backup strategy follows the project's principle of practical simplicity while ensuring protection of critical workflow data and maintaining recovery capability for development-stage projects.*

**Last updated:** August 2025  
**Document version:** 1.0