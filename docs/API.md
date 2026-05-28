# API Documentation

## Base URL

```
http://localhost:8080/api
```

## Authentication

All endpoints except `/auth/*` require JWT token in the Authorization header:

```
Authorization: Bearer <your_jwt_token>
```

## Response Format

### Successful Response
```json
{
  "success": true,
  "data": {},
  "message": "Operation successful"
}
```

### Error Response
```json
{
  "success": false,
  "error": "Error message",
  "timestamp": "2024-01-10T12:00:00Z"
}
```

## Endpoints

### Authentication

#### Register User
```
POST /auth/register
Content-Type: application/json

{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "securepassword123",
  "firstName": "John",
  "lastName": "Doe"
}
```

**Response:** 201 Created
```json
{
  "success": true,
  "data": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com",
    "role": "CUSTOMER"
  },
  "message": "User registered successfully"
}
```

#### Login
```
POST /auth/login
Content-Type: application/json

{
  "username": "john_doe",
  "password": "securepassword123"
}
```

**Response:** 200 OK
```json
{
  "success": true,
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
      "id": 1,
      "username": "john_doe",
      "email": "john@example.com",
      "role": "CUSTOMER"
    }
  },
  "message": "Login successful"
}
```

### Products

#### List Products
```
GET /products?page=0&size=10&category=electronics&search=laptop

Query Parameters:
  - page (optional): Page number (default: 0)
  - size (optional): Items per page (default: 10)
  - category (optional): Filter by category
  - search (optional): Search by name or SKU
```

**Response:** 200 OK
```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Laptop",
      "description": "High-performance laptop",
      "price": 1299.99,
      "category": "electronics",
      "sku": "LAP-001",
      "imageUrl": "https://example.com/laptop.jpg",
      "isActive": true
    }
  ],
  "message": "Products retrieved successfully"
}
```

#### Get Product Details
```
GET /products/{id}
```

**Response:** 200 OK
```json
{
  "success": true,
  "data": {
    "id": 1,
    "name": "Laptop",
    "description": "High-performance laptop",
    "price": 1299.99,
    "category": "electronics",
    "sku": "LAP-001",
    "imageUrl": "https://example.com/laptop.jpg",
    "isActive": true
  },
  "message": "Product retrieved successfully"
}
```

### Orders

#### Create Order
```
POST /orders
Content-Type: application/json

{
  "shippingAddress": "123 Main St",
  "shippingCity": "New York",
  "shippingState": "NY",
  "shippingZip": "10001",
  "items": [
    {
      "productId": 1,
      "quantity": 2
    }
  ]
}
```

**Response:** 201 Created
```json
{
  "success": true,
  "data": {
    "id": 1,
    "orderNumber": "ORD-20240110-001",
    "status": "PENDING",
    "totalAmount": 2599.98,
    "createdAt": "2024-01-10T12:00:00Z"
  },
  "message": "Order created successfully"
}
```

#### Get User Orders
```
GET /orders?page=0&size=10&status=PENDING

Query Parameters:
  - page (optional): Page number
  - size (optional): Items per page
  - status (optional): Filter by status (PENDING, PROCESSING, SHIPPED, DELIVERED, CANCELLED)
```

**Response:** 200 OK
```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "orderNumber": "ORD-20240110-001",
      "status": "PENDING",
      "totalAmount": 2599.98,
      "createdAt": "2024-01-10T12:00:00Z"
    }
  ],
  "message": "Orders retrieved successfully"
}
```

#### Get Order Details
```
GET /orders/{id}
```

**Response:** 200 OK
```json
{
  "success": true,
  "data": {
    "id": 1,
    "orderNumber": "ORD-20240110-001",
    "status": "PENDING",
    "totalAmount": 2599.98,
    "shippingAddress": "123 Main St",
    "shippingCity": "New York",
    "items": [
      {
        "productId": 1,
        "productName": "Laptop",
        "quantity": 2,
        "unitPrice": 1299.99,
        "subtotal": 2599.98
      }
    ],
    "createdAt": "2024-01-10T12:00:00Z"
  },
  "message": "Order retrieved successfully"
}
```

### Cart

#### Get Cart
```
GET /cart
```

#### Add to Cart
```
POST /cart/items
Content-Type: application/json

{
  "productId": 1,
  "quantity": 2
}
```

#### Update Cart Item
```
PUT /cart/items/{itemId}
Content-Type: application/json

{
  "quantity": 3
}
```

#### Remove from Cart
```
DELETE /cart/items/{itemId}
```

## HTTP Status Codes

| Code | Description |
|------|-------------|
| 200 | OK - Successful GET request |
| 201 | Created - Successful resource creation |
| 204 | No Content - Successful DELETE request |
| 400 | Bad Request - Invalid request data |
| 401 | Unauthorized - Missing or invalid token |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource not found |
| 409 | Conflict - Resource already exists |
| 500 | Internal Server Error - Server error |

## Error Codes

| Code | Description |
|------|-------------|
| VALIDATION_ERROR | Input validation failed |
| NOT_FOUND | Resource not found |
| UNAUTHORIZED | Authentication required |
| FORBIDDEN | Access denied |
| CONFLICT | Resource conflict |
| INTERNAL_ERROR | Server error |
