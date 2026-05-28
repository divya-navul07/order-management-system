# Order Management System

A production-ready full-stack e-commerce order management platform demonstrating modern software development practices, scalable architecture, and DevOps expertise.

## 🎯 Project Overview

This application manages the complete order lifecycle for an e-commerce platform, from product browsing to order fulfillment. It showcases:

- **Scalable Microservices Architecture** with Spring Boot
- **RESTful APIs** with comprehensive error handling
- **React + TypeScript** frontend with responsive design
- **Database Optimization** with SQL query tuning and Redis caching
- **Docker & Kubernetes** containerization and orchestration
- **CI/CD Pipelines** with GitHub Actions
- **Real-time Updates** with WebSocket support

## 🏗️ Architecture

### Backend Services
```
order-management-system/
├── backend/
│   ├── src/main/java/com/ordersystem/
│   │   ├── controller/       # REST API endpoints
│   │   ├── service/          # Business logic
│   │   ├── repository/       # Data access layer
│   │   ├── entity/           # JPA entities
│   │   ├── dto/              # Data Transfer Objects
│   │   ├── exception/        # Custom exceptions
│   │   └── config/           # Spring configurations
│   ├── resources/
│   │   ├── application.yml   # Configuration
│   │   └── db/migration/     # Flyway migrations
│   └── pom.xml               # Maven dependencies
└── frontend/
    ├── src/
    │   ├── components/       # React components
    │   ├── pages/            # Page components
    │   ├── services/         # API clients
    │   ├── hooks/            # Custom React hooks
    │   ├── types/            # TypeScript interfaces
    │   └── App.tsx           # Main app
    ├── package.json
    └── tsconfig.json
```

## 🚀 Quick Start

### Prerequisites
- Java 17+
- Node.js 18+
- Docker & Docker Compose
- Maven

### Local Development with Docker Compose

```bash
# Clone the repository
git clone https://github.com/divya-navul07/order-management-system.git
cd order-management-system

# Start all services
docker-compose up -d

# Backend API: http://localhost:8080/api
# Frontend: http://localhost:3000
# PostgreSQL: localhost:5432
# Redis: localhost:6379
```

### Manual Setup

**Backend:**
```bash
cd backend
mvn clean install
mvn spring-boot:run
```

**Frontend:**
```bash
cd frontend
npm install
npm start
```

## 📋 Key Features

### Product Management
- Browse products with pagination and filtering
- Real-time inventory management
- Search with full-text capabilities

### Order Processing
- Multi-step order workflow (Pending → Processing → Shipped → Delivered)
- Shopping cart management
- Order history and tracking
- Invoice generation

### User Management
- JWT-based authentication
- Role-based access control (Admin, Customer)
- User profile management

### Performance Optimization
- Redis caching for frequently accessed data
- Database query optimization with proper indexing
- Lazy loading and pagination
- Connection pooling with HikariCP

### Admin Dashboard
- Real-time order analytics
- Sales metrics and reporting
- Inventory management
- User management

## 🔌 API Endpoints

### Authentication
```
POST   /api/auth/register      - Register new user
POST   /api/auth/login         - Login user
POST   /api/auth/refresh       - Refresh JWT token
```

### Products
```
GET    /api/products           - List all products
GET    /api/products/:id       - Get product details
POST   /api/products           - Create product (Admin)
PUT    /api/products/:id       - Update product (Admin)
DELETE /api/products/:id       - Delete product (Admin)
```

### Orders
```
GET    /api/orders             - Get user orders
GET    /api/orders/:id         - Get order details
POST   /api/orders             - Create new order
PUT    /api/orders/:id         - Update order status (Admin)
GET    /api/orders/:id/invoice - Download invoice
```

### Cart
```
GET    /api/cart               - Get cart items
POST   /api/cart/items         - Add item to cart
PUT    /api/cart/items/:id     - Update cart item quantity
DELETE /api/cart/items/:id     - Remove item from cart
POST   /api/cart/checkout      - Checkout
```

## 🛠️ Technology Stack

