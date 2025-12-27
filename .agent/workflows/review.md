# Review Workflow

## Description
Code review workflow with systematic quality checks. Ensures code meets project standards for quality, security, and maintainability.

---

## Invocation
```
/review [file or PR reference]
```

---

## Steps

### Step 1: First Pass - Syntax & Structure

Quick scan for obvious issues:

```markdown
## First Review Pass

### Syntax Check
- [ ] No syntax errors
- [ ] Proper imports
- [ ] No unused variables
- [ ] No console.log statements

### Structure Check
- [ ] Meaningful variable names
- [ ] Functions are focused (single responsibility)
- [ ] File organization makes sense
```

### Step 2: Second Pass - Quality & Security

Deeper analysis:

```markdown
## Second Review Pass

### Type Safety
- [ ] No `any` types
- [ ] Proper interface definitions
- [ ] Null/undefined handled

### Error Handling
- [ ] Try-catch where needed
- [ ] Errors properly propagated
- [ ] User-friendly error messages

### Security
- [ ] No hardcoded secrets
- [ ] Input validation present
- [ ] SQL injection prevented
- [ ] XSS prevention in place
```

### Step 3: Edge Cases & Logic

```markdown
## Edge Case Analysis

### Boundary Conditions
- [ ] Empty arrays/null inputs handled
- [ ] Zero/negative numbers handled
- [ ] Maximum limits considered

### Logic Review
- [ ] Business logic correct
- [ ] Race conditions prevented
- [ ] State mutations intentional
```

### Step 4: Performance & Maintainability

```markdown
## Performance Check

- [ ] No N+1 queries
- [ ] Expensive operations memoized
- [ ] No unnecessary re-renders

## Maintainability Check

- [ ] Code is self-documenting
- [ ] Complex logic has comments (why, not what)
- [ ] Easy to modify in future
```

### Step 5: Review Summary

```markdown
## Review Summary

### Verdict: [Approve / Request Changes / Needs Discussion]

### Must Fix
1. [Critical issue 1]
2. [Critical issue 2]

### Should Fix
1. [Important improvement 1]

### Nice to Have
1. [Suggestion 1]

### Positive Feedback
- [What was done well]
```

---

## Output

Structured review report with:
- Pass/Fail for each category
- Issues categorized by severity
- Actionable feedback
- Positive recognition

---

## Related Workflows
- `/implement` - After review passes
- `/test` - Ensure tests cover issues found
