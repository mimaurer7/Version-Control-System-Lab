# Branching Strategy

## Feature Branch Workflow

This project uses the Feature Branch Workflow for version control.

### Branch Naming Conventions

- `feature/` - New features (e.g., `feature/add-security-scan`)
- `bugfix/` - Bug fixes (e.g., `bugfix/fix-css-layout`)
- `hotfix/` - Critical fixes for production
- `main` - Stable production-ready code

### Workflow

1. Create a new branch from `main`
2. Make changes and commit
3. Push branch and create pull request
4. Review and merge into `main`

### Example
```
git checkout -b feature/add-login
# Make changes
git add .
git commit -m "Add login functionality"
git push origin feature/add-login
```