---
description: Feature and code implementation workflow with TDD approach and quality checks
---

# Implement Workflow

## Description
Use this workflow when building new features or making code changes. It guides through planning, test-first development (TDD), implementation, quality checks, and self-review.

---

## Steps

1. **Plan the implementation** - For non-trivial features, call `/plan` first. Define implementation scope, list files to modify and create, and identify any new dependencies needed.

2. **Write tests first (TDD)** - Create test cases before implementation covering happy paths, edge cases, and error conditions. Follow AAA pattern (Arrange, Act, Assert).

3. **Implement the feature** - Follow established patterns: TypeScript strict mode compliant, no `any` types, proper error handling, input validation, no hardcoded secrets, and OWASP Top 10 security considerations.

4. **Run quality checks** - Execute `npx tsc --noEmit` for type check, `npx eslint .` for linting, `npx prettier --check .` for formatting, and `npm test` to verify all tests pass.

5. **Perform self-review** - Verify correctness (solves the problem), completeness (edge cases handled), clarity (code is readable), and consistency (follows project patterns).

6. **Iterate if needed** - If any quality check fails or review reveals issues, fix and re-run checks until all pass.

7. **Mark as ready for review** - Once all checks pass and self-review is complete, the implementation is ready for code review.

---

## Related Workflows
- Call `/plan` for complex feature planning
- Call `/test` for comprehensive testing
- Call `/review` for code review
