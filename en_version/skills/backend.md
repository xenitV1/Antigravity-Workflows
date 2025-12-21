---
name: backend
description: Backend development guide. 2025 best practices for Node.js, TypeScript, API design, database integration, and security.
metadata:
  skillport:
    category: development
    tags:
      - nodejs
      - typescript
      - api
      - database
      - security
---

# Backend Development Skill

> Guide for developing modern, secure, and scalable backends with Node.js and TypeScript.
> Compliant with 2025 best practices and industry standards.

---

## 🎯 Scope

| Area | Technologies |
|------|--------------|
| Runtime | Node.js 20+ (LTS) |
| Language | TypeScript (Strict Mode) |
| Framework | NestJS, Fastify, Express |
| API | REST, GraphQL, tRPC |
| Database | PostgreSQL, MongoDB, Redis |
| ORM | Prisma, Drizzle, TypeORM |
| Auth | JWT, OAuth 2.0, Passport |
| Test | Jest, Vitest, Supertest |

---

## 📏 Core Principles

### 1. TypeScript Strict Mode (Mandatory)

```json
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

### 2. `any` Type is Forbidden

```typescript
// ❌ INCORRECT
function processData(data: any) {
  return data.value;
}

// ✅ CORRECT
interface DataPayload {
  value: string;
  metadata?: Record<string, unknown>;
}

function processData(data: DataPayload): string {
  return data.value;
}

// Use unknown for unknown data
function parseInput(input: unknown): DataPayload {
  if (isDataPayload(input)) {
    return input;
  }
  throw new Error('Invalid input format');
}
```

### 3. Use ES Modules (ESM)

```typescript
// ✅ Modern ESM syntax
import { Router } from 'express';
import type { Request, Response } from 'express';

export const userRouter = Router();

// package.json
{
  "type": "module"
}
```

---

## 🏗️ Project Structure

### Feature-First Structure (Recommended)

```
src/
├── modules/
│   ├── auth/
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   ├── auth.repository.ts
│   │   ├── auth.dto.ts
│   │   ├── auth.types.ts
│   │   └── __tests__/
│   │       └── auth.service.test.ts
│   ├── users/
│   │   ├── users.controller.ts
│   │   ├── users.service.ts
│   │   └── ...
│   └── products/
├── shared/
│   ├── middleware/
│   ├── guards/
│   ├── interceptors/
│   ├── filters/
│   └── utils/
├── infrastructure/
│   ├── database/
│   ├── cache/
│   ├── queue/
│   └── logger/
├── config/
│   ├── app.config.ts
│   ├── database.config.ts
│   └── env.validation.ts
└── main.ts
```

---

## 🔧 API Design Rules

### RESTful Endpoint Conventions

```typescript
// Resource naming (plural, lowercase, kebab-case)
GET    /api/v1/users           // List
GET    /api/v1/users/:id       // Get one
POST   /api/v1/users           // Create
PATCH  /api/v1/users/:id       // Partial update
PUT    /api/v1/users/:id       // Full replace
DELETE /api/v1/users/:id       // Delete

// Nested resources
GET    /api/v1/users/:userId/orders
POST   /api/v1/users/:userId/orders

// Query parameters
GET    /api/v1/users?page=1&limit=10&sort=createdAt:desc&filter[status]=active
```

### Response Format Standard

```typescript
// Successful response
interface SuccessResponse<T> {
  success: true;
  data: T;
  meta?: {
    page?: number;
    limit?: number;
    total?: number;
    totalPages?: number;
  };
}

// Error response
interface ErrorResponse {
  success: false;
  error: {
    code: string;
    message: string;
    details?: Record<string, unknown>;
    stack?: string; // Only development
  };
}

// Example implementation
function createSuccessResponse<T>(data: T, meta?: object): SuccessResponse<T> {
  return { success: true, data, meta };
}

function createErrorResponse(code: string, message: string): ErrorResponse {
  return { 
    success: false, 
    error: { code, message } 
  };
}
```

### HTTP Status Codes

| Code | Usage |
|-----|----------|
| 200 | Successful GET, PATCH, PUT |
| 201 | Successful POST (Created) |
| 204 | Successful DELETE (No Content) |
| 400 | Validation error |
| 401 | Authentication required |
| 403 | Forbidden (No permissions) |
| 404 | Resource not found |
| 409 | Conflict (duplicate etc.) |
| 422 | Unprocessable Entity |
| 429 | Rate limit exceeded |
| 500 | Server error |

---

## ✅ Input Validation (Zod)

```typescript
import { z } from 'zod';

// Schema definition
const CreateUserSchema = z.object({
  email: z.string().email('Enter a valid email'),
  password: z.string()
    .min(8, 'Password must be at least 8 characters')
    .regex(/[A-Z]/, 'At least 1 uppercase letter')
    .regex(/[0-9]/, 'At least 1 digit'),
  name: z.string().min(2).max(100),
  age: z.number().int().min(13).max(120).optional(),
});

type CreateUserDto = z.infer<typeof CreateUserSchema>;

