---
name: documentation
description: Technical and code documentation guide. Docs-as-code, API documentation, and 2025 best practices.
metadata:
  skillport:
    category: operations
    tags:
      - documentation
      - technical-writing
      - api-docs
      - readme
---

# Documentation Skill

> Guide for writing effective technical documentation.
> Docs-as-code approach, API documentation, and maintainable docs.

---

## 🎯 Documentation Types

| Type | Target Audience | Purpose |
|-----|-------------|------|
| **README** | First-time viewers | Quick start, overview |
| **API Docs** | Developers | Endpoint usage |
| **Code Comments** | Maintainers | Why, not what |
| **Architecture** | Team | System design |
| **Changelog** | Users | Change tracking |
| **Runbook** | Ops/SRE | Operational procedures |

---

## 📏 README Best Practices

### README Template

```markdown
# Project Name

> Explain what the project does in one sentence.

## Features
- ✅ Feature 1
- ✅ Feature 2

## Quick Start
### Prerequisites
- Node.js 20+

### Installation
```bash
npm install
cp .env.example .env
npm run dev
```
```

### README Rules

- **Clear Title**: Make it clear what the project is.
- **Short Quick Start**: Should be runnable in 5 minutes.
- **Copy-paste ready**: Code blocks should work directly.
- **Use Visuals**: Badges, screenshots, diagrams.
- **Keep it updated**: No outdated info.

---

## 💻 Code Documentation

### JSDoc/TSDoc

```typescript
/**
 * Calculates the total price including tax.
 * 
 * @param amount - The base amount before tax
 * @param taxRate - Tax rate as a decimal (e.g., 0.18 for 18%)
 * @returns The total amount including tax
 */
function calculateTotal(amount: number, taxRate: number): number {
  return amount * (1 + taxRate);
}
```

### Comment Best Practices

- **❌ WRONG: What** (code already says it)
- **✅ CORRECT: Why** (explains why it was done this way)
- **✅ CORRECT: Business Logic** (e.g., "Premium users get discount as per campaign XYZ")
- **✅ CORRECT: Warning** (e.g., "⚠️ Do not change order of middleware!")

---

## 📡 API Documentation

### API Doc Template

```markdown
## Create User
Creates a new user account.

### Endpoint
`POST /api/v1/users`

### Request Body
```json
{
  "email": "user@example.com",
  "password": "SecurePass123!",
  "name": "John Doe"
}
```
```

---

## 📋 Changelog

### Keep a Changelog Format

- **Added**: New features.
- **Changed**: Changes in existing functionality.
- **Fixed**: Bug fixes.
- **Security**: In case of vulnerabilities.

---

## 🏗️ Architecture Documentation

### Architecture Decision Records (ADR)

- **Status**: Accepted
- **Context**: Why we needed a decision.
- **Decision**: What we decided.
- **Consequences**: Positive/Negative results.

---

## ✅ Checklist

### README
- [ ] Working quick start
- [ ] Tested code examples
- [ ] Links are working

### API Docs
- [ ] All endpoints documented
- [ ] Request/response examples present
- [ ] Error codes explained

### Code Comments
- [ ] "Why" is explained, not "what"
- [ ] Business logic documented
- [ ] TODOs contain context

---

## 🔴 Don't List

❌ Do not write obvious comments
❌ Do not leave without updating
❌ Do not use jargon without explanation
❌ Do not document only the happy path

---

## ✅ Must Do List

✅ Start with a README
✅ Document API with OpenAPI/Swagger
✅ Explain "why" in code
✅ Keep a Changelog
✅ Write ADRs
✅ Update regularly
✅ Provide examples
✅ Test the code in documentation

---

**Last Update:** December 2025
**Version:** 1.0
