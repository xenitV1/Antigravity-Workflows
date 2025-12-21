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

# 📋 Contents

1. [Core Principles](#1-core-principles)
2. [Decision to Add a Package](#2-decision-to-add-a-package)
3. [Security Auditing](#3-security-auditing)
4. [Version Management](#4-version-management)
5. [Upgrade Strategy](#5-upgrade-strategy)
6. [Lock File Management](#6-lock-file-management)
7. [Dependency Cleanup](#7-dependency-cleanup)
8. [Dependency Monitoring](#8-dependency-monitoring)
9. [Checklist](#9-checklist)
10. [Don't List](#10-dont-list)
11. [Must Do List](#11-must-do-list)

---

# 1. Core Principles

| Principle | Description |
|---------|----------|
| **Minimize Dependencies** | Do not add unnecessary packages |
| **Lock Versions** | Commit package-lock.json |
| **Audit Regularly** | Weekly security checks |
| **Update Strategically** | Careful with major updates |
| **Document Decisions** | Why this package? |

---

# 2. Decision to Add a Package

## 2.1 Before Adding a Package

```markdown
## Package Evaluation Checklist

### Is it really necessary?
- [ ] Is there a native solution? (built-in modules)
- [ ] Can it be done with a simple utility?
- [ ] Is it worth the project size increase?

### Package Quality
- [ ] Weekly downloads: >10K
- [ ] GitHub stars: >1K
- [ ] Last commit: <6 months
- [ ] Open issues reasonable
- [ ] Maintainer active

### Security
- [ ] npm audit clean
- [ ] Snyk/Dependabot scan
- [ ] No known vulnerabilities
- [ ] Dependency chain small

### License
- [ ] MIT / Apache 2.0 / ISC (compatible)
- [ ] Not GPL (for commercial projects)
```

## 2.2 Package Comparison

```markdown
## Package Comparison: Date Library

| Criteria | date-fns | dayjs | moment |
|--------|----------|-------|--------|
| Size (gzip) | 13KB | 2KB | 72KB |
| Tree-shakeable | ✅ | ❌ | ❌ |
| Immutable | ✅ | ✅ | ❌ |
| TypeScript | ✅ | ✅ | ✅ |
| Maintenance | ✅ | ✅ | ⚠️ Deprecated |

**Decision:** dayjs (smallest, active maintenance)
```

---

# 3. Security Auditing

## 3.1 npm audit

```bash
# Security scan
npm audit

# Automatic fix (careful!)
npm audit fix

# Fix including breaking changes
npm audit fix --force  # ⚠️ DANGEROUS

# JSON format (for CI)
npm audit --json

# Production dependencies only
npm audit --omit=dev
```

## 3.2 Understanding Audit Report

```
┌───────────────┬──────────────────────────────────────────────────────┐
│ Critical      │ eval injection in lodash < 4.17.21                    │
| Package       │ lodash                                                |
| Severity      │ critical                                              |
| Vulnerable    │ <4.17.21                                              |
| Patched in    │ >=4.17.21                                             |
| Dependency of │ my-project > some-package > lodash                    |
└───────────────┴──────────────────────────────────────────────────────┘
```

## 3.3 Snyk Integration

```bash
# Snyk CLI install
npm install -g snyk

# Auth
snyk auth

# Test
snyk test

# Monitor (continuous)
snyk monitor

# Fix suggestions
snyk wizard
```

## 3.4 Audit in CI Pipeline

```yaml
# .github/workflows/security.yml
name: Security Audit

on:
  push:
    branches: [main]
  schedule:
    - cron: '0 0 * * 1'  # Every Monday

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: npm audit
        run: npm audit --audit-level=high
        
      - name: Snyk scan
        uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

---

# 4. Version Management

## 4.1 Semantic Versioning

```
MAJOR.MINOR.PATCH
  │      │     │
  │      │     └── Backward compatible bug fixes
  │      └──────── Backward compatible new features
  └─────────────── Breaking changes
```

## 4.2 Version Range Syntax

```json
{
  "dependencies": {
    "exact": "1.2.3",           // Exact version
    "patch": "~1.2.3",          // 1.2.x (>=1.2.3 <1.3.0)
    "minor": "^1.2.3",          // 1.x.x (>=1.2.3 <2.0.0) [DEFAULT]
    "any": "*",                 // Any (DANGEROUS!)
    "range": ">=1.2.3 <2.0.0",  // Explicit range
    "latest": "latest"          // Latest stable (DANGEROUS!)
  }
}
```

## 4.3 Recommended Approach

```json
{
  "dependencies": {
    // Production: More conservative
    "express": "^4.18.2",      // Minor updates OK
    "prisma": "~5.6.0",        // Only patch
    
    // Security-critical: Lock
    "jsonwebtoken": "9.0.2"    // Exact version
  },
  "devDependencies": {
    // Dev: More liberal
    "typescript": "^5.0.0",
    "eslint": "^8.0.0"
  }
}
```

---

# 5. Upgrade Strategy

## 5.1 Regular Minor Updates

```bash
# Show outdated packages
npm outdated

# Interactive update
npx npm-check -u

# Only patch/minor (safe)
npm update

# Update all packages to latest minor
npx npm-check-updates -u --target minor
npm install
```

## 5.2 Major Updates (Carefully!)

```markdown
## Major Update Checklist: package@X.0.0

### Preparation
- [ ] Read CHANGELOG
- [ ] Is there a migration guide?
- [ ] List breaking changes

### Execution
- [ ] Create branch
- [ ] Package update
- [ ] Fix type errors
- [ ] Fix runtime errors
- [ ] Update tests
- [ ] All tests pass

### Verification
- [ ] Smoke test
- [ ] Test critical paths
- [ ] Performance check
- [ ] Code review
```

## 5.3 Major Update Example

```bash
# 1. Create branch
git checkout -b upgrade/react-19

# 2. Package update
npm install react@19 react-dom@19

# 3. Check TypeScript warnings
npx tsc --noEmit

# 4. Run tests
npm test

# 5. Fix breaking changes
# ... code changes ...

# 6. Test again
npm test

# 7. Build
npm run build

# 8. Commit & PR
git commit -m "chore: upgrade react to v19"
```

---

# 6. Lock File Management

## 6.1 package-lock.json

```bash
# Install strictly from lock file
npm ci  # Use in CI/CD (instead of npm install)

# Regenerate lock file
rm package-lock.json
npm install

# Lock file integrity check
npm audit signatures
```

## 6.2 .npmrc Settings

```ini
# .npmrc
save-exact=true              # Exact versions by default
package-lock=true            # Always generate lock file
audit=true                   # Auto audit on install
fund=false                   # Hide funding messages
engine-strict=true           # Enforce engine requirements
```

---

# 7. Dependency Cleanup

## 7.1 Find Unused Packages

```bash
# Install depcheck
npm install -g depcheck

# Find unused packages
depcheck

# Result
Unused dependencies
* lodash
* moment

Unused devDependencies
* @types/express
```

## 7.2 Package Size Analysis

```bash
# Bundle size analysis
npx source-map-explorer dist/main.js

# Import cost (VS Code extension)
# Shows size of each import

# bundlephobia.com
# Check package sizes online
```

## 7.3 Cleanup Script

```bash
# Remove unnecessary packages
npm uninstall lodash moment

# Clean node_modules and reinstall
rm -rf node_modules
npm ci

# Clean cache
npm cache clean --force
```

---

# 8. Dependency Monitoring

## 8.1 Dependabot Config

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: npm
    directory: "/"
    schedule:
      interval: weekly
      day: monday
      time: "09:00"
    open-pull-requests-limit: 10
    versioning-strategy: increase
    labels:
      - dependencies
    ignore:
      - dependency-name: "*"
        update-types: ["version-update:semver-major"]
    groups:
      dev-dependencies:
        dependency-type: development
```

## 8.2 Renovate Config

```json
// renovate.json
{
  "extends": ["config:base"],
  "packageRules": [
    {
      "matchUpdateTypes": ["minor", "patch"],
      "automerge": true
    },
    {
      "matchUpdateTypes": ["major"],
      "labels": ["breaking-change"]
    }
  ],
  "schedule": ["every weekend"]
}
```

---

# 9. Checklist

### When Adding a Package
- [ ] Really necessary?
- [ ] Alternatives evaluated?
- [ ] Package quality sufficient?
- [ ] Security audit clean?
- [ ] License compatible?
- [ ] Bundle size acceptable?

### Regular Maintenance (Weekly)
- [ ] Run npm audit
- [ ] Review Dependabot/Renovate PRs
- [ ] Check outdated packages

### Major Upgrade
- [ ] Read CHANGELOG
- [ ] List breaking changes
- [ ] Test in branch
- [ ] Run full test suite
- [ ] Check performance

---

# 10. Don't List

❌ Do not use "*" or "latest" with npm install --save
❌ Do not add package-lock.json to .gitignore
❌ Do not run npm audit fix --force blindly
❌ Do not deploy major updates without testing
❌ Do not keep deprecated packages for long
❌ Do not commit node_modules

---

# 11. Must Do List

✅ Commit package-lock.json
✅ Use `npm ci` in CI (not npm install)
✅ Run weekly npm audit
✅ Use Dependabot/Renovate
✅ Separate branch for major updates
✅ Clean up unused packages
✅ Monitor bundle size

---

**Last Update:** December 2025
**Version:** 2.0
