---
description: Interactively check and update outdated packages
---

1. **Check for Updates**:
   - Use `npm-check-updates` to see what's new.
   // turbo
   - Run `npx npm-check-updates`

2. **Review Changes**:
   - ⚠️ **WARNING**: Always review major version changes before updating!
   - Check changelogs for breaking changes.
   - Look for major version bumps (e.g., 1.x.x → 2.x.x).

3. **Update package.json**:
   - Update versions in your package file.
   // turbo
   - Run `npx npm-check-updates -u`

4. **Install New Versions**:
   - Install the updated packages.
   // turbo
   - Run `npm install`

5. **Test Thoroughly**:
   - Run your tests immediately after updating.
   // turbo
   - Run `npm test`

6. **Pro Tips**:
   - Use `-i` for interactive mode to selectively update: `npx ncu -i`.
   - Update only minor/patch versions: `npx ncu -u --target minor`.
   - Check for peer dependency conflicts with `npm ls`.