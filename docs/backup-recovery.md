# Backup and Recovery Procedures

## Remote Backup Strategy

### GitHub Remote Repository
- **Remote URL**: https://github.com/mimaurer7/Version-Control-System-Lab.git
- **Backup Frequency**: Every push to main branch
- **Automatic**: Yes, through git push commands

### Regular Backup Process

#### Daily Workflow
```bash
# After completing work
git add .
git commit -m "Descriptive message"
git push origin main
```

#### Weekly Verification
```bash
# Verify remote connection
git remote -v

# Check synchronization status
git status
```

## Recovery Procedures

### Scenario 1: Recover Entire Repository
If local repository is lost or corrupted:
```bash
# Clone from GitHub to restore
cd C:\Projects\School Projects
git clone https://github.com/mimaurer7/Version-Control-System-Lab.git
cd "Version Control System Lab"
```

**Recovery Time**: ~2-5 minutes depending on repository size

---

### Scenario 2: Recover Specific File Version
To restore a file to a previous version:
```bash
# View file history
git log -- path/to/file

# Restore file from specific commit
git checkout <commit-hash> -- path/to/file
```

**Recovery Time**: <1 minute

---

### Scenario 3: Undo Last Commit (Not Pushed)
```bash
# Undo commit but keep changes
git reset --soft HEAD~1

# Undo commit and discard changes
git reset --hard HEAD~1
```

---

### Scenario 4: Recover After Accidental Push
```bash
# Revert to previous commit
git revert HEAD

# Push the revert
git push origin main
```

---

## Testing Backup Procedures

### Test 1: Clone Test (Completed)
**Date**: November 22, 2024
**Procedure**: 
1. Pushed repository to GitHub
2. Verified all commits present
3. Confirmed branch structure intact

**Result**: ✅ SUCCESS - All data successfully backed up

---

### Test 2: File Recovery Simulation
**Procedure**:
1. Create test file
2. Commit and push
3. Delete locally
4. Recover from remote

**Command**:
```bash
git checkout origin/main -- filename
```

**Result**: Files can be recovered from remote repository

---

## Backup Schedule

| Frequency | Action | Responsible |
|-----------|--------|-------------|
| Daily | Push commits after work sessions | Developer |
| Weekly | Verify remote sync | Developer |
| Monthly | Clone test to verify backup integrity | Team Lead |
| Quarterly | Review backup procedures | Security Team |

## Emergency Contacts

- **GitHub Support**: https://support.github.com
- **Repository Owner**: Matthew Maurer (mimaurer7@gmail.com)
- **Backup Status**: https://github.com/mimaurer7/Version-Control-System-Lab

## Backup Verification Checklist
- [x] Remote repository configured
- [x] Initial push completed
- [x] Branch tracking established
- [x] Recovery procedures documented
- [x] Test clone successful