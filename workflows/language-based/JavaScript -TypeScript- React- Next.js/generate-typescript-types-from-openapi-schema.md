---
description: Auto-generate type-safe API client from OpenAPI/Swagger spec
---

1. **Get Your API Schema**:
   - Most APIs expose OpenAPI spec at `/swagger.json` or `/openapi.json`.
   - Download it or use the URL directly.

2. **Install openapi-typescript**:
   - Best tool for generating types.
   // turbo
   - Run `npm install --save-dev openapi-typescript`

3. **Generate Types**:
   - Create types from schema URL.
   // turbo
   - Run `npx openapi-typescript https://api.example.com/openapi.json -o src/types/api.ts`

4. **Use Generated Types**:
   - Import and use in your API calls.
   ```tsx
   import type { paths } from './types/api';
   
   type UserResponse = paths['/users']['get']['responses']['200']['content']['application/json'];
   
   async function getUsers(): Promise<UserResponse> {
     const res = await fetch('/api/users');
     return res.json();
   }
   ```

5. **Auto-Regenerate on Change**:
   - Add script to package.json.
   ```json
   {
     "scripts": {
       "generate:types": "openapi-typescript https://api.example.com/openapi.json -o src/types/api.ts"
     }
   }
   ```

6. **Alternative: tRPC**:
   - For Next.js apps, use tRPC for end-to-end type safety.
   // turbo
   - Run `npm install @trpc/server @trpc/client @trpc/react-query @trpc/next`

7. **Pro Tips**:
   - Run `npm run generate:types` before starting development.
   - Commit generated types to git for team consistency.
   - Use `openapi-fetch` for a fully typed fetch wrapper.