---
description: useEffect kaynaklı sonsuz döngüleri ve gereksiz render sorunlarını analiz edip çözer.
---

Act as a Senior React Debugging Expert.
1. **Analyze:** Look at the selected React component, specifically focusing on `useEffect`, `useLayoutEffect`, and state updates.
2. **Diagnose:** Identify patterns causing infinite re-renders:
   - Updating a state inside `useEffect` that is also in the dependency array.
   - Missing dependency array (causing run on every render).
   - Object/Array references creating unstable dependencies (Reference Equality).
3. **Fix:** Rewrite the `useEffect` logic. Use `useCallback` or `useMemo` to stabilize references if needed.
4. **Explain:** Explain strictly *why* the loop happened in Turkish.