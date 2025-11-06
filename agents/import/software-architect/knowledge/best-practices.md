# Best Practices Guide

Praktische best practices voor performance, security, scalability, en maintainability.

---

## Performance Optimization

### Frontend Performance

#### 1. **Bundle Optimization**
```javascript
// Code splitting
const Dashboard = lazy(() => import('./Dashboard'));

// Tree shaking
import { specific } from 'library';  // ✅
import * as all from 'library';      // ❌

// Dynamic imports
if (condition) {
  const module = await import('./heavy-module');
}
```

#### 2. **Image Optimization**
- Use WebP format (90% smaller than JPEG)
- Lazy load images below fold
- Responsive images met srcset
- Use CDN voor images (Cloudinary, Imgix)

```html
<img
  src="small.webp"
  srcset="medium.webp 768w, large.webp 1024w"
  loading="lazy"
  alt="Description"
/>
```

#### 3. **Caching Strategies**
```javascript
// Service Worker caching
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});

// Browser caching headers
Cache-Control: public, max-age=31536000, immutable  // Static assets
Cache-Control: no-cache                             // HTML
Cache-Control: private, max-age=3600                // User data
```

#### 4. **Rendering Patterns**
| Pattern | Use Case | FCP | TTI |
|---------|----------|-----|-----|
| **CSR** (Client-Side) | Apps, dashboards | Slow | Slow |
| **SSR** (Server-Side) | SEO-critical | Fast | Medium |
| **SSG** (Static) | Content sites | Fast | Fast |
| **ISR** (Incremental) | E-commerce | Fast | Fast |

### Backend Performance

#### 1. **Database Optimization**
```sql
-- Add indexes
CREATE INDEX idx_user_email ON users(email);
CREATE INDEX idx_order_created ON orders(created_at);

-- Query optimization
SELECT id, name FROM users WHERE email = ?;  -- ✅ Specific columns
SELECT * FROM users;                         -- ❌ Select all

-- Avoid N+1 queries
SELECT posts.*, users.name
FROM posts
JOIN users ON posts.user_id = users.id;     -- ✅ JOIN

-- Instead of:
posts.forEach(post => {
  post.author = await User.find(post.user_id);  -- ❌ N queries
});
```

#### 2. **Caching Layers**
```
┌─────────┐
│ Client  │ Browser cache (Service Worker)
└────┬────┘
     │
┌────▼────┐
│   CDN   │ Edge cache (Cloudflare, Fastly)
└────┬────┘
     │
┌────▼────┐
│API/App  │ Application cache (Redis, Memcached)
└────┬────┘
     │
┌────▼────┐
│Database │ Query cache (built-in DB cache)
└─────────┘
```

#### 3. **Rate Limiting**
```javascript
import rateLimit from 'express-rate-limit';

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // Max 100 requests per IP
  message: 'Too many requests'
});

app.use('/api/', limiter);
```

#### 4. **Connection Pooling**
```javascript
// Database connection pool
const pool = new Pool({
  max: 20,                // Max connections
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000,
});
```

---

## Security Best Practices

### OWASP Top 10 Protection

#### 1. **Injection Prevention**
```javascript
// SQL Injection - Use parameterized queries
// ❌ BAD
const query = `SELECT * FROM users WHERE email = '${email}'`;

// ✅ GOOD
const query = 'SELECT * FROM users WHERE email = ?';
db.query(query, [email]);

// NoSQL Injection
// ❌ BAD
db.find({ username: req.body.username });

// ✅ GOOD
const username = String(req.body.username);
db.find({ username });
```

#### 2. **XSS Prevention**
```javascript
// Sanitize user input
import DOMPurify from 'dompurify';

const clean = DOMPurify.sanitize(userInput);

// Use framework escaping
// React automatically escapes
<div>{userInput}</div>  // ✅ Safe

// Dangerous HTML
<div dangerouslySetInnerHTML={{ __html: userInput }} />  // ⚠️ Only for trusted content
```

#### 3. **CSRF Protection**
```javascript
import csrf from 'csurf';

app.use(csrf({ cookie: true }));

app.get('/form', (req, res) => {
  res.render('form', { csrfToken: req.csrfToken() });
});

// In HTML
<form method="POST">
  <input type="hidden" name="_csrf" value="{{csrfToken}}">
</form>
```

