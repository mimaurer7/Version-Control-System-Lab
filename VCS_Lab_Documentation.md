# Version Control System (VCS) Lab Documentation

**Student Name**: Matthew Maurer  
**GitHub Username**: mimaurer7  
**Course**: Cybersecurity  
**Date**: November 22, 2024  
**Repository**: https://github.com/mimaurer7/Version-Control-System-Lab

---

## Table of Contents
1. Introduction
2. Setup and Configuration
3. Branching Strategy
4. Secure Coding Practices
5. Backup and Recovery
6. Conclusion

---

## 1. Introduction

This document details the implementation of professional version control practices for the VCS Lab assignment. The project demonstrates Git fundamentals, branching workflows, security integration, and backup procedures essential for secure software development.

### Project Overview
- **Version Control System**: Git
- **Remote Repository**: GitHub
- **Branching Model**: Feature Branch Workflow
- **Security Integration**: Pre-commit hooks with automated scanning

---

## 2. Setup and Configuration

### 2.1 Repository Initialization

The repository was initialized using the `git init` command in the project directory:
```bash
git init
```

**[INSERT SCREENSHOT 1: Terminal showing git init output]**

### 2.2 Git Configuration

User information was configured to track commit authorship:
```bash
git config user.name "mimaurer7"
git config user.email "mimaurer7@gmail.com"
```

This ensures all commits are properly attributed to the repository owner.

### 2.3 .gitignore Configuration

A comprehensive `.gitignore` file was created to exclude:
- Personal configuration files (*.local, config/settings.json)
- Sensitive data (*.key, *.pem, *.env, secrets/)
- Dependency folders (node_modules/, venv/, __pycache__/)
- IDE settings (.vscode/settings.json, .idea/)
- Operating system files (.DS_Store, Thumbs.db)
- Build output (dist/, build/, *.log)
- Backup files (*.bak, *.tmp)

**[INSERT SCREENSHOT 5: .gitignore file contents]**

### 2.4 Project Structure

The following directory structure was established:
```
Version Control System Lab/
├── .git/                    # Git repository data
├── .gitignore               # Ignored files configuration
├── README.md                # Project documentation
├── src/                     # Source code
│   ├── index.html
│   ├── styles.css
│   └── app.js
├── scripts/                 # Automation scripts
│   └── security_scan.py
├── docs/                    # Documentation
│   ├── branching-strategy.md
│   ├── security-practices.md
│   └── backup-recovery.md
└── config/                  # Configuration
    └── settings.example.json
```

**[INSERT SCREENSHOT 4: VS Code Explorer showing project structure]**

### 2.5 Initial Commit

All project files were staged and committed:
```bash
git add .
git commit -m "Initial commit: Project setup with structure and base files"
```

**[INSERT SCREENSHOT 1: Git log showing initial commit]**

---

## 3. Branching Strategy

### 3.1 Feature Branch Workflow

This project implements the Feature Branch Workflow, which is ideal for small to medium projects. This workflow ensures the main branch always contains stable, production-ready code.

### 3.2 Branch Naming Conventions

Clear naming conventions were established:

| Prefix | Purpose | Example |
|--------|---------|---------|
| `feature/` | New features | `feature/add-security-dashboard` |
| `bugfix/` | Bug fixes | `bugfix/fix-css-styling` |
| `hotfix/` | Critical production fixes | `hotfix/security-patch` |
| `main` | Stable production code | `main` |

### 3.3 Workflow Demonstration

#### Feature Branch: Security Dashboard

**Step 1**: Create feature branch from main
```bash
git checkout -b feature/add-security-dashboard
```

**Step 2**: Implement feature (added security dashboard to index.html)

**Step 3**: Commit changes
```bash
git add src/index.html
git commit -m "Add security dashboard section to homepage"
```

**Step 4**: Merge into main
```bash
git checkout main
git merge feature/add-security-dashboard
```

#### Bugfix Branch: CSS Styling

**Step 1**: Create bugfix branch
```bash
git checkout -b bugfix/fix-css-styling
```

**Step 2**: Fix styling issues (added security dashboard CSS)

**Step 3**: Commit and merge
```bash
git add src/styles.css
git commit -m "Fix: Add styling for security dashboard section"
git checkout main
git merge bugfix/fix-css-styling
```

**[INSERT SCREENSHOT 2: Git branch output showing all branches]**

**[INSERT SCREENSHOT 1: Git log with graph showing merge history]**

### 3.4 Benefits of Feature Branch Workflow

1. **Isolation**: Each feature developed independently
2. **Stability**: Main branch always production-ready
3. **Collaboration**: Multiple developers can work simultaneously
4. **Code Review**: Changes reviewed before merging
5. **Rollback**: Easy to revert problematic features

---

## 4. Secure Coding Practices

### 4.1 Pre-commit Security Hooks

A pre-commit hook was implemented to run security scans before allowing commits:

