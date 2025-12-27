# Documentation Rule

## Activation
- **Mode:** Glob
- **Glob Pattern:** `*.md, README*, CHANGELOG*, docs/**, wiki/**`
- **Description:** Technical documentation and code documentation guide. Docs-as-code approach, API documentation, and maintainable documentation practices.

---

## Documentation Types

| Type | Audience | Purpose |
|------|----------|---------|
| README | First-time viewers | Quick start, overview |
| API Docs | Developers | Endpoint usage |
| Code Comments | Maintainers | Why, not what |
| Architecture | Team | System design |
| Changelog | Users | Change tracking |
| Runbook | Ops/SRE | Operational procedures |

---

## README Best Practices

### Template
```markdown
# Project Name

> One sentence explaining what this project does.

![Build](https://img.shields.io/badge/build-passing-green)
![Coverage](https://img.shields.io/badge/coverage-95%25-green)

## Features

- Feature 1
- Feature 2

## Quick Start

### Prerequisites
- Node.js 20+

### Installation
```bash
npm install
npm run dev
```

## Documentation

- [API Reference](./docs/api.md)
- [Architecture](./docs/architecture.md)

## License
MIT
```

### README Rules

| Rule | Description |
|------|-------------|
| Clear title | What it is immediately clear |
| Quick start short | Running in 5 minutes |
| Copy-paste ready | Code blocks work directly |
| Use visuals | Badges, screenshots, diagrams |
| Keep updated | No outdated info |

---

## Code Documentation

### JSDoc/TSDoc
```typescript
/**
 * Calculates total price including tax.
 *
 * @param amount - Base amount before tax
 * @param taxRate - Tax rate as decimal (0.18 = 18%)
 * @returns Total amount including tax
 *
 * @example
 * const total = calculateTotal(100, 0.18); // 118
 *
 * @throws {Error} If amount is negative
 */
function calculateTotal(amount: number, taxRate: number): number {
  if (amount < 0) throw new Error('Amount cannot be negative');
  return amount * (1 + taxRate);
}
```

### Comment Best Practices
```typescript
// WRONG: What (code already says this)
// Increment counter by 1
counter++;

// WRONG: Obvious
// Loop through users
for (const user of users) { }

// CORRECT: Why
// Using setTimeout to debounce frequent updates
setTimeout(() => saveChanges(), 500);

// CORRECT: Business logic
// Premium users get 20% discount per JIRA-1234
if (user.isPremium && order.total > 100) {
  discount = 0.20;
}

// CORRECT: Warning
// Do NOT change middleware order!
// Authentication must run before authorization
app.use(authenticate);
app.use(authorize);

// CORRECT: TODO with context
// TODO(john): Refactor after Q1 - JIRA-5678
```

---

## API Documentation

### OpenAPI/Swagger
```yaml
openapi: 3.0.3
info:
  title: User API
  version: 1.0.0

paths:
  /users:
    get:
      summary: List all users
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserList'
```

### Endpoint Documentation
```markdown
## Create User

`POST /api/v1/users`

### Request

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| email | string | Yes | Valid email |
| password | string | Yes | Min 8 chars |

### Response (201)
```json
{
  "success": true,
  "data": { "id": "uuid", "email": "user@example.com" }
}
```

### Error (400)
```json
{
  "success": false,
  "error": { "code": "VALIDATION_ERROR", "message": "Invalid email" }
}
```
```

---

## Changelog

### Keep a Changelog Format
```markdown
# Changelog

## [Unreleased]

### Added
- New user profile page

## [1.2.0] - 2025-01-15

### Added
- OAuth2 authentication

### Changed
- Updated dashboard layout

### Fixed
- Login button on mobile

### Security
- Patched XSS vulnerability
```

### Conventional Commits
```bash
feat(auth): add Google OAuth support
fix(api): handle null response
docs(readme): add installation instructions
refactor(utils): simplify date formatting
chore(deps): update dependencies

# Breaking change
feat(api)!: change response format
BREAKING CHANGE: Response now wrapped in 'data' object
```

---

## Architecture Documentation

### C4 Model
```markdown
## System Context (Level 1)
User -> Web App -> API -> Database

## Container Diagram (Level 2)
React SPA -> API Gateway -> [Auth, Users, Orders] -> PostgreSQL
```

### ADR Template
```markdown
# ADR-002: API Authentication

## Status
Accepted

## Context
Need to authenticate API requests.

## Decision
JWT tokens with refresh token rotation.

## Consequences
+ Stateless, scalable
- Token revocation complex
```

---

## Writing Guidelines

### Audience-First

| Audience | Approach |
|----------|----------|
| Beginners | No assumptions, every step, screenshots |
| Intermediate | Basic knowledge assumed, implementation focus |
| Experts | Full context assumed, edge cases, benchmarks |

### Style Guide

| Do | Don't |
|----|-------|
| Active voice | Passive voice |
| Short sentences | Long paragraphs |
| Numbered lists for steps | Prose for instructions |
| Show with examples | Only describe |
| Update regularly | Leave outdated |

---

## Checklist

### README
- [ ] One-line description
- [ ] Quick start works
- [ ] Code examples tested
- [ ] Links work
- [ ] Badges current

### API Docs
- [ ] All endpoints documented
- [ ] Request/response examples
- [ ] Error codes explained
- [ ] Authentication explained
- [ ] cURL examples present

### Code Comments
- [ ] Why explained, not what
- [ ] Business logic documented
- [ ] Edge cases explained
- [ ] TODOs have context

---

## Don't List

- Obvious comments
- Leave outdated
- Use jargon without explanation
- Write once, forget
- Document only happy path

---

## Must Do List

- Start with README
- Document API with OpenAPI
- Explain "why" in code
- Keep changelog
- Write ADRs
- Update regularly
- Provide examples
- Test documentation code

---

**Version:** 2.0 (Antigravity Rule)
