---
name: debugging
description: Systematic debugging guide. Root cause analysis, debugging methodologies and 2025 tools.
metadata:
  skillport:
    category: quality
    tags:
      - debugging
      - troubleshooting
      - root-cause-analysis
      - error-handling
---

# Debugging Skill - Systematic Error Correction

> Methodology for debugging with a systematic and scientific approach.
> Problem solving, root cause analysis, and debugging tools.

---

# 📋 Contents

1. [Debugging Cycle](#1-debugging-cycle)
2. [Phase 1: REPRODUCE](#2-phase-1-reproduce)
3. [Phase 2: UNDERSTAND](#3-phase-2-understand)
4. [Phase 3: ISOLATE](#4-phase-3-isolate)
5. [Phase 4: HYPOTHESIZE](#5-phase-4-hypothesize)
6. [Phase 5: TEST](#6-phase-5-test)
7. [Phase 6: FIX](#7-phase-6-fix)
8. [Phase 7: REFLECT](#8-phase-7-reflect)
9. [Debugging Tools](#9-debugging-tools)
10. [Checklist](#10-checklist)
11. [Don't List](#11-dont-list)
12. [Must Do List](#12-must-do-list)

---

# 1. Debugging Cycle

```
┌─────────────┐
│  REPRODUCE  │ ← Repeat the error consistently
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ UNDERSTAND  │ ← Understand the system and expected behavior
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   ISOLATE   │ ← Narrow down the problem to a specific area
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ HYPOTHESIZE │ ← List possible causes
└──────┬──────┘
       │
       ▼
┌─────────────┐
│    TEST     │ ← Test the hypotheses
└──────┬──────┘
       │
       ▼
┌─────────────┐
│     FIX     │ ← Fix and verify
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   REFLECT   │ ← Document what was learned
└─────────────┘
```

---

# 2. Phase 1: REPRODUCE

## 2.1 Reproduce the Error Consistently

```markdown
## Bug Reproduction Report

### Observed Behavior
- What is happening? [Detailed description]
- Error message: [Full error text]
- When did it start? [Date/commit]

### Steps to Reproduce
1. [Step 1]
2. [Step 2]
3. [Step 3]
→ Error occurs

### Environment Info
- OS: [Windows/Mac/Linux version]
- Node: [Version]
- Browser: [Chrome/Firefox + version]
- Dependencies: [Relevant package versions]

### Reproducibility
- [ ] Every time (100%)
- [ ] Often (~80%)
- [ ] Sometimes (~50%)
- [ ] Rarely (~10%)
- [ ] Not yet reproduced
```

## 2.2 Reproduction Hints

```typescript
// Deterministic test using Seed
Math.random = () => 0.5; // Fix Random

// Test by fixing date
jest.useFakeTimers();
jest.setSystemTime(new Date('2025-01-01'));

// Simulate network conditions
await page.route('**/*', route => route.abort()); // Offline
```

---

# 3. Phase 2: UNDERSTAND

## 3.1 Understand the System

```markdown
## System Map

### Relevant Components
1. [Component A] → [Task]
2. [Component B] → [Task]
3. [Component C] → [Task]

### Data Flow
```
User Input → API → Service → Database
     ↓
  Response ← Transform ← Query Result
```

### Expected Behavior vs Actual Behavior
| Step | Expected | Actual |
|------|----------|--------|
| Input | X | X ✅ |
| Process | Y | Z ❌ |
| Output | A | B ❌ |
```

## 3.2 5 Whys Technique

```markdown
## 5 Whys Analysis

**Problem:** User cannot login

1. **Why?** → API returns 401
2. **Why?** → Token is invalid
3. **Why?** → Token has expired
4. **Why?** → Token refresh not working
5. **Why?** → Refresh token endpoint changed but client not updated

**Root Cause:** API version updated but breaking change not handled in client
```

---

# 4. Phase 3: ISOLATE

## 4.1 Binary Search for Bug Finding

```markdown
## Isolation Strategy

### Divide and Conquer
1. Disable half of the system
2. Does the error persist?
   - Yes → Search in that half
   - No → Search in the other half
3. Repeat: divide the remaining half into two
```

```bash
# Git bisect to find faulty commit
git bisect start
git bisect bad HEAD           # Current is faulty
git bisect good v1.0.0        # This version was fine
# Git performs binary search automatically
git bisect run npm test       # Run automatic test
```

## 4.2 Minimal Reproduction

```typescript
// Extract minimal example from large app
// ❌ Do not debug with the whole app

// ✅ Create minimal repro
const minimalExample = () => {
  // Only the minimum code triggering the error
  const data = { id: null };
  return data.id.toString(); // TypeError is here!
};
```

---

# 5. Phase 4: HYPOTHESIZE

## 5.1 List Possible Causes

```markdown
## Hypothesis List

| # | Hypothesis | Probability | Test Method |
|---|---------|----------|--------------|
| 1 | Null pointer | 40% | Value check with Console.log |
| 2 | Race condition | 30% | Test by adding timeout |
| 3 | Cache stale | 20% | Test by clearing cache |
| 4 | API change | 10% | Check API response |

### Most Likely Hypothesis Should Be Tested First
→ Start: Hypothesis #1
```

## 5.2 Common Bug Patterns

| Pattern | Symptoms | Check |
|---------|------------|------------|
| **Null Reference** | TypeError: Cannot read | Is value undefined/null? |
| **Off-by-One** | Array out of bounds | Index calculation |
| **Race Condition** | Intermittent failure | Async ordering |
| **Memory Leak** | Slow over time | Is cleanup performed? |
| **Infinite Loop** | Freeze/hang | Loop condition |
| **Wrong Scope** | Unexpected value | Closure/scope |
| **Type Coercion** | `'5' + 5 = '55'` | Strict equality |

---

# 6. Phase 5: TEST

## 6.1 Debugging Tools

```typescript
// 1. Console methods
console.log('Value:', value);
console.table(arrayData);
console.group('Section');
console.trace('Stack trace');
console.time('operation');
// ... operation
console.timeEnd('operation');

// 2. Debugger statement
function processData(data) {
  debugger; // Breakpoint
  return transform(data);
}

// 3. Conditional breakpoint (in DevTools)
// Right-click on line number → Add conditional breakpoint
// Condition: user.role === 'admin'
```

## 6.2 Node.js Debugging

```bash
# Node Inspector
node --inspect src/index.js
# Chrome: chrome://inspect

# Node Inspector with break
node --inspect-brk src/index.js

# VS Code launch.json
{
  "type": "node",
  "request": "launch",
  "name": "Debug",
  "program": "${workspaceFolder}/src/index.js",
  "skipFiles": ["<node_internals>/**"]
}
```

## 6.3 Network Debugging

```typescript
// Fetch/XHR intercepting
const originalFetch = window.fetch;
window.fetch = async (...args) => {
  console.log('Fetch:', args);
  const response = await originalFetch(...args);
  console.log('Response:', response.status);
  return response;
};

// Axios interceptor
axios.interceptors.request.use(config => {
  console.log('Request:', config);
  return config;
});

axios.interceptors.response.use(
  response => {
    console.log('Response:', response);
    return response;
  },
  error => {
    console.error('Error:', error);
    return Promise.reject(error);
  }
);
```

---

# 7. Phase 6: FIX

## 7.1 Fix Strategy

```markdown
## Fix Plan

### Root Cause
[Clearly state the root cause]

### Proposed Fix
[Explain the fix approach]

### Code Changes
```diff
- const value = data.item.value;
+ const value = data?.item?.value ?? 'default';
```

### Verification
- [ ] Bug no longer occurs
- [ ] No new bug created (regression)
- [ ] Test written
- [ ] Edge cases checked
```

## 7.2 Post-Fix Test

```typescript
// Write regression test
test('should handle null item in data', () => {
  const data = { item: null };
  expect(() => processData(data)).not.toThrow();
  expect(processData(data)).toBe('default');
});

test('should handle missing item property', () => {
  const data = {};
  expect(() => processData(data)).not.toThrow();
});
```

---

# 8. Phase 7: REFLECT

## 8.1 Post-Mortem Documentation

```markdown
## Bug Post-Mortem

### Summary
[Brief summary of the error]

### Timeline
- [Date] Error reported
- [Date] Root cause found
- [Date] Fix deployed

### Root Cause
[Detailed explanation]

### Impact
- Number of affected users: [X]
- Downtime: [Y minutes]
- Revenue impact: [If any]

### Lessons Learned
1. [Learned 1]
2. [Learned 2]

### Prevention
To prevent such errors:
1. [ ] [Action 1]
2. [ ] [Action 2]
```

---

# 9. Debugging Tools

## 9.1 Static Analysis

```bash
# Find potential errors with ESLint
npx eslint . --ext .ts,.tsx

# TypeScript type checking
npx tsc --noEmit

# SonarQube/SonarLint
# VS Code extension or CI integration
```

## 9.2 Runtime Analysis

```typescript
// Performance profiling
console.profile('myFunction');
myFunction();
console.profileEnd('myFunction');

// Memory snapshot
// Chrome DevTools → Memory → Take heap snapshot

// React DevTools Profiler
// Components tab → Profiler → Record
```

## 9.3 Logging Best Practices

```typescript
// Structured logging
import pino from 'pino';

const logger = pino({
  level: process.env.LOG_LEVEL || 'info',
});

logger.info({ userId, action: 'login' }, 'User logged in');
logger.error({ err, userId }, 'Login failed');

// Log levels
logger.trace('Very detailed');
logger.debug('Debugging info');
logger.info('General info');
logger.warn('Warning');
logger.error('Error');
logger.fatal('Fatal error');
```

---

# 10. Checklist

In every debugging session:

- [ ] Error reproduced consistently
- [ ] System and expected behavior understood
- [ ] Problem isolated
- [ ] Hypotheses listed and prioritized
- [ ] Most likely hypothesis tested first
- [ ] Root cause found
- [ ] Fix applied and verified
- [ ] Regression test written
- [ ] Post-mortem documented

---

# 11. Don't List

❌ Do not try to fix by guessing (print debugging loop)
❌ Do not change multiple things at once
❌ Do not fix without understanding the root cause
❌ Do not open PR without writing tests
❌ Do not commit debugging code (console.log)
❌ Do not swallow errors silently (empty catch)
❌ Do not assume "fixed" with just a timeout

---

# 12. Must Do List

✅ Reproduce first, then debug
✅ Isolate with binary search
✅ Write down and test hypotheses
✅ Make one change at a time
✅ Write a test for every fix
✅ Document lessons learned
✅ Read the stack trace carefully
✅ Use version control (git stash, bisect)

---

**Last Update:** December 2025
**Version:** 2.0
