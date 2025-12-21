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

# 📋 Contents

1. [Core Principles](#1-core-principles)
2. [Multi-File Change Process](#2-multi-file-change-process)
3. [Tools and Techniques](#3-tools-and-techniques)
4. [Context Preservation (Context Keeping)](#4-context-preservation-context-keeping)
5. [Dangerous Situations](#5-dangerous-situations)
6. [Rollback Strategies](#6-rollback-strategies)
7. [Checklist](#7-checklist)
8. [Don't List](#8-dont-list)
9. [Must Do List](#9-must-do-list)

---

# 1. Core Principles

## 1.1 Atomic Changes

```markdown
## Atomic Change Rule

Every commit should contain only ONE logical change:

✅ CORRECT:
- Commit 1: "rename: userId -> customerId in types"
- Commit 2: "rename: userId -> customerId in services"
- Commit 3: "rename: userId -> customerId in controllers"

❌ INCORRECT:
- Commit 1: "refactor everything" (all changes in one commit)
```

## 1.2 Test-First Approach

```bash
# Run tests before and after each step
npm test

# Make step
# ... change ...

# Test again
npm test

# If passed, commit
git commit -m "step X: description"
```

## 1.3 Dependency Order

```markdown
## Change Order

Follow the direction of dependencies:

1. Types/Interfaces (most independent)
2. Utilities/Helpers
3. Services/Repositories
4. Controllers/Handlers
5. Routes/Entry points
6. Tests
7. Documentation
```

---

# 2. Multi-File Change Process

## 2.1 Phase 1: Analysis and Planning

```markdown
## Change Plan

### Impact Analysis
Change: [What will change]

### Affected Files
1. `src/types/user.ts` - Type definition
2. `src/services/userService.ts` - Service layer
3. `src/controllers/userController.ts` - Controller
4. `src/routes/userRoutes.ts` - Routes
5. `tests/user.test.ts` - Tests

### Dependency Graph
```
types/user.ts
     │
     ├── services/userService.ts
     │        │
     │        └── controllers/userController.ts
     │                     │
     │                     └── routes/userRoutes.ts
     │
     └── tests/user.test.ts
```

### Risk Assessment
- Breaking change: [Yes/No]
- Downtime required: [Yes/No]
- Rollback plan: [Strategy]
```

## 2.2 Phase 2: Preparation

```bash
# 1. Create clean branch
git checkout -b feature/rename-user-to-customer

# 2. Verify working state
npm test
npm run build
npm run lint

# 3. Backup/stash (for safety)
git stash push -m "backup before big refactor"
```

## 2.3 Phase 3: Step-by-Step Implementation

```typescript
// STEP 1: Change Type definition
// src/types/user.ts
// ❌ Old
interface User {
  userId: string;
  name: string;
}

// ✅ New
interface User {
  customerId: string;  // userId -> customerId
  name: string;
}

// Commit: "rename: userId -> customerId in User interface"
```

```typescript
// STEP 2: Update Service
// src/services/userService.ts
export async function getUser(customerId: string) { // userId -> customerId
  return db.user.findUnique({
    where: { customerId } // userId -> customerId
  });
}

// Commit: "rename: userId -> customerId in userService"
```

```typescript
// STEP 3: Update Controller
// Commit: "rename: userId -> customerId in userController"

// STEP 4: Update Routes
// Commit: "rename: userId -> customerId in routes"

// STEP 5: Update Tests
// Commit: "rename: userId -> customerId in tests"
```

## 2.4 Phase 4: Verification

```bash
# Run all checks
npm run lint
npx tsc --noEmit
npm test
npm run build

# If all pass
git push origin feature/rename-user-to-customer
```

---

# 3. Tools and Techniques

## 3.1 IDE Refactoring (Rename Symbol)

```typescript
// VS Code / WebStorm
// F2 or Right Click -> Rename Symbol

// Automatically updates all usages
// BUT: Only TypeScript/JavaScript references
// Won't find usages inside strings!
```

## 3.2 Check with Grep

```bash
# Find all usages
grep -r "userId" --include="*.ts" --include="*.tsx" src/

# Case insensitive
grep -ri "userid" src/

# Exclude directories
grep -r "userId" --exclude-dir={node_modules,dist} .
```

## 3.3 Find and Replace (Carefully!)

```bash
# Replace with sed (USE CAREFULLY!)
# Preview first
grep -r "oldName" src/

# Then replace
find src -type f -name "*.ts" -exec sed -i 's/oldName/newName/g' {} +

# WARNING: Sed does blind replacement, false matches possible!
```

## 3.4 Auto-detection with TypeScript

```bash
# Show type errors
npx tsc --noEmit

# Watch mode
npx tsc --noEmit --watch
```

---

# 4. Context Preservation (Context Keeping)

## 4.1 Document Working State

```markdown
## Progress Tracker

### Completed Steps
- [x] Types updated
- [x] Services updated
- [ ] Controllers updated
- [ ] Routes updated
- [ ] Tests updated

### Current Step
Updating `userId` -> `customerId` in Controllers

### Pending Issues
- [ ] Legacy API backward compatibility
- [ ] Database migration might be needed

### Notes
- There are 3 places with userId in userController.ts
- One is query param, two are in body
```

## 4.2 Using Git Stash

```bash
# Save unfinished work
git stash push -m "WIP: userId rename, controllers remaining"

# List stashes
git stash list

# Apply back
git stash pop

# Apply specific stash
git stash apply stash@{0}
```

## 4.3 Branch Strategy

```bash
# Feature branch
git checkout -b refactor/rename-userid

# Intermediate commits
git commit -m "WIP: types done"
git commit -m "WIP: services done"

# Squash before merge (optional)
git rebase -i main
# Mark WIP commits as "squash"
```

---

# 5. Dangerous Situations

## 5.1 Breaking Change Detection

```typescript
// API change = Breaking change
// BEFORE: /users/:userId
// AFTER: /users/:customerId

// Solution 1: Support both old and new
router.get('/users/:userId', handleByUserId);
router.get('/users/:customerId', handleByCustomerId);

// Solution 2: Aliasing
router.get('/users/:id', (req) => {
  const id = req.params.id; // Generic name
});
```

## 5.2 Database Column Rename

```sql
-- DANGEROUS: Direct rename
ALTER TABLE users RENAME COLUMN user_id TO customer_id;
-- ❌ Breaks old code!

-- SAFE: Expand and Contract pattern
-- Step 1: Add new column
ALTER TABLE users ADD COLUMN customer_id UUID;
UPDATE users SET customer_id = user_id;

-- Step 2: Update code (support both columns)

-- Step 3: Remove old column (after code is fully migrated)
ALTER TABLE users DROP COLUMN user_id;
```

---

# 6. Rollback Strategies

## 6.1 Git Revert

```bash
# Revert specific commit
git revert <commit-hash>

# Range revert
git revert HEAD~3..HEAD

# Revert merge
git revert -m 1 <merge-commit>
```

## 6.2 Partial Rollback

```bash
# Revert only specific file
git checkout HEAD~1 -- src/services/userService.ts

# Revert to specific commit version
git checkout abc123 -- src/services/userService.ts
```

---

# 7. Checklist

### Before Starting
- [ ] Affected files listed
- [ ] Dependency order determined
- [ ] Tests passed
- [ ] Clean git state

### At Every Step
- [ ] One logical change
- [ ] Tests passed
- [ ] Type check passed
- [ ] Separate commit made

### After Completion
- [ ] All tests passed
- [ ] Build successful
- [ ] Lint clean
- [ ] Code review received
- [ ] Documentation updated

---

# 8. Don't List

❌ Do not make all changes in a single commit
❌ Do not proceed without running tests
❌ Do not skip the dependency order
❌ Do not rely solely on manual string replacement (grep + sed)
❌ Do not perform DB column rename + code change in the same deployment

---

# 9. Must Do List

✅ Document impact analysis
✅ Follow dependency order
✅ Run tests after every step
✅ Commit every atomic step
✅ Use IDE refactoring tools
✅ Check with Grep
✅ Ensure Zero TypeScript errors
✅ Have a rollback plan

---

**Last Update:** December 2025
**Version:** 2.0
