---
name: multi-file-sync
description: Multi-file change and context preservation guide. Atomic changes, refactoring across files, and safe migration.
metadata:
  skillport:
    category: operations
    tags:
      - multi-file
      - refactoring
      - migration
      - context
---

# Multi-File Sync Skill

> Guide for changing multiple files safely and consistently.
> Atomic steps, context preservation, and rollback strategies.

---

## 📏 Core Principles

### 1. Atomic Changes

Every commit should contain only ONE logical change.

- **✅ CORRECT**: 
  - Commit 1: "rename: userId -> customerId in types"
  - Commit 2: "rename: userId -> customerId in services"
- **❌ INCORRECT**: 
  - Commit 1: "refactor everything" (all changes in one commit)

### 2. Dependency Order

Follow the direction of dependencies:

1. Types/Interfaces (most independent)
2. Utilities/Helpers
3. Services/Repositories
4. Controllers/Handlers
5. Routes/Entry points
6. Tests
7. Documentation

---

## 🔄 Multi-File Change Process

### Phase 1: Analysis and Planning

Document the impact analysis, affected files, and dependency graph.

### Phase 2: Preparation

Create a clean branch, verify working state (tests, build, lint), and backup/stash.

### Phase 3: Step-by-Step Implementation

1. Update Type definitions -> Commit.
2. Update Services -> Commit.
3. Update Controllers -> Commit.
4. Update Routes -> Commit.
5. Update Tests -> Commit.

---

## 🛠️ Tools and Techniques

### IDE Refactoring (Rename Symbol)
Automates updates for all occurrences, but only for TS/JS references. It won't find string occurrences.

### Grep / Find and Replace
Use `grep` to find all occurrences and `sed` for replacement (with caution!). Always preview with `grep` first.

### TypeScript Auto-detection
Use `npx tsc --noEmit` to find type errors after changes.

---

## 🔍 Context Preservation

### Progress Tracker
Always maintain a checklist of completed and pending steps, current step details, and any issues or legacy compatibility notes.

---

## 🔙 Rollback Strategies

- **Git Revert**: Revert specific commits or ranges.
- **Partial Rollback**: Bring specific files back to their previous state using `git checkout`.

---

## ✅ Checklist

- [ ] Affected files listed
- [ ] Dependency order determined
- [ ] Tests and type check pass at every step
- [ ] Separate commits made for each atomic change
- [ ] Build and lint pass after completion
- [ ] Documentation updated

---

## 🔴 Don't List

❌ Do not make all changes in a single commit
❌ Do not proceed without running tests
❌ Do not skip the dependency order
❌ Do not rely solely on manual string replacement
❌ Do not perform DB rename and code change in the same deployment

---

## ✅ Must Do List

✅ Document impact analysis
✅ Follow dependency order
✅ Run tests after every step
✅ Use IDE refactoring tools
✅ Ensure Zero TypeScript errors
✅ Have a rollback plan

---

**Last Update:** December 2025
**Version:** 1.0
