# Multi-File Sync Rule

## Activation
- **Mode:** Model Decision
- **Description:** Safe multi-file change and context preservation guide. Activate for: cross-file refactoring, rename operations, migration tasks, and coordinated changes across multiple files.

---

## Core Principles

### Atomic Changes
Each commit should contain ONE logical change:

```
CORRECT:
- Commit 1: "rename: userId -> customerId in types"
- Commit 2: "rename: userId -> customerId in services"
- Commit 3: "rename: userId -> customerId in controllers"

WRONG:
- Commit 1: "refactor everything" (all changes in one)
```

### Test-First Approach
```bash
npm test           # Before change
# ... make change ...
npm test           # After change
git commit -m "step X: description"
```

### Dependency Order
```
1. Types/Interfaces (most independent)
2. Utilities/Helpers
3. Services/Repositories
4. Controllers/Handlers
5. Routes/Entry points
6. Tests
7. Documentation
```

---

## Multi-File Change Process

### Phase 1: Analysis & Planning

```markdown
## Change Plan

### Impact Analysis
Change: [What will change]

### Affected Files
1. src/types/user.ts - Type definition
2. src/services/userService.ts - Service layer
3. src/controllers/userController.ts - Controller
4. tests/user.test.ts - Tests

### Dependency Graph
types/user.ts
     |
     +-- services/userService.ts
     |        |
     |        +-- controllers/userController.ts
     |
     +-- tests/user.test.ts

### Risk Assessment
- Breaking change: [Yes/No]
- Downtime required: [Yes/No]
- Rollback strategy: [Strategy]
```

### Phase 2: Preparation

```bash
# 1. Create clean branch
git checkout -b feature/rename-user-to-customer

# 2. Verify working state
npm test && npm run build && npm run lint

# 3. Backup (safety)
git stash push -m "backup before refactor"
```

### Phase 3: Step-by-Step Implementation

```typescript
// STEP 1: Change type definition
// src/types/user.ts
interface User {
  customerId: string;  // userId -> customerId
}
// Commit: "rename: userId -> customerId in User interface"

// STEP 2: Update service
// Commit: "rename: userId -> customerId in userService"

// STEP 3: Update controller
// STEP 4: Update routes
// STEP 5: Update tests
```

### Phase 4: Verification

```bash
npm run lint
npx tsc --noEmit
npm test
npm run build

# If all pass
git push origin feature/rename-user-to-customer
```

---

## Tools & Techniques

### IDE Refactoring
```
VS Code / WebStorm: F2 or Right-click -> Rename Symbol
- Updates all TypeScript/JavaScript references
- WARNING: Won't find string usages!
```

### Grep Verification
```bash
# Find all usages
grep -r "userId" --include="*.ts" src/

# Case insensitive
grep -ri "userid" src/

# Exclude directories
grep -r "userId" --exclude-dir={node_modules,dist} .
```

### TypeScript Error Detection
```bash
npx tsc --noEmit
npx tsc --noEmit --watch
```

---

## Context Preservation

### Progress Tracker
```markdown
## Progress

### Completed Steps
- [x] Types updated
- [x] Services updated
- [ ] Controllers updated
- [ ] Tests updated

### Current Step
Controllers: userId -> customerId

### Pending Issues
- [ ] Legacy API backward compatibility
```

### Git Stash
```bash
# Save work in progress
git stash push -m "WIP: userId rename, controllers left"

# List stashes
git stash list

# Restore
git stash pop
```

---

## Dangerous Situations

### Breaking Changes
```typescript
// API change = Breaking change
// BEFORE: /users/:userId
// AFTER: /users/:customerId

// Solution: Support both
router.get('/users/:userId', handleByUserId);
router.get('/users/:customerId', handleByCustomerId);
```

### Database Column Rename
```sql
-- DANGEROUS: Direct rename
ALTER TABLE users RENAME COLUMN user_id TO customer_id;
-- Old code breaks!

-- SAFE: Expand and Contract
-- Step 1: Add new column
ALTER TABLE users ADD COLUMN customer_id UUID;
UPDATE users SET customer_id = user_id;

-- Step 2: Update code (support both)
-- Step 3: Remove old column (after code migration)
ALTER TABLE users DROP COLUMN user_id;
```

---

## Rollback Strategies

```bash
# Revert specific commit
git revert <commit-hash>

# Revert range
git revert HEAD~3..HEAD

# Partial rollback (specific file)
git checkout HEAD~1 -- src/services/userService.ts
```

---

## Checklist

### Before Starting
- [ ] Affected files listed
- [ ] Dependency order determined
- [ ] Tests passing
- [ ] Clean git state

### Each Step
- [ ] Single logical change
- [ ] Tests pass
- [ ] Type check passes
- [ ] Separate commit made

### After Completion
- [ ] All tests pass
- [ ] Build successful
- [ ] Lint clean
- [ ] Code review obtained
- [ ] Documentation updated

---

## Don't List

- All changes in single commit
- Continue without testing
- Skip dependency order
- Blind string replace (grep + sed)
- Database rename + code change in same deployment

---

## Must Do List

- Perform and document impact analysis
- Follow dependency order
- Test after each step
- Separate commit per step
- Use IDE refactoring tools
- Verify with grep
- TypeScript errors must be zero
- Have rollback plan

---

**Version:** 2.0 (Antigravity Rule)
