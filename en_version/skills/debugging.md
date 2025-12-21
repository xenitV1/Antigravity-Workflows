---
name: debugging
description: Systematic debugging guide. Root cause analysis, debugging methodologies, and 2025 tools.
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

## 🎯 Debugging Cycle

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

## 📏 Phase 1: REPRODUCE

### Reproduce the Error Consistently

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
- OS, Node, Browser versions
- Relevant dependencies

### Reproducibility
- [ ] Every time (100%)
- [ ] Often (~80%)
- [ ] Sometimes (~50%)
- [ ] Rarely (~10%)
- [ ] Not yet reproduced
```

---

## 🔍 Phase 2: UNDERSTAND

### 5 Whys Technique

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

## 🎯 Phase 3: ISOLATE

### Binary Search for Bug Finding

```bash
# Git bisect to find faulty commit
git bisect start
git bisect bad HEAD           # Current is faulty
git bisect good v1.0.0        # This version was fine
# Git performs binary search automatically
git bisect run npm test       # Run automatic test
```

---

## 💡 Phase 4: HYPOTHESIZE

### Common Bug Patterns

| Pattern | Symptoms | Check |
|---------|------------|------------|
| **Null Reference** | TypeError: Cannot read | Is value undefined/null? |
| **Off-by-One** | Array out of bounds | Index calculation |
| **Race Condition** | Intermittent failure | Async ordering |
| **Memory Leak** | Slow over time | Is cleanup performed? |

---

## 🧪 Phase 5: TEST

### Debugging Tools

```typescript
// 1. Console methods
console.table(arrayData);
console.trace('Stack trace');
console.time('operation');

// 2. Debugger statement
function processData(data) {
  debugger; // Breakpoint
  return transform(data);
}
```

---

## 🔧 Phase 6: FIX

### Fix post-test

```typescript
// Write a regression test
test('should handle null item in data', () => {
  const data = { item: null };
  expect(() => processData(data)).not.toThrow();
  expect(processData(data)).toBe('default');
});
```

---

## 📝 Phase 7: REFLECT

### Post-Mortem Documentation

```markdown
## Bug Post-Mortem

### Summary
[Brief summary of the error]

### Root Cause
[Detailed explanation]

### Lessons Learned
1. [Learned 1]
2. [Learned 2]

### Prevention
To prevent such errors:
1. [ ] [Action 1]
```

---

## ✅ Checklist

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

## 🔴 Don't List

❌ Do not try to fix by guessing (print debugging loop)
❌ Do not change multiple things at once
❌ Do not fix without understanding the root cause
❌ Do not open PR without writing tests
❌ Do not commit debugging code (console.log)
❌ Do not swallow errors silently (empty catch)
❌ Do not assume "fixed" with just a timeout

---

## ✅ Must Do List

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
**Version:** 1.0