#### 4. **Authentication & Authorization**
```javascript
// Hash passwords
import bcrypt from 'bcrypt';

const hashedPassword = await bcrypt.hash(password, 10);
const isValid = await bcrypt.compare(password, hashedPassword);

// JWT best practices
const token = jwt.sign(
  { userId: user.id },
  process.env.JWT_SECRET,
  {
    expiresIn: '15m',      // Short expiry
    algorithm: 'HS256'
  }
);

// Store refresh token in httpOnly cookie
res.cookie('refreshToken', refreshToken, {
  httpOnly: true,          // No JS access
  secure: true,            // HTTPS only
  sameSite: 'strict',      // CSRF protection
  maxAge: 7 * 24 * 60 * 60 * 1000  // 7 days
});
```

#### 5. **Security Headers**
```javascript
import helmet from 'helmet';

app.use(helmet());

// Or manually:
app.use((req, res, next) => {
  res.setHeader('X-Content-Type-Options', 'nosniff');
  res.setHeader('X-Frame-Options', 'DENY');
  res.setHeader('X-XSS-Protection', '1; mode=block');
  res.setHeader('Strict-Transport-Security', 'max-age=31536000');
  res.setHeader('Content-Security-Policy', "default-src 'self'");
  next();
});
```

#### 6. **Input Validation**
```javascript
import { z } from 'zod';

const userSchema = z.object({
  email: z.string().email(),
  age: z.number().min(18).max(120),
  username: z.string().min(3).max(20).regex(/^[a-zA-Z0-9_]+$/)
});

const result = userSchema.safeParse(req.body);
if (!result.success) {
  return res.status(400).json(result.error);
}
```

### Environment Variables
```javascript
// ❌ NEVER commit secrets
const apiKey = 'sk_live_abc123';

// ✅ Use env variables
const apiKey = process.env.STRIPE_API_KEY;

// ✅ Validate required env vars at startup
const requiredEnvVars = ['DATABASE_URL', 'JWT_SECRET', 'STRIPE_API_KEY'];
requiredEnvVars.forEach(varName => {
  if (!process.env[varName]) {
    throw new Error(`Missing required env var: ${varName}`);
  }
});
```

---

## Scalability Patterns

### Horizontal Scaling

#### 1. **Load Balancing**
```
       ┌─────────────┐
       │Load Balancer│
       └──────┬──────┘
              │
     ┌────────┼────────┐
     │        │        │
  ┌──▼──┐  ┌──▼──┐  ┌──▼──┐
  │App 1│  │App 2│  │App 3│
  └─────┘  └─────┘  └─────┘
```

#### 2. **Database Replication**
```
      ┌─────────┐
      │ Primary │ (writes)
      └────┬────┘
           │
    ┌──────┼──────┐
    │      │      │
┌───▼──┐ ┌─▼───┐ ┌─▼───┐
│Read 1│ │Read│ │Read 3│ (reads)
└──────┘ └─────┘ └─────┘
```

#### 3. **Caching Strategy**
```javascript
async function getUser(id) {
  // Check cache first
  const cached = await redis.get(`user:${id}`);
  if (cached) return JSON.parse(cached);

  // Cache miss - fetch from DB
  const user = await db.users.findById(id);

  // Store in cache
  await redis.setex(`user:${id}`, 3600, JSON.stringify(user));

  return user;
}
```

#### 4. **Database Sharding**
```
Shard by user ID:
- Shard 1: users 0-999999
- Shard 2: users 1000000-1999999
- Shard 3: users 2000000-2999999

function getShardForUser(userId) {
  return Math.floor(userId / 1000000);
}
```

### Async Processing

#### Message Queues
```javascript
// Producer
await queue.publish('send-email', {
  to: 'user@example.com',
  subject: 'Welcome!',
  body: 'Thanks for signing up'
});

// Consumer
queue.subscribe('send-email', async (job) => {
  await emailService.send(job.data);
});
```

#### Background Jobs
```javascript
// Use Bull/BullMQ for Node.js
import { Queue } from 'bullmq';

const emailQueue = new Queue('emails');

// Add job
await emailQueue.add('welcome-email', {
  userId: '123'
}, {
  attempts: 3,
  backoff: {
    type: 'exponential',
    delay: 2000
  }
});

// Process job
const worker = new Worker('emails', async (job) => {
  await sendEmail(job.data.userId);
});
```

---

## Maintainability

### Code Quality

#### 1. **SOLID Principles**

**S - Single Responsibility**
```javascript
// ❌ BAD - Multiple responsibilities
class User {
  save() { /* DB logic */ }
  sendEmail() { /* Email logic */ }
  generateReport() { /* Report logic */ }
}

// ✅ GOOD - Single responsibility
class User { /* Just user data */ }
class UserRepository { save() { } }
class EmailService { send() { } }
class ReportGenerator { generate() { } }
```

