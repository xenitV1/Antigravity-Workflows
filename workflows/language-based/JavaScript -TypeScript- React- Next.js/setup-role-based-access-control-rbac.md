---
description: Role-based permissions
---

1. **Define Roles**:
   ```prisma
   enum Role {
     USER
     ADMIN
     MODERATOR
   }
   ```

2. **Protect Routes**:
   ```ts
   if (session?.user?.role !== 'ADMIN') {
     return Response.json({ error: 'Forbidden' }, { status: 403 });
   }
   ```

3. **Conditional UI**:
   ```tsx
   {isAdmin && <AdminPanel />}
   ```

4. **Pro Tips**:
   - Use enums for type safety.
   - Cache permissions.