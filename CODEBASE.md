# CODEBASE.md

> **Auto-generated project context file.** Refreshed on every session start.
>
> **Purpose:** Provides Claude AI with project structure, OS info, and coding standards automatically.

---

# 📁 Project Context

**Project:** `Antigravity-Workflows`
**Framework:** `Unknown`
**Type:** `Unknown`
**Path:** `c:\Users\Mehmet\Desktop\Antigravity-Workflows`
**Detected:** 2025-12-31 17:05:23

---

## 🖥️ Operating System

| Property | Value |
|----------|-------|
| **OS** | Windows |
| **Shell** | PowerShell / CMD |

---

## ⚡ Terminal Commands (Current OS)

#### 🪟 Windows Terminal Commands

##### PowerShell
```powershell
ls                    # List files
cd <path>             # Change directory
pwd                   # Current directory
mkdir <dir>            # Create directory
rm <file>             # Remove file
rm -r <dir>           # Remove directory
cat <file>            # View file
echo $env:PATH        # Show environment variables
```

##### Common Tasks
- **File Explorer**: `start .`
- **Open with default app**: `start <file>`
- **Process manager**: `taskmgr` or `Get-Process`
- **Network info**: `ipconfig` or `Get-NetIPAddress`
- **System info**: `systeminfo`

##### Package Managers
```powershell
winget install <app>     # Install application
winget search <app>      # Search for application
winget upgrade <app>     # Upgrade application
winget list              # List installed apps
```

---


## 🎯 Project Environment

| Property | Value |
|----------|-------|
| **Project Type** | Unknown |
| **Framework** | Unknown |
| **Platform** | Unknown |

---

## 📋 Quick Project Commands



---

## 📂 Project Structure

```
CODEBASE.md
CORE.md
GEMINI.md
LICENSE
README.md
skills/
  architecture.md
  backend.md
  debugging.md
  dependency-management.md
  design-system.md
  documentation.md
  geo-analytics.md
  geo-content.md
  geo-fundamentals.md
  geo-technical.md
  mobile.md
  multi-file-sync.md
  optimization.md
  production-deployment.md
  refactoring.md
  seo-analytics.md
  seo-content.md
  seo-fundamentals.md
  seo-local.md
  seo-offpage.md
  seo-technical.md
  testing.md
  ultrathink.md
```


# Clean Code - Pragmatic AI Coding Standards

> **CRITICAL SKILL** - This skill overrides all verbose tendencies. When writing code, be **concise, direct, and solution-focused**.

---

## Golden Rules

### 1. No Verbose Explanations
**WRONG:**
```javascript
// Check if user is authenticated before allowing access to protected route
// This is a security measure to prevent unauthorized access
if (user.isAuthenticated) {
  // User is authenticated, grant access
  return renderProtectedPage();
} else {
  // User is not authenticated, redirect to login
  return redirect('/login');
}
```

**RIGHT:**
```javascript
if (!user.isAuthenticated) return redirect('/login');
return renderProtectedPage();
```

### 2. No Self-Explanatory Comments
Code should be self-documenting. If you need a comment, rename the variable.

**WRONG:**
```javascript
// Get all users from database
const users = db.get('users');

// Filter out inactive users
const active = users.filter(u => u.active);
```

**RIGHT:**
```javascript
const activeUsers = db.get('users').filter(u => u.active);
```

### 3. Direct Solutions Only
**WRONG:**
```javascript
// First, let's create a helper function to handle the case where
// we need to check if a value exists in the array...
function hasValue(arr, val) {
  return arr.includes(val);
}

// Now we can use it
if (hasValue(users, id)) {
  // ...
}
```

**RIGHT:**
```javascript
if (users.includes(id)) { /* ... */ }
```

---

## When to Write Code

### Write Code When:
1. **User asks for a feature** → Write the feature, not a planning document
2. **User reports a bug** → Fix it, don't explain the debugging process
3. **User asks "how does X work"** → Brief explanation, then move on

