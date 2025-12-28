---
description: Systematic debugging workflow for identifying and resolving issues
---

# Debug Workflow

## Description
Use this workflow when facing bugs or errors. It guides through reproducing the issue, isolating the root cause, testing hypotheses, applying fixes, and verifying solutions.

---

## Steps

1. **Reproduce the issue** - Gather exact error messages, steps to reproduce, environment details (OS, runtime version, browser if applicable), and note reproducibility (always, sometimes, rare).

2. **Understand the system** - Map data flow through components, identify expected vs actual behavior, and understand the context. For complex issues, call `/ultrathink` first for deep analysis.

3. **Isolate the problem** - Use binary search method to narrow down which part of the code contains the bug, create minimal reproduction case, and pinpoint the exact location.

4. **Form hypotheses** - List possible root causes with probability estimates, define test methods for each hypothesis, and systematically test each one.

5. **Apply the fix** - Implement the minimal change that addresses the root cause, ensure the fix doesn't break related functionality, and document why the fix works.

6. **Verify the solution** - Confirm the bug no longer reproduces, test related functionality still works, write regression tests to prevent recurrence, and run full test suite.

7. **Document findings** - Create post-mortem with root cause analysis, identify why it wasn't caught earlier, and recommend prevention strategies.

---

## Related Workflows
- Call `/ultrathink` for complex root cause analysis
- Call `/test` to write regression tests after fixing