### Backend
- **Java 17** - Programming language
- **Spring Boot 3.x** - Framework
- **Spring Data JPA** - ORM
- **Spring Security** - Authentication & Authorization
- **PostgreSQL** - Primary database
- **Redis** - Caching layer
- **Flyway** - Database migrations
- **Lombok** - Code generation
- **JWT** - Token-based authentication
- **JUnit 5** - Testing

### Frontend
- **React 18** - UI library
- **TypeScript** - Type safety
- **Vite** - Build tool
- **React Router** - Navigation
- **Axios** - HTTP client
- **React Query** - Data fetching & caching
- **Zustand** - State management

### DevOps & Infrastructure
- **Docker** - Containerization
- **Docker Compose** - Local orchestration
- **Kubernetes** - Production orchestration
- **GitHub Actions** - CI/CD pipeline

## 📊 Database Schema

### Key Tables
- **users** - User accounts with authentication
- **products** - Product catalog
- **orders** - Order headers
- **order_items** - Order line items
- **cart_items** - Shopping cart
- **inventory** - Stock management
- **invoices** - Order invoices

### Relationships
```
Users (1) ──── (N) Orders
       └── (N) CartItems

Products (1) ──── (N) OrderItems
        ├── (1) Inventory
        └── (N) CartItems

Orders (1) ──── (N) OrderItems
```

## 🔒 Security Features

- JWT token-based authentication
- Password encryption with bcrypt
- SQL injection prevention with parameterized queries
- CORS configuration
- Rate limiting on API endpoints
- Input validation and sanitization
- Role-based access control (RBAC)
- Secure headers (CSP, X-Frame-Options, etc.)

## 📈 Performance Optimizations

1. **Database Query Optimization**
   - Indexed columns for fast lookups
   - Proper JOIN strategies
   - Query result caching with Redis

2. **Caching Strategy**
   - Product catalog caching
   - User session caching
   - Inventory cache invalidation

3. **Frontend Optimization**
   - Code splitting and lazy loading
   - Image optimization
   - React Query for efficient data fetching

4. **Backend Optimization**
   - Connection pooling (HikariCP)
   - Request/Response compression
   - Async processing for long-running tasks

## 🧪 Testing

```bash
# Backend unit tests
cd backend
mvn test

# Backend integration tests
mvn verify

# Frontend tests
cd frontend
npm test
```

## 📦 Deployment

### Docker Build
```bash
# Build backend image
docker build -t order-management-backend:latest ./backend

# Build frontend image
docker build -t order-management-frontend:latest ./frontend
```

### Docker Compose
```bash
docker-compose up -d
```

### Kubernetes Deployment
```bash
kubectl apply -f k8s/
```

## 📚 Documentation

- **[API Documentation](./docs/API.md)** - Detailed API reference
- **[Architecture Guide](./docs/ARCHITECTURE.md)** - System design and decisions
- **[Development Setup](./backend/README.md)** - Backend development guide
- **[Frontend Setup](./frontend/README.md)** - Frontend development guide

## 🎓 Learning Outcomes

This project demonstrates:

✅ **Full-stack Development** - From database to UI  
✅ **Scalable Architecture** - Microservices patterns and best practices  
✅ **Performance Optimization** - Query tuning, caching strategies  
✅ **DevOps & Cloud** - Docker, Kubernetes, CI/CD automation  
✅ **Security** - Authentication, authorization, secure coding  
✅ **Code Quality** - Clean code, design patterns, testing  
✅ **Professional Practices** - Documentation, version control, collaboration  

## 🚦 Project Status

- [x] Backend API scaffolding
- [x] Frontend scaffolding
- [x] Database schema
- [x] Docker configuration
- [x] Documentation
- [ ] Authentication system (In Progress)
- [ ] Product management (In Progress)
- [ ] Order processing (In Progress)
- [ ] CI/CD pipeline (In Progress)
- [ ] Advanced features (Planned)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

MIT License - feel free to use this project for personal or commercial purposes.

## 👨‍💻 Author

**Divya Navul** - Software Developer  
Experienced in full-stack development, cloud infrastructure, and microservices architecture.

---

**Repository:** [https://github.com/divya-navul07/order-management-system](https://github.com/divya-navul07/order-management-system)

**For questions or suggestions, feel free to open an issue or reach out!**
