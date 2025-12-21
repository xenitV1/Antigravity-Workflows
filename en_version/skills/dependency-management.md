---
name: dependency-management
description: Package and dependency management guide. Security audit, version management, and upgrade strategies.
metadata:
  skillport:
    category: operations
    tags:
      - npm
      - dependencies
      - security
      - versioning
---

# Dependency Management Skill

> Guide for secure and sustainable dependency management.
> Security auditing, version control, and upgrade strategies.

---

## 🎯 Core Principles

| Principle | Description |
|---------|----------|
| **Minimize Dependencies** | Do not add unnecessary packages |
| **Lock Versions** | Commit package-lock.json |
| **Audit Regularly** | Weekly security checks |
| **Update Strategically** | Careful with major updates |

---

## 📏 Decision to Add a Package

### Before Adding a Package

- **Is it really necessary?**: Can it be done with a native solution or a simple utility?
- **Package Quality**: Check weekly downloads (>10K), GitHub stars (>1K), and last commit (<6 months).
- **Security**: npm audit must be clean.
- **License**: MIT / Apache 2.0 / ISC are compatible. Do not use GPL for commercial projects.

---

## 🔒 Security Auditing

### npm audit

```bash
# Security scan
npm audit

# Automatic fix (use with caution!)
npm audit fix

# Json format for CI
npm audit --json
```

---

## 📦 Version Management

### Semantic Versioning

```
MAJOR.MINOR.PATCH
  │      │     │
  │      │     └── Backward compatible bug fixes
  │      └──────── Backward compatible new features
  └─────────────── Breaking changes
```

### Version Range Syntax

- **Exact**: `1.2.3` (Full version)
- **Patch**: `~1.2.3` (1.2.x)
- **Minor**: `^1.2.3` (1.x.x) [DEFAULT]

---

## ⬆️ Upgrade Strategy

### Regular Minor Updates

```bash
# Show outdated packages
npm outdated

# Interactive update
npx npm-check -u

# Only patch/minor (safe)
npm update
```

### Major Updates (Carefully!)

1. **Read CHANGELOG**: Check migration guides and breaking changes.
2. **Create Branch**: Perform updates and fixes in a separate branch.
3. **Verify**: Run full tests and check for performance regressions.

---

## 🧹 Dependency Cleanup

### Find Unused Packages

```bash
# Install depcheck
npm install -g depcheck

# Find unused packages
depcheck
```

### Cleanup Script

```bash
# Remove unnecessary packages
npm uninstall <package-name>

# Clean node_modules and reinstall
rm -rf node_modules
npm ci
```

---

## ✅ Checklist

### When Adding a Package
- [ ] Really necessary?
- [ ] Alternatives evaluated?
- [ ] Security audit clean?
- [ ] License compatible?

### Regular Maintenance (Weekly)
- [ ] Run npm audit
- [ ] Review Dependabot/Renovate PRs
- [ ] Check outdated packages

---

## 🔴 Don't List

❌ Do not use "*" or "latest" in package.json
❌ Do not add package-lock.json to .gitignore
❌ Do not run `npm audit fix --force` blindly
❌ Do not deploy major updates without testing

---

## ✅ Must Do List

✅ Commit package-lock.json
✅ Use `npm ci` in CI/CD pipeline
✅ Run weekly npm audit
✅ Use Dependabot or Renovate
✅ Create separate branches for major updates
✅ Clean up unused dependencies

---

**Last Update:** December 2025
**Version:** 1.0
