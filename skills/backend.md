---
name: backend
description: Backend geliştirme rehberi. Node.js, TypeScript, API tasarımı, veritabanı entegrasyonu ve güvenlik için 2025 best practices.
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

> Node.js ve TypeScript ile modern, güvenli ve ölçeklenebilir backend geliştirme rehberi.
> 2025 best practices ve endüstri standartlarına uygun.

---

# 📋 İçindekiler

1. [Kapsam](#1-kapsam)
2. [Temel Prensipler](#2-temel-prensipler)
3. [Proje Yapısı](#3-proje-yapısı)
4. [API Tasarım Kuralları](#4-api-tasarım-kuralları)
5. [Input Validation (Zod)](#5-input-validation-zod)
6. [Güvenlik Best Practices](#6-güvenlik-best-practices)
7. [Veritabanı Patterns](#7-veritabanı-patterns)
8. [Performance Optimization](#8-performance-optimization)
9. [Error Handling](#9-error-handling)
10. [Kontrol Listesi](#10-kontrol-listesi)
11. [Yapma Listesi](#11-yapma-listesi)
12. [Mutlaka Yap Listesi](#12-mutlaka-yap-listesi)

---

# 1. Kapsam

| Alan | Teknolojiler |
|------|--------------|
| Runtime | Node.js 20+ (LTS) |
| Dil | TypeScript (Strict Mode) |
| Framework | NestJS, Fastify, Express |
| API | REST, GraphQL, tRPC |
| Veritabanı | PostgreSQL, MongoDB, Redis |
| ORM | Prisma, Drizzle, TypeORM |
| Auth | JWT, OAuth 2.0, Passport |
| Test | Jest, Vitest, Supertest |

---

# 2. Temel Prensipler

## 2.1 TypeScript Strict Mode (Zorunlu)

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

## 2.2 `any` Tipi Yasak

```typescript
// ❌ YANLIŞ
function processData(data: any) {
  return data.value;
}

// ✅ DOĞRU
interface DataPayload {
  value: string;
  metadata?: Record<string, unknown>;
}

function processData(data: DataPayload): string {
  return data.value;
}

// Bilinmeyen veri için unknown kullan
function parseInput(input: unknown): DataPayload {
  if (isDataPayload(input)) {
    return input;
  }
  throw new Error('Invalid input format');
}
```

## 2.3 ES Modules (ESM) Kullan

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

# 3. Proje Yapısı

## 3.1 Feature-First Structure (Önerilen)

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

# 4. API Tasarım Kuralları

## 4.1 RESTful Endpoint Conventions

```typescript
// Resource naming (çoğul, küçük harf, kebab-case)
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

## 4.2 Response Format Standardı

```typescript
// Başarılı response
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

// Hata response
interface ErrorResponse {
  success: false;
  error: {
    code: string;
    message: string;
    details?: Record<string, unknown>;
    stack?: string; // Sadece development
  };
}

// Örnek implementasyon
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

## 4.3 HTTP Status Codes

| Kod | Kullanım |
|-----|----------|
| 200 | Başarılı GET, PATCH, PUT |
| 201 | Başarılı POST (Created) |
| 204 | Başarılı DELETE (No Content) |
| 400 | Validation hatası |
| 401 | Authentication gerekli |
| 403 | Yetki yok (Forbidden) |
| 404 | Resource bulunamadı |
| 409 | Conflict (duplicate vb.) |
| 422 | Unprocessable Entity |
| 429 | Rate limit aşıldı |
| 500 | Server hatası |

---

# 5. Input Validation (Zod)

```typescript
import { z } from 'zod';

// Schema tanımı
const CreateUserSchema = z.object({
  email: z.string().email('Geçerli email giriniz'),
  password: z.string()
    .min(8, 'Şifre en az 8 karakter olmalı')
    .regex(/[A-Z]/, 'En az 1 büyük harf')
    .regex(/[0-9]/, 'En az 1 rakam'),
  name: z.string().min(2).max(100),
  age: z.number().int().min(13).max(120).optional(),
});

type CreateUserDto = z.infer<typeof CreateUserSchema>;

// Middleware olarak kullanım
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

// Route'da kullanım
router.post('/users', validateBody(CreateUserSchema), createUser);
```

---

# 6. Güvenlik Best Practices

## 6.1 Environment Variables

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

// ❌ ASLA yapma
const secret = "hardcoded-secret-key";

// ✅ Her zaman env'den al
const secret = env.JWT_SECRET;
```

## 6.2 Security Headers (Helmet)

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
  windowMs: 15 * 60 * 1000, // 15 dakika
  max: 100, // IP başına 100 istek
  message: { error: 'Too many requests' }
}));
```

## 6.3 SQL Injection Prevention

```typescript
// ❌ ASLA raw query'de değişken kullanma
const query = `SELECT * FROM users WHERE id = ${userId}`;

// ✅ Parametrized query kullan
const user = await prisma.user.findUnique({
  where: { id: userId }
});

// Veya raw query gerekiyorsa
const users = await prisma.$queryRaw`
  SELECT * FROM users WHERE id = ${userId}
`;
```

## 6.4 Authentication & Authorization

```typescript
// JWT middleware
import jwt from 'jsonwebtoken';

interface JwtPayload {
  userId: string;
  email: string;
  role: 'user' | 'admin';
}

function authMiddleware(req: Request, res: Response, next: NextFunction) {
  const token = req.headers.authorization?.replace('Bearer ', '');
  
  if (!token) {
    return res.status(401).json(createErrorResponse('UNAUTHORIZED', 'Token required'));
  }
  
  try {
    const decoded = jwt.verify(token, env.JWT_SECRET) as JwtPayload;
    req.user = decoded;
    next();
  } catch {
    return res.status(401).json(createErrorResponse('INVALID_TOKEN', 'Invalid token'));
  }
}

// Role-based access
function requireRole(...roles: string[]) {
  return (req: Request, res: Response, next: NextFunction) => {
    if (!roles.includes(req.user.role)) {
      return res.status(403).json(createErrorResponse('FORBIDDEN', 'Access denied'));
    }
    next();
  };
}

// Kullanım
router.delete('/users/:id', authMiddleware, requireRole('admin'), deleteUser);
```

---

# 7. Veritabanı Patterns

## 7.1 Repository Pattern

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
  
  // ... diğer metodlar
}
```

## 7.2 Transaction Handling

```typescript
async function transferMoney(fromId: string, toId: string, amount: number) {
  return prisma.$transaction(async (tx) => {
    const from = await tx.account.update({
      where: { id: fromId },
      data: { balance: { decrement: amount } },
    });
    
    if (from.balance < 0) {
      throw new Error('Insufficient funds');
    }
    
    await tx.account.update({
      where: { id: toId },
      data: { balance: { increment: amount } },
    });
    
    return { success: true };
  });
}
```

---

# 8. Performance Optimization

## 8.1 Async/Await Best Practices

```typescript
// ❌ Sequential (yavaş)
const user = await getUser(id);
const orders = await getOrders(id);
const payments = await getPayments(id);

// ✅ Parallel (hızlı)
const [user, orders, payments] = await Promise.all([
  getUser(id),
  getOrders(id),
  getPayments(id),
]);

// Promise.allSettled (hata toleranslı)
const results = await Promise.allSettled([
  fetchData1(),
  fetchData2(),
  fetchData3(),
]);
```

## 8.2 Caching (Redis)

```typescript
import Redis from 'ioredis';

const redis = new Redis(env.REDIS_URL);

async function getCachedUser(id: string): Promise<User | null> {
  const cacheKey = `user:${id}`;
  
  // Cache'den oku
  const cached = await redis.get(cacheKey);
  if (cached) {
    return JSON.parse(cached);
  }
  
  // DB'den çek ve cache'le
  const user = await userRepository.findById(id);
  if (user) {
    await redis.set(cacheKey, JSON.stringify(user), 'EX', 3600); // 1 saat
  }
  
  return user;
}

// Cache invalidation
async function updateUser(id: string, data: UpdateUserDto) {
  const user = await userRepository.update(id, data);
  await redis.del(`user:${id}`);
  return user;
}
```

## 8.3 Database Query Optimization

```typescript
// ❌ N+1 problem
const users = await prisma.user.findMany();
for (const user of users) {
  const posts = await prisma.post.findMany({ where: { authorId: user.id } });
}

// ✅ Include ile tek sorgu
const users = await prisma.user.findMany({
  include: { posts: true },
});

// ✅ Select ile sadece gerekli alanlar
const users = await prisma.user.findMany({
  select: {
    id: true,
    name: true,
    email: true,
    _count: { select: { posts: true } },
  },
});
```

---

# 9. Error Handling

```typescript
// Custom error classes
class AppError extends Error {
  constructor(
    public statusCode: number,
    public code: string,
    message: string,
  ) {
    super(message);
    this.name = 'AppError';
  }
}

class NotFoundError extends AppError {
  constructor(resource: string) {
    super(404, 'NOT_FOUND', `${resource} not found`);
  }
}

class ValidationError extends AppError {
  constructor(message: string) {
    super(400, 'VALIDATION_ERROR', message);
  }
}

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

# 10. Kontrol Listesi

Her backend geliştirmede:

- [ ] TypeScript strict mode aktif
- [ ] `any` tipi kullanılmadı
- [ ] Tüm inputlar validate edildi (Zod)
- [ ] Environment variables env'den okunuyor
- [ ] SQL injection koruması var
- [ ] Authentication/Authorization implement edildi
- [ ] Rate limiting aktif
- [ ] CORS doğru yapılandırıldı
- [ ] Error handling merkezi
- [ ] Logging implement edildi
- [ ] Unit testler yazıldı

---

# 11. Yapma Listesi

❌ `any` tipi kullanma
❌ Hardcoded secret/password yazma
❌ Raw SQL'de değişken birleştirme
❌ Sync fonksiyonlarla dosya/network işlemi
❌ Console.log production'da bırakma
❌ Error stack'i kullanıcıya gösterme
❌ Input validation'ı atlama
❌ N+1 query yapma

---

# 12. Mutlaka Yap Listesi

✅ Her endpoint için input validation
✅ Tüm async işlemlerde try-catch
✅ Proper HTTP status codes
✅ Response format standardizasyonu
✅ Environment-based configuration
✅ Security headers (Helmet)
✅ Rate limiting
✅ Request logging
✅ Database transactions where needed
✅ Cache stratejisi

---

**Son Güncelleme:** Aralık 2025
**Versiyon:** 2.0
