---
description: Code review workflow with systematic quality checks for security and maintainability
---

# Review Workflow

## Description
Use this workflow to review code changes and pull requests. It ensures code meets project standards for quality, security, and maintainability through systematic checks.

---

## Steps

1. **First pass - syntax and structure** - Quick scan for obvious issues: check for syntax errors, proper imports, unused variables, console.log statements, meaningful variable names, focused functions, and logical file organization.

2. **Second pass - quality and security** - Deeper analysis: verify type safety (no `any` types, proper interfaces, null/undefined handled), error handling (try-catch, error propagation, user-friendly messages), and security (no hardcoded secrets, input validation, SQL injection prevention, XSS prevention).

3. **Edge cases and logic** - Check boundary conditions (empty arrays/null inputs, zero/negative numbers, maximum limits) and logic review (business logic correctness, race conditions prevented, state mutations intentional).

4. **Performance and maintainability** - Verify performance (no N+1 queries, expensive operations memoized, no unnecessary re-renders) and maintainability (self-documenting code, comments explain why not what, easy to modify).

5. **Generate review summary** - Provide verdict (Approve/Request Changes/Needs Discussion), list must-fix issues, should-fix improvements, and nice-to-have suggestions. Include positive feedback on what was done well.

---

## Related Workflows
- Call `/implement` after review passes
- Call `/test` to ensure tests cover issues found
