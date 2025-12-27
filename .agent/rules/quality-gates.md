# Quality Gates - Code Quality Standards

## Activation
- **Mode:** Always On
- **Description:** Mandatory quality checks applied to every code change. These rules are always active and cannot be bypassed.

---

## Mandatory Checks (After EVERY Code Change)

### 1. Static Analysis
```bash
# TypeScript - Type safety check
npx tsc --noEmit

# ESLint - Code quality check
npx eslint .

# Prettier - Format check
npx prettier --check .
```

### 2. Test Verification
```bash
# Run test suite
npm test

# Check coverage (minimum 80%)
npm run test:coverage
```

---

## 2x Code Review Rule

Every code change MUST be reviewed TWICE:

### First Review (Syntax Check)
- [ ] No syntax errors
- [ ] Variable names are meaningful
- [ ] Imports are correct and used
- [ ] No unused variables
- [ ] No console.log statements

### Second Review (Quality Check)
- [ ] Edge cases handled
- [ ] Error handling present
- [ ] Type safety ensured (no `any`)
- [ ] Security best practices applied
- [ ] Performance considered

---

## TypeScript Standards

### Strict Mode Required
```json
{
  "strict": true,
  "noImplicitAny": true,
  "strictNullChecks": true,
  "noImplicitReturns": true
}
```

### Forbidden Patterns
- `any` type is **FORBIDDEN**
- Use `unknown` for uncertain types with type guards
- Always define interfaces/types for data structures

---

## Security Checklist

- [ ] No hardcoded secrets in code
- [ ] Environment variables validated
- [ ] Input validation present (Zod/Yup)
- [ ] SQL injection prevented (parameterized queries)
- [ ] XSS prevention in place
- [ ] Authentication/Authorization checked
- [ ] Rate limiting configured

---

## Pre-Commit Checklist

Before ANY commit:

```markdown
## Pre-Commit Verification

### Code Quality
- [ ] ESLint passes (no errors)
- [ ] TypeScript passes (no type errors)
- [ ] Prettier formatted
- [ ] Code reviewed 2x

### Security
- [ ] No secrets in code
- [ ] Input validation added
- [ ] Error handling present

### Testing
- [ ] Tests pass
- [ ] New tests written for new code
- [ ] Edge cases covered

### Cleanup
- [ ] No console.log statements
- [ ] No unused imports
- [ ] No commented-out code
- [ ] No TODO without ticket reference
```

---

## Post-Operation Report

After completing any code task, provide:

```markdown
## Quality Report

### Checks Performed
- [ ] ESLint: [Pass/Fail]
- [ ] TypeScript: [Pass/Fail]
- [ ] Tests: [Pass/Fail]
- [ ] Review: [1st/2nd complete]

### Issues Found
[List any issues and resolutions]

### Confidence
Code quality confidence: [%]
```

---

## Violation Consequences

> **WARNING:** Skipping quality checks is a SEVERE VIOLATION.

If quality gates are not passed:
1. Do NOT proceed with the task
2. Fix all issues first
3. Re-run checks until all pass
4. Document any exceptions

---

**Version:** 1.1 (Always On Rule)