**Location**: `.git/hooks/pre-commit`
```bash
#!/bin/sh
# Pre-commit hook for security scanning

echo "Running security checks..."
python scripts/security_scan.py

if [ $? -ne 0 ]; then
    echo "Security scan failed! Commit aborted."
    exit 1
fi

echo "Security checks passed!"
exit 0
```

This hook:
- Runs automatically before each commit
- Executes the security_scan.py script
- Blocks commits if security issues are detected
- Ensures only validated code enters the repository

### 4.2 Security Scanning Tools

#### Recommended CI/CD Integration:

**SonarQube**
- Purpose: Static code analysis
- Detection: Code smells, bugs, security vulnerabilities
- Integration: GitHub Actions, GitLab CI
- Benefits: Continuous quality monitoring

**Snyk**
- Purpose: Dependency vulnerability scanning
- Detection: Known security issues in libraries
- Integration: `snyk test` in CI pipeline
- Benefits: Real-time vulnerability alerts

**OWASP Dependency Check**
- Purpose: Identify vulnerable dependencies
- Detection: CVE database matching
- Integration: Maven/Gradle plugin or CLI
- Benefits: Comprehensive vulnerability reporting

### 4.3 Dependency Management

**Update Schedule**:
- **Weekly**: Check for dependency updates
- **Monthly**: Review and apply security patches
- **Immediate**: Critical security vulnerabilities

**Update Process**:
1. Review changelogs for breaking changes
2. Update in development environment
3. Run full test suite
4. Deploy to staging environment
5. Monitor for issues
6. Deploy to production

**Commands**:
```bash
# Python
pip list --outdated
pip install --upgrade package-name

# Node.js
npm outdated
npm update
```

### 4.4 Security Checklist

- [x] Pre-commit hooks configured
- [x] Dependencies scanned for vulnerabilities
- [x] Secrets not committed (.gitignore configured)
- [x] .gitignore properly configured
- [x] Code reviewed before merging
- [ ] CI/CD security scans (would be configured in production)

---

## 5. Backup and Recovery

### 5.1 Remote Repository Configuration

The local repository was connected to GitHub for remote backup:
```bash
git remote add origin https://github.com/mimaurer7/Version-Control-System-Lab.git
git push -u origin main
```

**[INSERT SCREENSHOT 6: GitHub repository page]**

### 5.2 Backup Strategy

**Frequency**: 
- Automatic backup on every push to main
- Daily pushes during active development
- Weekly verification of sync status

**Verification Commands**:
```bash
git remote -v          # Verify remote connection
git status             # Check sync status
```

### 5.3 Recovery Procedures

#### Scenario 1: Complete Repository Loss

If the local repository is lost or corrupted:
```bash
cd C:\Projects\School Projects
git clone https://github.com/mimaurer7/Version-Control-System-Lab.git
```

**Recovery Time**: 2-5 minutes

#### Scenario 2: File Recovery

To restore a specific file to a previous version:
```bash
git log -- path/to/file                    # View file history
git checkout <commit-hash> -- path/to/file # Restore file
```

**Recovery Time**: <1 minute

#### Scenario 3: Undo Last Commit
```bash
git reset --soft HEAD~1   # Undo commit, keep changes
git reset --hard HEAD~1   # Undo commit, discard changes
```

#### Scenario 4: Revert Pushed Changes
```bash
git revert HEAD           # Create revert commit
git push origin main      # Push revert
```

### 5.4 Backup Testing

**Test Performed**: Repository clone verification  
**Date**: November 22, 2024  
**Result**: ✅ SUCCESS - All commits, branches, and files successfully backed up

**Verification**:
1. Pushed all commits to GitHub
2. Verified commit history matches local
3. Confirmed all branches present
4. Tested file accessibility

### 5.5 Backup Schedule

| Frequency | Action | Responsible |
|-----------|--------|-------------|
| Daily | Push commits after work | Developer |
| Weekly | Verify remote sync | Developer |
| Monthly | Clone test for integrity | Team Lead |
| Quarterly | Review procedures | Security Team |

---

## 6. Conclusion

This VCS lab successfully demonstrates professional version control practices including:

✅ **Repository Setup**: Proper initialization and configuration  
✅ **Version Control**: Atomic commits with descriptive messages  
✅ **Branching Strategy**: Feature Branch Workflow with clear conventions  
✅ **Security Integration**: Pre-commit hooks and scanning tools  
✅ **Backup & Recovery**: Remote repository with tested recovery procedures

These practices form the foundation of secure, collaborative software development and are essential skills for cybersecurity professionals.

### Key Takeaways

1. **Version control is essential** for tracking changes and collaboration
2. **Branching workflows** enable parallel development without conflicts
3. **Security must be integrated** into the development process from the start
4. **Regular backups** prevent data loss and enable quick recovery
5. **Documentation** ensures practices can be followed by team members

### Repository Access

- **GitHub**: https://github.com/mimaurer7/Version-Control-System-Lab
- **Owner**: Matthew Maurer (mimaurer7@gmail.com)

---

**End of Documentation**