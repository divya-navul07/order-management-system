# Architecture Overview

## System Design

This is a full-stack e-commerce order management system built with modern, scalable technologies.

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                   Client (React + TypeScript)                │
│                    Running on Port 3000                      │
└────────────────────────────┬────────────────────────────────┘
                             │ HTTPS
                             ▼
┌─────────────────────────────────────────────────────────────┐
│              API Gateway / Load Balancer                     │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐   │
│  │      Spring Boot REST API (Port 8080)               │   │
│  │                                                      │   │
│  │  ┌────────────┐  ┌────────────┐  ┌────────────┐    │   │
│  │  │ Auth       │  │ Product    │  │ Order      │    │   │
│  │  │ Controller │  │ Controller │  │ Controller │    │   │
│  │  └────────────┘  └────────────┘  └────────────┘    │   │
│  │         ▼              ▼               ▼           │   │
│  │  ┌────────────────────────────────────────────┐   │   │
│  │  │         Service Layer                      │   │   │
│  │  │  - Business Logic                         │   │   │
│  │  │  - Validation                             │   │   │
│  │  │  - Transaction Management                 │   │   │
│  │  └────────────────────────────────────────────┘   │   │
│  │         ▼                                          │   │
│  │  ┌────────────────────────────────────────────┐   │   │
│  │  │    Data Access Layer (JPA Repository)      │   │   │
│  │  └────────────────────────────────────────────┘   │   │
│  └──────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                      ▼              ▼
        ┌──────────────────┐  ┌──────────────┐
        │   PostgreSQL DB  │  │   Redis      │
        │   (Primary)      │  │   (Cache)    │
        └──────────────────┘  └──────────────┘
```

## Backend Architecture - Layered Design

### 1. Controller Layer
- REST API endpoints for auth, products, orders, and cart
- Request/response handling with DTOs
- Input validation annotations
- HTTP status code management

### 2. Service Layer
- Business logic encapsulation
- Transaction management with @Transactional
- Data processing and validation
- Cross-cutting concerns

### 3. Repository Layer
- Data access abstraction using Spring Data JPA
- Custom query methods for performance
- Relationship management
- Query optimization

### 4. Entity Layer
- JPA annotated entities
- Database mappings and relationships
- Validation annotations
- Audit fields (createdAt, updatedAt)

## Frontend Architecture

### Component Structure
```
App.tsx
├── Pages/
│   ├── Login
│   ├── Register
│   ├── Dashboard
│   ├── Products
│   ├── Cart
│   └── Orders
├── Components/
│   ├── Header
│   ├── Sidebar
│   ├── ProductCard
│   └── OrderTable
├── Services/
│   ├── api.ts (Axios instance)
│   ├── authService.ts
│   └── orderService.ts
├── Store/ (Zustand)
│   ├── authStore
│   ├── cartStore
│   └── orderStore
└── Types/
    ├── user.ts
    ├── product.ts
    └── order.ts
```

### State Management Strategy
- **Zustand** for global state (auth, cart)
- **React Query** for server state (products, orders)
- **Local state** for component-specific data

## Database Design

### Entity Relationships
```
Users (1) ──────── (N) Orders
             ├── (N) OrderItems
             └── (N) CartItems

Products (1) ───── (N) OrderItems
          ├── (1) Inventory
          └── (N) CartItems

Orders (1) ──── (N) OrderItems
      └── (1) Invoice
```

### Indexing Strategy
- **Primary Keys**: All ID columns
- **Foreign Keys**: user_id, product_id, order_id
- **Filter Columns**: status, is_active, category
- **Sort Columns**: created_at
- **Search Columns**: email, username, sku

## Performance Optimization

### Caching Layer
- **Redis** for frequently accessed data
- **Cache-aside pattern** for products
- **TTL-based invalidation** for inventory changes
- **User session caching**

### Database Optimization
- **Connection pooling** (HikariCP with 20 max connections)
- **Query optimization** with proper indexes
- **Lazy loading** with JPA fetch strategies
- **Pagination** for all list endpoints
- **Batch processing** for bulk operations

### API Optimization
- **Response compression** (gzip)
- **JSON serialization** optimization
- **Request validation** early in pipeline
- **Async processing** for long-running tasks

## Security Architecture

### Authentication
- **JWT tokens** for stateless authentication
- **Refresh tokens** for token rotation
- **BCrypt** for password hashing (10 salt rounds)

### Authorization
- **Role-based access control** (RBAC)
- **@PreAuthorize** method-level security
- **Resource-level access checks**

### API Security
- **CORS** configuration for allowed origins
- **CSRF** protection enabled
- **Input validation** with Bean Validation
- **SQL injection** prevention with parameterized queries
- **XSS** prevention with JSON encoding

## Deployment Architecture

### Docker Containerization
- **Backend**: Java Spring Boot container
- **Frontend**: Node.js with serve
- **Database**: PostgreSQL 15 Alpine
- **Cache**: Redis 7 Alpine

### Kubernetes Orchestration (Optional)
- Service discovery
- Load balancing
- Auto-scaling based on metrics
- Health checks and liveness probes

## Scalability Considerations

1. **Horizontal Scaling**: Stateless backend services
2. **Caching Layer**: Redis reduces database load
3. **Database Optimization**: Proper indexing and query tuning
4. **Async Processing**: For long-running tasks
5. **Load Balancing**: Distribute traffic across instances
6. **Connection Pooling**: HikariCP for efficient database connections

## Monitoring & Logging

- **Spring Actuator** for metrics and health checks
- **Centralized logging** with configured log files
- **Performance monitoring** with custom metrics
- **Error tracking** and alerting
