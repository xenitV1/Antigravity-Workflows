---
description: Test generation and execution workflow following test pyramid principles
---

# Test Workflow

## Description
Use this workflow when creating or running tests. It generates comprehensive tests following the test pyramid (70% unit, 20% integration, 10% E2E) and ensures adequate coverage.

---

## Steps

1. **Identify test scope** - Determine which components or features need testing. Classify test types needed: unit tests (functions, utils), integration tests (API, services), or E2E tests (user flows).

2. **Write unit tests** - Follow AAA pattern (Arrange, Act, Assert). Cover happy paths and edge cases (empty inputs, null values, boundary conditions).

3. **Write integration tests** - Test API endpoints with various request scenarios, valid and invalid inputs, and verify response codes and data structures.

4. **Run coverage analysis** - Execute tests with coverage reporting. Check overall coverage >= 80%, critical paths >= 95%, and new code = 100%.

5. **Ensure test quality** - Verify tests are independent (can run in any order), deterministic (no flaky tests), with proper cleanup and mocked external services.

6. **Run test suite** - Execute all tests and ensure they pass. Fix any failures before proceeding.

---

## Related Workflows
- Call `/implement` for tests before implementation
- Call `/debug` to write regression tests after fixes