**O - Open/Closed**
```javascript
// ✅ Open for extension, closed for modification
class PaymentProcessor {
  process(payment: Payment, method: PaymentMethod) {
    return method.processPayment(payment);
  }
}

class StripePayment implements PaymentMethod {
  processPayment(payment: Payment) { }
}

class PayPalPayment implements PaymentMethod {
  processPayment(payment: Payment) { }
}
```

**L - Liskov Substitution**
```javascript
// Base class behavior must work for derived classes
class Bird {
  fly() { /* implementation */ }
}

// ❌ BAD - Penguin can't fly
class Penguin extends Bird {
  fly() { throw new Error("Can't fly"); }
}

// ✅ GOOD - Separate interfaces
interface Flyable { fly(): void }
interface Swimmable { swim(): void }

class Sparrow implements Flyable { }
class Penguin implements Swimmable { }
```

**D - Dependency Inversion**
```javascript
// ❌ BAD - High-level depends on low-level
class UserService {
  private db = new MySQLDatabase();  // Tightly coupled
}

// ✅ GOOD - Both depend on abstraction
interface Database { query(sql: string): any }

class UserService {
  constructor(private db: Database) { }
}
```

#### 2. **DRY (Don't Repeat Yourself)**
```javascript
// ❌ BAD - Repetition
if (user.age >= 18 && user.country === 'US') { }
if (user.age >= 18 && user.country === 'US') { }

// ✅ GOOD - Extract
function isEligibleUser(user) {
  return user.age >= 18 && user.country === 'US';
}
```

#### 3. **Clean Functions**
```javascript
// ❌ BAD - Long function, unclear
function processOrder(order) {
  // 100 lines of code
}

// ✅ GOOD - Small, focused
function processOrder(order) {
  validateOrder(order);
  calculateTotal(order);
  applyDiscounts(order);
  chargePayment(order);
  sendConfirmation(order);
}
```

### Testing Strategy

#### Test Pyramid
```
        ┌────────┐
        │ E2E    │  10%  (Slow, expensive)
        └────────┘
      ┌──────────┐
      │Integration│  20%  (Medium speed)
      └──────────┘
    ┌──────────────┐
    │  Unit Tests  │  70%  (Fast, cheap)
    └──────────────┘
```

#### Testing Best Practices
```javascript
// Unit test
describe('calculateTotal', () => {
  it('should sum item prices', () => {
    const items = [
      { price: 10 },
      { price: 20 }
    ];
    expect(calculateTotal(items)).toBe(30);
  });

  it('should return 0 for empty array', () => {
    expect(calculateTotal([])).toBe(0);
  });
});

// Integration test
describe('UserAPI', () => {
  it('should create user and return 201', async () => {
    const response = await request(app)
      .post('/api/users')
      .send({ email: 'test@example.com' });

    expect(response.status).toBe(201);
    expect(response.body).toHaveProperty('id');
  });
});

// E2E test
test('user can complete checkout', async ({ page }) => {
  await page.goto('/products');
  await page.click('[data-testid="add-to-cart"]');
  await page.goto('/checkout');
  await page.fill('#credit-card', '4242424242424242');
  await page.click('[data-testid="complete-order"]');
  await expect(page.locator('.success-message')).toBeVisible();
});
```

### Documentation

#### Code Comments
```javascript
// ❌ BAD - Obvious comment
// Increment i by 1
i++;

// ✅ GOOD - Explains WHY
// We skip the first item because it's always the header
for (let i = 1; i < items.length; i++) { }

// ✅ GOOD - Explains complex logic
// Binary search requires sorted array. We sort here instead of
// at insertion time because reads are 100x more frequent than writes.
items.sort((a, b) => a.value - b.value);
```

#### README Structure
```markdown
# Project Name

## What it does
Brief description (2-3 sentences)

## Quick Start
npm install
npm run dev

## Tech Stack
- Next.js 14
- PostgreSQL
- Tailwind CSS

## Project Structure
src/
├── app/          # Next.js pages
├── components/   # React components
└── lib/          # Utilities

## Environment Variables
DATABASE_URL=...
API_KEY=...

## Deployment
Deploy to Vercel: vercel deploy

## Contributing
See CONTRIBUTING.md
```

---

## Monitoring & Observability

### Key Metrics

#### 1. **Application Metrics**
```javascript
// Response time
const start = Date.now();
await processRequest(req);
const duration = Date.now() - start;
metrics.recordResponseTime(duration);

// Error rate
try {
  await process();
} catch (error) {
  metrics.incrementErrorCount();
  throw error;
}

// Throughput
metrics.incrementRequestCount();
```

