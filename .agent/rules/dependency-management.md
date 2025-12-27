# Dependency Management Rule

## Activation
- **Mode:** Glob
- **Glob Pattern:** `package.json, *.lock, yarn.lock, pnpm-lock.yaml`
- **Description:** Package and dependency management guide. Security auditing, version management, and upgrade strategies. Auto-activates for package files.

---

## Core Principles

| Principle | Description |
|-----------|-------------|
| Minimize Dependencies | Don't add unnecessary packages |
| Lock Versions | Commit package-lock.json |
| Audit Regularly | Weekly security check |
| Update Strategically | Major updates carefully |
| Document Decisions | Why this package? |

---

## Before Adding a Package

### Necessity Check
- [ ] Native solution exists? (built-in modules)
- [ ] Can be done with simple util?
- [ ] Worth the bundle size?

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
- [ ] Small dependency chain

### License
- [ ] MIT / Apache 2.0 / ISC (compatible)
- [ ] Not GPL (for commercial projects)

---

## Security Auditing

### npm audit
```bash
# Security scan
npm audit

# Auto fix (careful!)
npm audit fix

# JSON format (for CI)
npm audit --json

# Production only
npm audit --omit=dev
```

### Snyk Integration
```bash
npm install -g snyk
snyk auth
snyk test
snyk monitor
```

### CI Pipeline
```yaml
- name: npm audit
  run: npm audit --audit-level=high

- name: Snyk scan
  uses: snyk/actions/node@master
```

---

## Version Management

### Semantic Versioning
```
MAJOR.MINOR.PATCH
  |      |     |
  |      |     +-- Backward compatible bug fixes
  |      +-------- Backward compatible new features
  +--------------- Breaking changes
```

### Version Range Syntax
```json
{
  "exact": "1.2.3",           // Exactly this version
  "patch": "~1.2.3",          // 1.2.x (>=1.2.3 <1.3.0)
  "minor": "^1.2.3",          // 1.x.x (>=1.2.3 <2.0.0) [DEFAULT]
  "any": "*",                 // Any (DANGEROUS!)
  "latest": "latest"          // Latest stable (DANGEROUS!)
}
```

### Recommended Approach
```json
{
  "dependencies": {
    "express": "^4.18.2",      // Minor updates OK
    "prisma": "~5.6.0",        // Patch only
    "jsonwebtoken": "9.0.2"    // Exact (security-critical)
  }
}
```

---

## Upgrade Strategy

### Regular Minor Updates
```bash
# Show outdated
npm outdated

# Interactive update
npx npm-check -u

# Safe update (patch/minor)
npm update

# All to latest minor
npx npm-check-updates -u --target minor
npm install
```

### Major Updates (Careful!)
```markdown
## Major Update Checklist

### Preparation
- [ ] Read CHANGELOG
- [ ] Check migration guide
- [ ] List breaking changes

### Implementation
- [ ] Create branch
- [ ] Update package
- [ ] Fix type errors
- [ ] Fix runtime errors
- [ ] Update tests

### Verification
- [ ] Smoke test
- [ ] Performance check
- [ ] Code review
```

---

## Lock File Management

```bash
# Install from lock file (use in CI/CD)
npm ci

# Regenerate lock file
rm package-lock.json
npm install

# Integrity check
npm audit signatures
```

### .npmrc Settings
```ini
save-exact=true         # Exact versions by default
package-lock=true       # Always generate lock file
audit=true              # Auto audit on install
engine-strict=true      # Enforce engine requirements
```

---

## Dependency Cleanup

### Find Unused Packages
```bash
npm install -g depcheck
depcheck

# Output:
# Unused dependencies: lodash, moment
# Unused devDependencies: @types/express
```

### Bundle Size Analysis
```bash
npx source-map-explorer dist/main.js
# Check bundlephobia.com
```

### Cleanup
```bash
npm uninstall lodash moment
rm -rf node_modules && npm ci
npm cache clean --force
```

---

## Dependency Monitoring

### Dependabot Config
```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: npm
    directory: "/"
    schedule:
      interval: weekly
    ignore:
      - dependency-name: "*"
        update-types: ["version-update:semver-major"]
```

### Renovate Config
```json
{
  "extends": ["config:base"],
  "packageRules": [
    {
      "matchUpdateTypes": ["minor", "patch"],
      "automerge": true
    }
  ]
}
```

---

## Checklist

### When Adding Package
- [ ] Really necessary?
- [ ] Alternatives evaluated?
- [ ] Quality sufficient?
- [ ] Security audit clean?
- [ ] License compatible?
- [ ] Bundle size acceptable?

### Regular Maintenance (Weekly)
- [ ] Run npm audit
- [ ] Review Dependabot PRs
- [ ] Check outdated packages

### Major Upgrade
- [ ] Read CHANGELOG
- [ ] List breaking changes
- [ ] Test in branch
- [ ] Full test suite pass
- [ ] Performance check

---

## Don't List

- Use "*" or "latest" versions
- Add package-lock.json to .gitignore
- Run npm audit fix --force blindly
- Deploy major updates without testing
- Keep deprecated packages long
- Commit node_modules

---

## Must Do List

- Commit package-lock.json
- Use `npm ci` in CI (not npm install)
- Run npm audit weekly
- Use Dependabot/Renovate
- Separate branch for major updates
- Clean unused packages
- Monitor bundle size

---

**Version:** 2.0 (Antigravity Rule)