### Don't Write Code When:
1. User only asks "what do you think?"
2. User is exploring ideas (use brainstorming mode)
3. No clear requirement exists (ask, don't assume)

---

## Anti-Patterns to Avoid

| Anti-Pattern | Example | Fix |
|--------------|---------|-----|
| **Over-commenting** | Comment every line | Delete obvious comments |
| **Over-abstracting** | Helper for one-line operation | Inline the code |
| **Over-engineering** | Factory for 2 objects | Direct instantiation |
| **Defensive coding** | Check for impossible null | Remove dead code |
| **Tutorial-style** | "First we import..." | Just write the code |
| **Yoda conditions** | `if (null === x)` | `if (x === null)` |
| **Early returns** | Deep nesting | Guard clauses |

---

## Code Style Guidelines

### JavaScript/TypeScript
```typescript
// Prefer concise patterns
const result = data?.map(x => x.value).filter(Boolean) ?? [];

// Guard clauses
if (!user) return unauthorized();

// Direct returns
return isValid ? success() : error();

// No unnecessary intermediates
return items.filter(x => x.active).map(x => x.id);
```

### Python
```python
# Concise, pythonic
active_users = [u for u in users if u.is_active]

# Guard clauses
if not request.user.is_authenticated:
    return HttpResponseForbidden()

# Direct returns
return JsonResponse({"data": result})
```

### React/Next.js
```tsx
// Direct, no prop drilling abstractions
export default function UserProfile({ user }: { user: User }) {
  if (!user) return <LoginPrompt />;
  return <ProfileData user={user} />;
}

// No separate container components
// No unnecessary HOCs
// Use hooks directly
```

---

## What NOT to Do

### Never Add These Comments:
- ❌ "This function returns..."
- ❌ "We need to import..."
- ❌ "Now let's create..."
- ❌ "This is a React component..."
- ❌ "Here we are handling..."
- ❌ "Note that..."
- ❌ "TODO: add error handling" (add it or don't mention it)

### Never Add These Files:
- ❌ `utils.ts` with one function
- ❌ `constants.ts` with 3 values
- ❌ `types.ts` for one interface
- ❌ Separate `container/` and `components/` without reason

---

## Practical Examples

### Example 1: API Handler
**Verbose (BAD):**
```typescript
// Import the express framework for handling HTTP requests
import express from 'express';

// Create a new router instance
const router = express.Router();

/**
 * GET /api/users
 * Returns a list of all users in the database
 */
router.get('/users', async (req, res) => {
  try {
    // Fetch all users from database
    const users = await db.users.findMany();

    // Return the users as JSON
    res.json({ users });
  } catch (error) {
    // If there's an error, log it and return 500
    console.error(error);
    res.status(500).json({ error: 'Server error' });
  }
});
```

**Concise (GOOD):**
```typescript
import express from 'express';

const router = express.Router();

router.get('/users', async (req, res) => {
  const users = await db.users.findMany();
  res.json({ users });
});
```

### Example 2: React Component
**Verbose (BAD):**
```tsx
// This is a functional component that displays a user card
// It takes a user object as a prop and renders the user's information
interface UserCardProps {
  user: User;
}

export const UserCard: React.FC<UserCardProps> = ({ user }) => {
  // If there's no user, show a loading state
  if (!user) {
    return <div>Loading...</div>;
  }

  // Render the user card with name and email
  return (
    <div className="user-card">
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
};
```

**Concise (GOOD):**
```tsx
export function UserCard({ user }: { user: User }) {
  if (!user) return <div>Loading...</div>;

  return (
    <div className="user-card">
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
}
```

---

## Quick Checklist Before Writing

Ask yourself:
1. **Is this code necessary?** → If no, don't write it
2. **Can this be simpler?** → Simplify it
3. **Am I explaining obvious things?** → Delete the explanation
4. **Is there a shorter way?** → Use it
5. **Am I creating files for no reason?** → Put code inline

---

## Response Format

When asked to write code, respond like this:

```
[Direct code block]

[Brief explanation if needed, max 2 sentences]
```

**NOT like this:**
```
[Step-by-step tutorial]
[Multiple code blocks with explanations]
[File-by-file breakdown]
```

---

## Summary

| Do | Don't |
|----|-------|
| Write code directly | Write tutorials |
| Use concise syntax | Use verbose patterns |
| Let code self-document | Add obvious comments |
| Fix bugs immediately | Explain the fix first |
| Return early | Deep nesting |
| Inline small things | Create unnecessary files |
| Use language idioms | Force patterns |

---

**Remember: The user wants working code, not a programming lesson.**

---

*This file is auto-generated by Maestro session hooks. Do not edit manually.*
