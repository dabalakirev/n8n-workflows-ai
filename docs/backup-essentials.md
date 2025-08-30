# Backup Essentials

## 🔄 Pre-Change Backup

**Before major workflow changes:**
1. **Export workflows:** n8n Settings → Download → save as `workflow-name-v1.0-2025-MM-DD.json`
2. **Git commit:** All changes must be committed
3. **Document credentials:** List credential names (no sensitive data)

## 🛡️ Recovery

**Restore workflow:**
1. **Import:** n8n Settings → Import → select backup JSON
2. **Recreate credentials:** Same names as documented
3. **Test:** Run workflow manually to verify

## ✅ Backup Checklist

**Before Major Changes:**
- [ ] Export workflows to JSON
- [ ] Git commit all changes
- [ ] Document credential names

**Recovery Steps:**
- [ ] Import JSON backup
- [ ] Recreate credentials
- [ ] Test workflow functionality

## 🎯 Key Principle

**GitHub repository = primary backup**. Always commit workflow JSON files to Git for version control and recovery.

---

**Emergency Recovery:** Clone repository → Import workflows → Recreate credentials → Test