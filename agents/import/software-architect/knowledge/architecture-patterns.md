# Architecture Patterns Guide

Uitgebreide gids voor software architectuur patronen met praktische trade-offs en implementatie strategieën.

---

## Table of Contents
1. [Monolithic Architecture](#monolithic-architecture)
2. [Microservices Architecture](#microservices-architecture)
3. [Event-Driven Architecture](#event-driven-architecture)
4. [Serverless Architecture](#serverless-architecture)
5. [JAMstack Architecture](#jamstack-architecture)
6. [Microfrontends](#microfrontends)
7. [Clean Architecture](#clean-architecture)
8. [Domain-Driven Design](#domain-driven-design)

---

## Monolithic Architecture

### Wat is het?
Alle componenten van de applicatie draaien in één process en delen dezelfde codebase, database, en deployment.

### Varianten

#### 1. **Traditional Monolith**
Alle code in één codebase, vaak met tight coupling tussen layers.

```
┌─────────────────────────────┐
│     Monolithic Application   │
│                              │
│  ┌──────────┐  ┌──────────┐ │
│  │   UI     │  │   API    │ │
│  └──────────┘  └──────────┘ │
│  ┌──────────┐  ┌──────────┐ │
│  │ Business │  │   Data   │ │
│  │  Logic   │  │  Access  │ │
│  └──────────┘  └──────────┘ │
└───────────┬─────────────────┘
            │
        ┌───▼────┐
        │Database│
        └────────┘
```

#### 2. **Modular Monolith**
Monolith met strikte module boundaries. Beste van beide werelden voor veel apps.

```
┌─────────────────────────────────────┐
│       Modular Monolith               │
│                                      │
│  ┌─────────┐  ┌─────────┐  ┌──────┐│
│  │ User    │  │ Product │  │Order ││
│  │ Module  │  │ Module  │  │Module││
│  └────┬────┘  └────┬────┘  └───┬──┘│
│       │            │            │   │
│       └────────────┴────────────┘   │
│              Shared Kernel          │
└───────────────┬─────────────────────┘
                │
            ┌───▼────┐
            │Database│
            └────────┘
```

### Strengths
- ✅ **Simpel**: Eén codebase, één deployment, één database
- ✅ **Development Speed**: Snel features toevoegen, geen network overhead
- ✅ **Debugging**: Easy om te debuggen, alles in één process
- ✅ **Transactions**: ACID transactions binnen één database
- ✅ **Testing**: Integration testing is straightforward
- ✅ **Deployment**: Single deployment artifact

### Weaknesses
- ❌ **Scaling**: Moet hele app schalen, niet individuele componenten
- ❌ **Technology Lock-in**: Moeilijk om verschillende tech stacks te gebruiken
- ❌ **Deployment Risk**: Kleine change vereist full redeploy
- ❌ **Team Scaling**: Moeilijk voor grote teams om parallel te werken
- ❌ **Complexity**: Kan spaghetti code worden zonder discipline

### Best For
- 🎯 Startups en MVPs (simpelheid > scaling)
- 🎯 Small to medium teams (< 20 developers)
- 🎯 Apps met consistente technology requirements
- 🎯 Business met simpele domain zonder duidelijke boundaries

### Migration Path
**Van Traditional → Modular Monolith**:
1. Identificeer domain boundaries
2. Introduceer module interfaces
3. Refactor naar strikte boundaries
4. Extract modules naar packages/libs
5. (Optioneel) Later split naar microservices

---

## Microservices Architecture

### Wat is het?
Applicatie opgesplitst in kleine, onafhankelijke services die elk hun eigen process en database hebben.

### Architecture Diagram

```
┌────────┐     ┌──────────┐     ┌─────────┐
│ Client │────▶│API       │────▶│Service  │
└────────┘     │Gateway   │     │Registry │
               └─────┬────┘     └────┬────┘
                     │               │
        ┌────────────┼───────────────┼────────────┐
        │            │               │            │
    ┌───▼───┐   ┌───▼───┐   ┌───▼───┐   ┌────▼───┐
    │User   │   │Product│   │Order  │   │Payment │
    │Service│   │Service│   │Service│   │Service │
    └───┬───┘   └───┬───┘   └───┬───┘   └────┬───┘
        │           │           │            │
    ┌───▼───┐   ┌───▼───┐   ┌───▼───┐   ┌────▼───┐
    │User DB│   │Prod DB│   │OrdDB  │   │Pay DB  │
    └───────┘   └───────┘   └───────┘   └────────┘
```

### Core Principles
1. **Single Responsibility**: Elke service doet één ding goed
2. **Autonomous**: Services kunnen onafhankelijk deployen
3. **Decentralized**: Geen centrale database, elke service own data
4. **Fault Isolated**: Failure in één service crasht niet hele systeem
5. **Technology Agnostic**: Services kunnen verschillende tech stacks gebruiken

### Strengths
- ✅ **Independent Scaling**: Schaal only wat nodig is
- ✅ **Technology Freedom**: Elke service kan eigen stack gebruiken
- ✅ **Team Autonomy**: Teams kunnen onafhankelijk werken
- ✅ **Fault Isolation**: Failure is geïsoleerd
- ✅ **Incremental Updates**: Deploy individuele services
- ✅ **Organizational Scaling**: Werkt voor grote teams (Conway's Law)

### Weaknesses
- ❌ **Complexity**: Distributed systems complexity (network, latency)
- ❌ **Data Consistency**: No ACID transactions across services
- ❌ **Testing**: Integration testing is complex
- ❌ **Debugging**: Distributed tracing nodig
- ❌ **Operational Overhead**: Monitoring, logging, orchestration
- ❌ **Network Overhead**: Service-to-service calls add latency

### Best For
- 🎯 Large organizations (> 50 developers)
- 🎯 Apps met duidelijke domain boundaries
- 🎯 Different scaling requirements per component
- 🎯 Teams die autonomy willen
- 🎯 Polyglot requirements (verschillende languages)

### Avoid When
- ⚠️ Je een startup bent (premature optimization)
- ⚠️ Domain boundaries niet duidelijk zijn
- ⚠️ Team geen distributed systems ervaring heeft
- ⚠️ Je geen DevOps/infrastructure capacity hebt

### Implementation Checklist
- [ ] **Service Discovery**: Consul, Eureka, Kubernetes DNS
- [ ] **API Gateway**: Kong, AWS API Gateway, Traefik
- [ ] **Inter-service Communication**: REST, gRPC, message queues
- [ ] **Distributed Tracing**: Jaeger, Zipkin, OpenTelemetry
- [ ] **Centralized Logging**: ELK Stack, Splunk, Datadog
- [ ] **Circuit Breaker**: Hystrix, Resilience4j
- [ ] **Container Orchestration**: Kubernetes, Docker Swarm

---

## Event-Driven Architecture

### Wat is het?
Services communiceren via asynchrone events. Producers sturen events, consumers reageren.

### Architecture Diagram

```
┌─────────┐        ┌──────────────┐        ┌─────────┐
│Producer │───────▶│  Event Bus   │───────▶│Consumer │
│Service 1│        │  (Kafka/RMQ) │        │Service A│
└─────────┘        └──────────────┘        └─────────┘
                          │
                          ├──────────────▶┌─────────┐
                          │               │Consumer │
                          │               │Service B│
                          │               └─────────┘
                          │
                          └──────────────▶┌─────────┐
                                          │Consumer │
                                          │Service C│
                                          └─────────┘
```

### Patterns

#### 1. **Event Notification**
Simpele notifications: "iets is gebeurd"
```javascript
// Producer
eventBus.publish('user.registered', { userId: '123' });

// Consumer
eventBus.subscribe('user.registered', (event) => {
  sendWelcomeEmail(event.userId);
});
```

#### 2. **Event-Carried State Transfer**
Event bevat alle data, consumers hoeven niet te fetch
```javascript
eventBus.publish('order.created', {
  orderId: '456',
  userId: '123',
  items: [...],
  total: 99.99
});
```

#### 3. **Event Sourcing**
Store alle state changes als events, rebuild state door events te replaying
```javascript
// Events
const events = [
  { type: 'CartCreated', cartId: '789' },
  { type: 'ItemAdded', cartId: '789', item: 'Book' },
  { type: 'ItemRemoved', cartId: '789', item: 'Book' },
  { type: 'CartCheckedOut', cartId: '789' }
];

// Rebuild state
const cart = events.reduce(applyEvent, {});
```

#### 4. **CQRS (Command Query Responsibility Segregation)**
Separate models voor reads en writes
```
┌─────────┐        ┌──────────┐
│Commands │───────▶│Write DB  │
│(writes) │        │(Event    │
└─────────┘        │ Store)   │
                   └────┬─────┘
                        │
                   ┌────▼─────┐
                   │Event Bus │
                   └────┬─────┘
                        │
                   ┌────▼─────┐
                   │Read DB   │◀────┌─────────┐
                   │(Projected│     │Queries  │
                   │  Views)  │     │(reads)  │
                   └──────────┘     └─────────┘
```

### Strengths
- ✅ **Decoupling**: Services don't know about each other
- ✅ **Scalability**: Easy om consumers toe te voegen
- ✅ **Resilience**: Offline consumers catch up later
- ✅ **Audit Trail**: Event log is complete history
- ✅ **Temporal Queries**: Kan state op elk moment in tijd reconstrueren

### Weaknesses
- ❌ **Complexity**: Harder om te debuggen (eventual consistency)
- ❌ **Event Versioning**: Breaking changes in events zijn lastig
- ❌ **Ordering**: Event ordering kan issues geven
- ❌ **Debugging**: Distributed tracing complex
- ❌ **Learning Curve**: Team moet async mindset hebben

### Best For
- 🎯 High-throughput systems
- 🎯 Apps met complex business logic
- 🎯 Audit requirements (banking, healthcare)
- 🎯 Real-time analytics
- 🎯 Microservices die losjes gekoppeld moeten zijn

### Technology Choices
- **Message Brokers**: Kafka, RabbitMQ, AWS SQS/SNS, Azure Service Bus
- **Event Store**: EventStoreDB, Kafka (can double as event store)
- **Stream Processing**: Kafka Streams, Apache Flink, AWS Kinesis

---

## Serverless Architecture

### Wat is het?
Applicatie draait als functions (FaaS) zonder server management. Pay-per-execution model.

### Architecture Diagram

```
┌────────┐
│ Client │
└───┬────┘
    │
┌───▼──────────┐
│  API Gateway │
└───┬──────────┘
    │
    ├──────────────┬──────────────┬──────────────┐
    │              │              │              │
┌───▼───┐      ┌───▼───┐      ┌───▼───┐      ┌───▼───┐
│Lambda │      │Lambda │      │Lambda │      │Lambda │
│Func A │      │Func B │      │Func C │      │Func D │
└───┬───┘      └───┬───┘      └───┬───┘      └───┬───┘
    │              │              │              │
    └──────────────┴──────────────┴──────────────┘
                   │
              ┌────▼─────┐
              │DynamoDB/ │
              │S3/RDS    │
              └──────────┘
```

### Core Concepts

#### 1. **Function as a Service (FaaS)**
```javascript
// AWS Lambda handler
export const handler = async (event) => {
  const userId = event.pathParameters.userId;
  const user = await db.getUser(userId);
  return {
    statusCode: 200,
    body: JSON.stringify(user)
  };
};
```

#### 2. **Backend as a Service (BaaS)**
Use managed services voor database, auth, storage:
- **Database**: DynamoDB, Firestore, Supabase
- **Auth**: Cognito, Auth0, Firebase Auth
- **Storage**: S3, Cloudflare R2

#### 3. **Event-Driven Triggers**
Functions triggered door events:
- HTTP requests (API Gateway)
- Database changes (DynamoDB Streams)
- File uploads (S3 events)
- Scheduled (CloudWatch Events/EventBridge)
- Queue messages (SQS)

### Strengths
- ✅ **No Server Management**: Geen infra te beheren
- ✅ **Auto-scaling**: Schaalt automatisch met load
- ✅ **Pay-per-use**: Only betalen voor executions
- ✅ **Fast Deployment**: Deploy functions in seconden
- ✅ **Built-in HA**: Highly available by default

### Weaknesses
- ❌ **Cold Starts**: First invocation kan langzaam zijn (100-1000ms)
- ❌ **Vendor Lock-in**: Moeilijk om te migreren tussen providers
- ❌ **Debugging**: Local development niet identiek aan cloud
- ❌ **Stateless**: No persistent connections (WebSockets lastig)
- ❌ **Timeouts**: Max execution time (AWS: 15min, Vercel: 60s-300s)
- ❌ **Cost**: Kan duur worden bij constant high traffic

### Best For
- 🎯 Intermittent workloads (niet constant traffic)
- 🎯 Event-driven workflows
- 🎯 Startups zonder DevOps capacity
- 🎯 APIs met variable load
- 🎯 Background jobs en scheduled tasks

### Avoid When
- ⚠️ Constant high traffic (traditional servers goedkoper)
- ⚠️ Low latency vereist (cold starts issue)
- ⚠️ Long-running processes (> 15min)
- ⚠️ WebSocket/real-time vereist
- ⚠️ Vendor lock-in dealbreaker is

### Providers
| Provider | Service | Max Timeout | Free Tier |
|----------|---------|-------------|-----------|
| AWS | Lambda | 15 min | 1M requests/month |
| Vercel | Functions | 60s (hobby) - 900s (pro) | 100GB-hours/month |
| Cloudflare | Workers | No limit (but CPU-time limited) | 100k requests/day |
| Netlify | Functions | 10s (free) - 26s (pro) | 125k requests/month |

---

## JAMstack Architecture

### Wat is het?
**J**avaScript + **A**PIs + **M**arkup. Pre-rendered static sites + client-side JS + API calls voor dynamic data.

### Architecture Diagram

```
┌──────────────────────────────────┐
│      Build Time (CI/CD)          │
│                                  │
│  ┌────────┐      ┌────────────┐ │
│  │ Static │─────▶│Pre-rendered│ │
│  │  Site  │      │   HTML     │ │
│  │Generator│      └──────┬─────┘ │
│  └────────┘             │       │
└──────────────────────────┼───────┘
                           │
                      ┌────▼─────┐
                      │   CDN    │
                      │(Vercel/  │
                      │Netlify)  │
                      └────┬─────┘
                           │
                    ┌──────▼──────┐
                    │   Browser   │
                    │             │
                    │  Hydrates + │
                    │  API Calls  │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  Headless   │
                    │  CMS / APIs │
                    │(Sanity/     │
                    │ Contentful) │
                    └─────────────┘
```

### Core Principles
1. **Pre-rendering**: Generate HTML at build time
2. **CDN Distribution**: Serve static files from edge
3. **API-driven**: Dynamic data via APIs
4. **Git-based Workflow**: Content in Git, deploy on push

### Patterns

#### 1. **Static Site Generation (SSG)**
```javascript
// Next.js getStaticProps
export async function getStaticProps() {
  const posts = await fetchPosts();
  return { props: { posts } };
}
```

#### 2. **Incremental Static Regeneration (ISR)**
```javascript
// Revalidate every 60 seconds
export async function getStaticProps() {
  const posts = await fetchPosts();
  return {
    props: { posts },
    revalidate: 60
  };
}
```

#### 3. **Client-side Data Fetching**
```javascript
// SWR or React Query
const { data } = useSWR('/api/user', fetcher);
```

### Strengths
- ✅ **Performance**: Pre-rendered = instant load
- ✅ **SEO**: HTML available immediately
- ✅ **Scalability**: CDN handles traffic spikes
- ✅ **Security**: No server = smaller attack surface
- ✅ **Developer Experience**: Git workflow, preview deploys
- ✅ **Cost**: CDN hosting is cheap

### Weaknesses
- ❌ **Build Times**: Large sites = long builds
- ❌ **Dynamic Content**: Not ideal for highly dynamic apps
- ❌ **Real-time**: Hard om real-time features te doen
- ❌ **Personalization**: User-specific content requires client-side

### Best For
- 🎯 Marketing websites
- 🎯 Blogs en documentation
- 🎯 E-commerce (producten pre-rendered)
- 🎯 Landing pages
- 🎯 Portfolio sites

### Tech Stack Examples

**Next.js + Sanity + Vercel**
```
┌──────────┐    ┌─────────┐    ┌────────┐
│ Next.js  │───▶│ Sanity  │───▶│Vercel  │
│  (SSG)   │    │  (CMS)  │    │ (CDN)  │
└──────────┘    └─────────┘    └────────┘
```

**Astro + Contentful + Netlify**
```
┌──────────┐    ┌────────────┐    ┌─────────┐
│  Astro   │───▶│Contentful  │───▶│Netlify  │
│  (SSG)   │    │   (CMS)    │    │  (CDN)  │
└──────────┘    └────────────┘    └─────────┘
```

---

## Microfrontends

### Wat is het?
Frontend opgesplitst in kleinere, onafhankelijke apps die elk eigen team en deployment hebben.

### Architecture Diagram

```
                ┌───────────────┐
                │  Shell App    │
                │ (Host/Router) │
                └───────┬───────┘
                        │
        ┌───────────────┼───────────────┐
        │               │               │
  ┌─────▼────┐    ┌─────▼────┐   ┌─────▼────┐
  │ Product  │    │ Checkout │   │ Account  │
  │   MFE    │    │   MFE    │   │   MFE    │
  │ (React)  │    │  (Vue)   │   │ (Angular)│
  └──────────┘    └──────────┘   └──────────┘
      │                │              │
  ┌───▼───┐        ┌───▼───┐      ┌───▼───┐
  │Team A │        │Team B │      │Team C │
  └───────┘        └───────┘      └───────┘
```

### Implementation Approaches

#### 1. **Build-time Integration**
NPM packages published en imported:
```javascript
// Shell app
import ProductMFE from '@company/product-mfe';
import CheckoutMFE from '@company/checkout-mfe';
```

❌ **Con**: Moet full redeploy bij change in micro-frontend

#### 2. **Run-time Integration via Module Federation**
Webpack Module Federation loads modules at runtime:
```javascript
// webpack.config.js (Shell)
new ModuleFederationPlugin({
  name: 'shell',
  remotes: {
    products: 'products@http://products.com/remoteEntry.js',
    checkout: 'checkout@http://checkout.com/remoteEntry.js'
  }
});
```

✅ **Pro**: Independent deployments

#### 3. **iframe Integration**
Each MFE in iframe:
```html
<iframe src="https://products.company.com"></iframe>
<iframe src="https://checkout.company.com"></iframe>
```

✅ **Pro**: Complete isolation
❌ **Con**: Performance overhead, styling issues

#### 4. **Web Components**
Standaard web components:
```javascript
// Define MFE
class ProductMFE extends HTMLElement {
  connectedCallback() {
    this.innerHTML = '<div>Products</div>';
  }
}
customElements.define('product-mfe', ProductMFE);

// Use in Shell
<product-mfe></product-mfe>
```

### Strengths
- ✅ **Team Autonomy**: Teams kunnen onafhankelijk werken
- ✅ **Technology Freedom**: Elk MFE kan eigen framework gebruiken
- ✅ **Independent Deployment**: Deploy zonder andere teams
- ✅ **Scalable Teams**: Organizational scaling (Conway's Law)

### Weaknesses
- ❌ **Complexity**: Much more complex dan monolithic frontend
- ❌ **Performance**: Multiple framework bundles = grotere payload
- ❌ **Consistency**: Hard om consistent UX te behouden
- ❌ **Shared State**: Cross-MFE state is challenging
- ❌ **Debugging**: Harder to debug across boundaries

### Best For
- 🎯 Large organizations (> 100 frontend developers)
- 🎯 Multiple teams owning different domains
- 🎯 Apps met duidelijke feature boundaries
- 🎯 Legacy modernization (gradual migration)

### Avoid When
- ⚠️ Small teams (< 20 developers)
- ⚠️ Performance is critical (bundle overhead)
- ⚠️ Tight UX consistency vereist
- ⚠️ Geen duidelijke domain boundaries

---

## Clean Architecture

### Wat is het?
Layered architecture met dependency rule: outer layers depend on inner layers, never reverse.

### Layer Diagram

```
        ┌─────────────────────────────┐
        │   Frameworks & Drivers      │
        │  (UI, DB, External APIs)    │
        └──────────────┬──────────────┘
                       │
        ┌──────────────▼──────────────┐
        │  Interface Adapters         │
        │  (Controllers, Presenters)  │
        └──────────────┬──────────────┘
                       │
        ┌──────────────▼──────────────┐
        │  Application Business Rules │
        │      (Use Cases)            │
        └──────────────┬──────────────┘
                       │
        ┌──────────────▼──────────────┐
        │  Enterprise Business Rules  │
        │       (Entities)            │
        └─────────────────────────────┘
```

### Dependency Rule
**Inner layers NEVER depend on outer layers**
- Entities know nothing about use cases
- Use cases know nothing about controllers
- Controllers know nothing about frameworks

### Example Structure
```
src/
├── domain/                 # Entities (innermost)
│   ├── User.ts
│   └── Product.ts
├── application/            # Use Cases
│   ├── CreateUser.ts
│   └── GetProduct.ts
├── infrastructure/         # Interface Adapters
│   ├── api/
│   │   └── UserController.ts
│   ├── database/
│   │   └── UserRepository.ts
│   └── external/
│       └── EmailService.ts
└── main.ts                 # Frameworks & Drivers
```

### Strengths
- ✅ **Testability**: Business logic isolated, easy to unit test
- ✅ **Independence**: Framework/DB changes don't affect business rules
- ✅ **Maintainability**: Clear separation of concerns
- ✅ **Flexibility**: Easy om external dependencies te swappen

### Weaknesses
- ❌ **Boilerplate**: Veel interfaces en adapters
- ❌ **Learning Curve**: Team moet pattern snappen
- ❌ **Overkill**: For simple CRUD apps

### Best For
- 🎯 Complex business logic
- 🎯 Long-lived applications
- 🎯 Apps waar requirements vaak wijzigen

---

## Domain-Driven Design (DDD)

### Wat is het?
Focus on business domain, model software naar real-world domain.

### Core Concepts

#### 1. **Ubiquitous Language**
Same terms gebruiken in code als in business
```javascript
// Bad
class CustomerRecord { }

// Good
class Customer { }
```

#### 2. **Bounded Contexts**
Domain opgesplitst in contexts met eigen models
```
┌────────────────┐  ┌────────────────┐  ┌────────────────┐
│  Sales Context │  │ Shipping       │  │  Accounting    │
│                │  │  Context       │  │  Context       │
│  Customer      │  │  Order         │  │  Invoice       │
│  Order         │  │  Shipment      │  │  Payment       │
└────────────────┘  └────────────────┘  └────────────────┘
```

#### 3. **Aggregates**
Cluster of entities treated as single unit
```javascript
class Order {  // Aggregate Root
  constructor(
    public id: OrderId,
    private items: OrderItem[],  // Part of aggregate
    private status: OrderStatus
  ) {}

  addItem(item: OrderItem) {
    // Business logic ensures invariants
    if (this.status !== 'DRAFT') {
      throw new Error('Cannot add items to non-draft order');
    }
    this.items.push(item);
  }
}
```

#### 4. **Value Objects**
Immutable objects zonder identity
```javascript
class Money {
  constructor(
    private amount: number,
    private currency: string
  ) {}

  add(other: Money): Money {
    if (this.currency !== other.currency) {
      throw new Error('Currency mismatch');
    }
    return new Money(this.amount + other.amount, this.currency);
  }
}
```

#### 5. **Domain Events**
Things that happened in the domain
```javascript
class OrderPlaced {
  constructor(
    public orderId: string,
    public customerId: string,
    public timestamp: Date
  ) {}
}
```

### Strengths
- ✅ **Business Alignment**: Code reflects real business
- ✅ **Complexity Management**: Handles complex domains well
- ✅ **Maintainability**: Clear boundaries and responsibilities

### Weaknesses
- ❌ **Overhead**: For simple CRUD apps
- ❌ **Learning Curve**: Team moet DDD patterns kennen
- ❌ **Time Investment**: Requires domain experts involvement

### Best For
- 🎯 Complex business domains
- 🎯 Large enterprise applications
- 🎯 Teams met access tot domain experts

---

## Architecture Decision Framework

### Startup (< 10 people)
✅ **Modular Monolith** + **JAMstack** (if frontend-heavy)
- Start simpel, split later als nodig
- Focus on shipping features, niet infra

### Scale-up (10-50 people)
✅ **Modular Monolith** or **Selective Microservices**
- Split only wat echt moet schalen apart
- Event-driven voor async workflows
- Monolith voor rest

### Enterprise (50-500+ people)
✅ **Microservices** + **Event-Driven** + **DDD**
- Bounded contexts → microservices
- Teams krijgen ownership
- Governance en standards belangrijk

### Decision Matrix

| Factor | Monolith | Microservices | Serverless |
|--------|----------|---------------|------------|
| Team Size | < 20 | > 50 | Any |
| Deployment Freq | Weekly | Daily/multiple | Continuous |
| Scaling Need | Vertical | Horizontal | Auto |
| DevOps Maturity | Low-Mid | High | Low |
| Domain Complexity | Simple-Mid | High | Simple-Mid |

---

## Migration Strategies

### 1. Strangler Fig Pattern
Gradually replace old system:
```
Phase 1: ┌──────────┐
         │Monolith  │
         │(100%)    │
         └──────────┘

Phase 2: ┌──────────┐  ┌──────┐
         │Monolith  │  │New   │
         │(70%)     │  │(30%) │
         └──────────┘  └──────┘

Phase 3: ┌──────────┐  ┌──────┐
         │Monolith  │  │New   │
         │(30%)     │  │(70%) │
         └──────────┘  └──────┘

Phase 4:                ┌──────┐
                        │New   │
                        │(100%)│
                        └──────┘
```

### 2. Feature Flags
Test nieuwe architecture in production:
```javascript
if (featureFlags.newCheckout) {
  return newCheckoutService.process(order);
} else {
  return legacyCheckout.process(order);
}
```

### 3. Branch by Abstraction
Introduce abstraction layer, swap implementation:
```javascript
// Before
database.query('SELECT * FROM users');

// Abstraction
interface UserRepository {
  findAll(): Promise<User[]>;
}

// Old implementation
class MySQLUserRepository implements UserRepository { }

// New implementation
class PostgreSQLUserRepository implements UserRepository { }
```

---

## Conclusion

**Start simple, evolve when needed.**

- 🎯 **Startup**: Monolith + JAMstack
- 🎯 **Growing**: Modular Monolith + Selective services
- 🎯 **Enterprise**: Microservices + Event-driven + DDD

**Architecture is about trade-offs, not right or wrong.**
