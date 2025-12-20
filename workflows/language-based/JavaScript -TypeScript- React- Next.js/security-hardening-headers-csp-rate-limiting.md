---
description: Essential security headers, CSP, and rate limiting
---

1. **Security Headers (`next.config.js`)**:
   - Add these headers to prevent common attacks.
   ```js
   module.exports = {
     async headers() {
       return [
         {
           source: '/:path*',
           headers: [
             { key: 'X-DNS-Prefetch-Control', value: 'on' },
             { key: 'Strict-Transport-Security', value: 'max-age=63072000; includeSubDomains; preload' },
             { key: 'X-Content-Type-Options', value: 'nosniff' },
             { key: 'X-Frame-Options', value: 'SAMEORIGIN' },
             { key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' }
           ]
         }
       ]
     }
   }
   ```

2. **Content Security Policy (CSP)**:
   - Create `src/middleware.ts`.
   ```ts
   import { NextResponse } from 'next/server';
   import type { NextRequest } from 'next/server';
   
   export function middleware(request: NextRequest) {
     const nonce = Buffer.from(crypto.randomUUID()).toString('base64');
     const cspHeader = `
       default-src 'self';
       script-src 'self' 'nonce-${nonce}' 'strict-dynamic';
       style-src 'self' 'nonce-${nonce}';
       img-src 'self' blob: data:;
       font-src 'self';
       object-src 'none';
       base-uri 'self';
       form-action 'self';
       frame-ancestors 'none';
       upgrade-insecure-requests;
     `.replace(/\s{2,}/g, ' ').trim();
     
     const requestHeaders = new Headers(request.headers);
     requestHeaders.set('x-nonce', nonce);
     requestHeaders.set('Content-Security-Policy', cspHeader);

     const response = NextResponse.next({
       request: {
         headers: requestHeaders,
       },
     });
     response.headers.set('Content-Security-Policy', cspHeader);
     return response;
   }
   ```

3. **Rate Limiting (API Routes)**:
   - Prevent abuse with simple in-memory rate limiting.
   ```ts
   // lib/rate-limit.ts
   const rateLimit = new Map();
   
   export function checkRateLimit(ip: string, limit = 10) {
     const now = Date.now();
     const windowMs = 60 * 1000; // 1 minute
     const record = rateLimit.get(ip) || { count: 0, resetTime: now + windowMs };
     
     if (now > record.resetTime) {
       record.count = 1;
       record.resetTime = now + windowMs;
     } else {
       record.count++;
     }
     
     rateLimit.set(ip, record);
     return record.count <= limit;
   }
   ```

4. **Pro Tips**:
   - Never commit `.env` files.
   - Regularly audit your dependencies: `npm audit fix`.