// Use as middleware
function validateBody<T>(schema: z.ZodSchema<T>) {
  return (req: Request, res: Response, next: NextFunction) => {
    const result = schema.safeParse(req.body);
    if (!result.success) {
      return res.status(400).json(
        createErrorResponse('VALIDATION_ERROR', result.error.message)
      );
    }
    req.body = result.data;
    next();
  };
}

// Use in route
router.post('/users', validateBody(CreateUserSchema), createUser);
```

---

## 🔒 Security Best Practices

### 1. Environment Variables

```typescript
// env.validation.ts
import { z } from 'zod';

const envSchema = z.object({
  NODE_ENV: z.enum(['development', 'production', 'test']),
  PORT: z.string().transform(Number),
  DATABASE_URL: z.string().url(),
  JWT_SECRET: z.string().min(32),
  JWT_EXPIRES_IN: z.string().default('7d'),
});

export const env = envSchema.parse(process.env);

// ❌ NEVER do this
const secret = "hardcoded-secret-key";

// ✅ Always get from env
const secret = env.JWT_SECRET;
```

### 2. Security Headers (Helmet)

```typescript
import helmet from 'helmet';
import rateLimit from 'express-rate-limit';
import cors from 'cors';

app.use(helmet());
app.use(helmet.contentSecurityPolicy({
  directives: {
    defaultSrc: ["'self'"],
    scriptSrc: ["'self'"],
  }
}));

// CORS configuration
app.use(cors({
  origin: env.ALLOWED_ORIGINS.split(','),
  credentials: true,
}));

// Rate limiting
app.use(rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // 100 requests per IP
  message: { error: 'Too many requests' }
}));
```

### 3. SQL Injection Prevention

```typescript
// ❌ NEVER use variables in raw query
const query = `SELECT * FROM users WHERE id = ${userId}`;

// ✅ Use parametrized query
const user = await prisma.user.findUnique({
  where: { id: userId }
});

// Or if raw query is necessary
const users = await prisma.$queryRaw`
  SELECT * FROM users WHERE id = ${userId}
`;
```

---

## 🗄️ Database Patterns

### Repository Pattern

```typescript
// users.repository.ts
interface IUserRepository {
  findById(id: string): Promise<User | null>;
  findByEmail(email: string): Promise<User | null>;
  create(data: CreateUserDto): Promise<User>;
  update(id: string, data: UpdateUserDto): Promise<User>;
  delete(id: string): Promise<void>;
}

class UserRepository implements IUserRepository {
  constructor(private prisma: PrismaClient) {}

  async findById(id: string): Promise<User | null> {
    return this.prisma.user.findUnique({ where: { id } });
  }

  async findByEmail(email: string): Promise<User | null> {
    return this.prisma.user.findUnique({ where: { email } });
  }

  async create(data: CreateUserDto): Promise<User> {
    return this.prisma.user.create({ data });
  }
}
```

---

## ⚡ Performance Optimization

### 1. Async/Await Best Practices

```typescript
// ✅ Parallel (fast)
const [user, orders, payments] = await Promise.all([
  getUser(id),
  getOrders(id),
  getPayments(id),
]);
```

### 2. Caching (Redis)

```typescript
async function getCachedUser(id: string): Promise<User | null> {
  const cacheKey = `user:${id}`;
  
  // Read from cache
  const cached = await redis.get(cacheKey);
  if (cached) {
    return JSON.parse(cached);
  }
  
  // Fetch from DB and cache
  const user = await userRepository.findById(id);
  if (user) {
    await redis.set(cacheKey, JSON.stringify(user), 'EX', 3600); // 1 hour
  }
  
  return user;
}
```

---

## 📝 Error Handling

```typescript
// Global error handler
function errorHandler(err: Error, req: Request, res: Response, next: NextFunction) {
  console.error(err);
  
  if (err instanceof AppError) {
    return res.status(err.statusCode).json(
      createErrorResponse(err.code, err.message)
    );
  }
  
  // Unknown error
  return res.status(500).json(
    createErrorResponse('INTERNAL_ERROR', 'Something went wrong')
  );
}

app.use(errorHandler);
```

---

## ✅ Checklist

In every backend development:

- [ ] TypeScript strict mode active
- [ ] `any` type not used
- [ ] All inputs validated (Zod)
- [ ] Environment variables read from env
- [ ] SQL injection protection present
- [ ] Authentication/Authorization implemented
- [ ] Rate limiting active
- [ ] CORS configured correctly
- [ ] Error handling centralized
- [ ] Logging implemented
- [ ] Unit tests written

---

## 🔴 Don't List

❌ Do not use `any` type
❌ Do not write hardcoded secrets/passwords
❌ Do not concatenate variables in raw SQL
❌ Do not perform file/network operations with sync functions
❌ Do not leave console.log in production
❌ Do not show error stack to the user
❌ Do not skip input validation
❌ Do not make N+1 queries

---

## ✅ Must Do List

✅ Input validation for every endpoint
✅ Try-catch in all async operations
✅ Proper HTTP status codes
✅ Response format standardization
✅ Environment-based configuration
✅ Security headers (Helmet)
✅ Rate limiting
✅ Request logging
✅ Database transactions where needed
✅ Cache strategy

---

**Last Update:** December 2025
**Version:** 1.0
