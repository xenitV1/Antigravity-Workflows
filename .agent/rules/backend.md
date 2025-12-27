# Backend Development Rule

## Activation
- **Mode:** Glob
- **Glob Pattern:** `*.ts, *.js, src/**, api/**, server/**`
- **Description:** Backend development guide for Node.js, TypeScript, API design, database integration, and security. Auto-activates for server-side code files.

---

## Tech Stack (2025)

| Area | Technologies |
|------|--------------|
| Runtime | Node.js 20+ (LTS) |
| Language | TypeScript (Strict Mode) |
| Framework | NestJS, Fastify, Express, Hono.js |
| API | REST, GraphQL, tRPC |
| Database | PostgreSQL, MongoDB, Redis |
| ORM | Prisma, Drizzle, TypeORM |
| Auth | JWT, OAuth 2.0, Passport |

---

## Core Principles

### TypeScript Strict Mode (MANDATORY)
```json
{
  "strict": true,
  "noImplicitAny": true,
  "strictNullChecks": true
}
```

### `any` is FORBIDDEN
```typescript
// ❌ WRONG
function process(data: any) { ... }

// ✅ CORRECT
interface DataPayload { value: string; }
function process(data: DataPayload): string { ... }
```

---

## Project Structure

```
src/
├── modules/
│   └── users/
│       ├── users.controller.ts
│       ├── users.service.ts
│       ├── users.repository.ts
│       ├── users.dto.ts
│       └── users.entity.ts
├── common/
│   ├── decorators/
│   ├── guards/
│   ├── interceptors/
│   └── filters/
├── config/
└── main.ts
```

---

## API Design Rules

### REST Conventions
| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | /users | List all |
| GET | /users/:id | Get one |
| POST | /users | Create |
| PATCH | /users/:id | Update |
| DELETE | /users/:id | Delete |

### Response Format
```typescript
interface ApiResponse<T> {
  success: boolean;
  data?: T;
  error?: { code: string; message: string; };
  meta?: { page: number; total: number; };
}
```

---

## Input Validation (Zod)

```typescript
import { z } from 'zod';

const createUserSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
  name: z.string().min(2).max(50),
});

// Validate
const result = createUserSchema.safeParse(input);
if (!result.success) {
  throw new ValidationError(result.error);
}
```

---

## Security Checklist

- [ ] Environment variables validated
- [ ] Rate limiting configured
- [ ] Helmet.js for security headers
- [ ] CORS properly configured
- [ ] SQL injection prevented (parameterized queries)
- [ ] XSS prevention in place
- [ ] JWT with proper expiration
- [ ] Password hashing (bcrypt/argon2)

---

## Database Patterns

### Repository Pattern
```typescript
class UserRepository {
  async findById(id: string): Promise<User | null> {
    return this.prisma.user.findUnique({ where: { id } });
  }

  async create(data: CreateUserDto): Promise<User> {
    return this.prisma.user.create({ data });
  }
}
```

### Transaction Handling
```typescript
await prisma.$transaction(async (tx) => {
  await tx.user.update({ ... });
  await tx.account.create({ ... });
});
```

---

## Error Handling

```typescript
class AppError extends Error {
  constructor(
    public statusCode: number,
    public code: string,
    message: string
  ) {
    super(message);
  }
}

// Global error handler
app.use((err, req, res, next) => {
  const status = err.statusCode || 500;
  res.status(status).json({
    success: false,
    error: { code: err.code, message: err.message }
  });
});
```

---

## Checklist

- [ ] TypeScript strict mode enabled
- [ ] No `any` types used
- [ ] Input validation with Zod
- [ ] Proper error handling
- [ ] Security headers configured
- [ ] Rate limiting in place
- [ ] API follows REST conventions
- [ ] Tests written

---

**Version:** 2.0 (Antigravity Rule)