#### 2. **Business Metrics**
- Daily/Monthly Active Users (DAU/MAU)
- Conversion rate
- Revenue per user
- Churn rate

#### 3. **Infrastructure Metrics**
- CPU usage
- Memory usage
- Disk I/O
- Network traffic

### Logging Best Practices

```javascript
// ❌ BAD
console.log('error');

// ✅ GOOD - Structured logging
logger.error('Failed to process payment', {
  userId: user.id,
  orderId: order.id,
  amount: order.total,
  error: error.message,
  timestamp: new Date().toISOString()
});

// Log levels
logger.debug('Debugging info');      // Development only
logger.info('User logged in');       // Important events
logger.warn('Deprecated API used');  // Warnings
logger.error('Payment failed');      // Errors
logger.fatal('Database unreachable');// Critical
```

### Alerting

```yaml
# Example alert rules
alerts:
  - name: HighErrorRate
    condition: error_rate > 1%
    duration: 5m
    severity: critical
    notification: pagerduty

  - name: SlowResponseTime
    condition: p95_response_time > 1s
    duration: 10m
    severity: warning
    notification: slack

  - name: HighMemoryUsage
    condition: memory_usage > 90%
    duration: 15m
    severity: warning
    notification: email
```

---

## Deployment Best Practices

### CI/CD Pipeline

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm ci
      - run: npm test
      - run: npm run lint

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm ci
      - run: npm run build
      - uses: actions/upload-artifact@v3
        with:
          name: build
          path: dist/

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/download-artifact@v3
      - run: |
          # Deploy to production
          vercel --prod
```

### Blue-Green Deployment

```
Phase 1:           Phase 2:           Phase 3:
┌─────────┐       ┌─────────┐       ┌─────────┐
│ Blue    │◄──┐   │ Blue    │       │ Blue    │
│ (v1.0)  │   │   │ (v1.0)  │       │ (v1.0)  │
└─────────┘   │   └─────────┘       └─────────┘
              │                           │
┌──────────┐  │   ┌─────────┐       ┌─────────┐
│Load      │──┘   │Load     │──┐    │Load     │──┐
│Balancer  │      │Balancer │  │    │Balancer │  │
└──────────┘      └─────────┘  │    └─────────┘  │
                                │                 │
              ┌─────────┐       │   ┌─────────┐  │
              │ Green   │       │   │ Green   │◄─┘
              │ (v1.1)  │       └──▶│ (v1.1)  │
              └─────────┘           └─────────┘
```

### Feature Flags

```javascript
import { FeatureFlag } from './feature-flags';

if (FeatureFlag.isEnabled('new-checkout')) {
  return <NewCheckout />;
} else {
  return <LegacyCheckout />;
}

// Gradual rollout
FeatureFlag.enable('new-checkout', {
  percentage: 10,        // 10% of users
  userIds: ['123', '456'] // Specific users
});
```

---

## Cost Optimization

### Cloud Cost Best Practices

1. **Right-size instances**: Don't over-provision
2. **Use spot instances**: For non-critical workloads (70% cheaper)
3. **Auto-scaling**: Scale down during low traffic
4. **Reserved instances**: 40-60% discount for predictable load
5. **Monitor unused resources**: Delete zombie resources

### Database Optimization

```javascript
// Use connection pooling
const pool = new Pool({ max: 10 });

// Batch inserts instead of individual
// ❌ BAD
for (const item of items) {
  await db.insert(item);  // N queries
}

// ✅ GOOD
await db.batchInsert(items);  // 1 query

// Use appropriate index
CREATE INDEX idx_user_email ON users(email);

// Archive old data
// Move orders > 1 year to archive table
```

---

## Key Takeaways

### Performance
- ⚡ Optimize what matters (use profiler first)
- 📦 Code split and lazy load
- 🎯 Cache aggressively
- 🖼️ Optimize images (WebP, lazy load)

### Security
- 🔒 Never trust user input (validate & sanitize)
- 🔑 Hash passwords (bcrypt, argon2)
- 🍪 Use httpOnly cookies for sensitive tokens
- 🛡️ Apply security headers (Helmet.js)

### Scalability
- 📈 Horizontal scaling > vertical scaling
- 🔄 Use message queues for async work
- 💾 Cache frequently accessed data
- 🗂️ Shard database when needed

### Maintainability
- 📝 Write tests (70% unit, 20% integration, 10% E2E)
- 🧹 Keep functions small and focused
- 📖 Document WHY, not WHAT
- 🔍 Monitor everything

**Remember**: Premature optimization is the root of all evil. Measure first, optimize second.
