# 🏗️ Architecture Documentation

This document provides a detailed overview of the Food-Ordering-Delivery-Web-Application architecture.

## Table of Contents
- [System Architecture](#system-architecture)
- [Frontend Architecture](#frontend-architecture)
- [Backend Architecture](#backend-architecture)
- [Database Design](#database-design)
- [API Design](#api-design)
- [Security Architecture](#security-architecture)
- [Deployment Architecture](#deployment-architecture)

---

## System Architecture

### High-Level Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        Client Layer                              │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │              React Application (Port 3000)                 │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐ │ │
│  │  │  Components  │  │  Redux Store │  │  HTTP Services   │ │ │
│  │  └──────────────┘  └──────────────┘  └──────────────────┘ │ │
│  └─────────────────────────┬──────────────────────────────────┘ │
│                            │                                     │
└────────────────────────────┼─────────────────────────────────────┘
                             │ HTTP/REST
                             │ JWT Token
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API Gateway Layer                           │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │         Spring Boot Application (Port 8080)               │ │
│  │         CORS Configuration / Security Filters              │ │
│  └────────────────────────────────────────────────────────────┘ │
│                            │                                     │
└────────────────────────────┼─────────────────────────────────────┘
                             │
┌────────────────────────────┼─────────────────────────────────────┐
│                   Business Logic Layer                           │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                  Controllers Layer                         │  │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────┐  │  │
│  │  │  Meal    │ │ MealType │ │   User   │ │ FinalOrder │  │  │
│  │  │Controller│ │Controller│ │Controller│ │ Controller │  │  │
│  │  └──────────┘ └──────────┘ └──────────┘ └────────────┘  │  │
│  └───────────────────────────────────────────────────────────┘  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                   Services Layer                          │  │
│  │  (Business Logic, Validation, Authorization)             │  │
│  └───────────────────────────────────────────────────────────┘  │
│                            │                                     │
└────────────────────────────┼─────────────────────────────────────┘
                             │
┌────────────────────────────┼─────────────────────────────────────┐
│                   Data Access Layer                              │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │              JPA Repositories                             │  │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────┐  │  │
│  │  │  Meal    │ │ MealType │ │   User   │ │ FinalOrder │  │  │
│  │  │Repository│ │Repository│ │Repository│ │ Repository │  │  │
│  │  └──────────┘ └──────────┘ └──────────┘ └────────────┘  │  │
│  └───────────────────────────────────────────────────────────┘  │
│                            │                                     │
└────────────────────────────┼─────────────────────────────────────┘
                             │ JDBC
                             │ Hibernate ORM
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Database Layer                                │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │        MySQL Database (food_ordering_db)                  │ │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────┐  │ │
│  │  │  users   │ │  meals   │ │meal_types│ │final_orders│  │ │
│  │  └──────────┘ └──────────┘ └──────────┘ └────────────┘  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Frontend Architecture

### Component Hierarchy

```
App.js
├── NavbarComponent
├── Routes
│   ├── PublicRoutes
│   │   ├── MenuMealTypeComponent
│   │   ├── ListMealByMealTypeComponent
│   │   ├── CartComponent
│   │   ├── FinalOrderByIdComponent
│   │   └── RegistrationComponent
│   │
│   ├── PrivateRoutes (USER)
│   │   ├── MyProfileComponent
│   │   ├── MyActiveFinalOrdersComponent
│   │   ├── MyDeliveredFinalOrdersComponent
│   │   └── OrderHistoryComponent
│   │
│   ├── PrivateRoutes (EMPLOYEE)
│   │   ├── ActiveFinalOrdersComponent
│   │   └── OrderHistoryComponent
│   │
│   └── PrivateRoutes (ADMIN)
│       ├── ListMealComponent
│       ├── CreateMealComponent
│       ├── EditMealComponent
│       ├── ListMealTypeComponent
│       ├── CreateMealTypeComponent
│       ├── EditMealTypeComponent
│       ├── ListUserComponent
│       ├── ListEmployeeComponent
│       └── CreateEmployeeComponent
│
└── FooterComponent
```

### State Management (Redux)

```
Redux Store
├── cart (Redux Slice)
│   ├── items: []
│   ├── totalPrice: 0
│   └── itemCount: 0
│
├── auth (Local State)
│   ├── isAuthenticated: boolean
│   ├── user: User Object
│   ├── token: string
│   └── role: string
│
└── UI (Local State)
    ├── loading: boolean
    ├── error: string
    └── successMessage: string
```

### Data Flow

```
User Interaction
        │
        ▼
React Component
        │
        ▼
Event Handler / Dispatch Redux Action
        │
        ▼
API Service (Axios)
        │
    ┌───┴───┐
    │       │
HTTP Request    Response
    │           │
    ▼           ▼
Backend API    Parse JSON
    │           │
    ▼           ▼
Process    Update Redux Store
    │           │
Response        ▼
    │       Update Component State
    └──────►Render UI
```

### HTTP Interceptor

```
Request Flow:
┌──────────────┐
│ HTTP Request │
└──────┬───────┘
       │
       ▼
┌─────────────────────────────────┐
│ Interceptor                     │
│ - Add JWT Token to Header       │
│ - Add Content-Type Header       │
│ - Set Request Timeout           │
└──────┬──────────────────────────┘
       │
       ▼
┌──────────────────────┐
│ Send to Backend      │
└──────┬───────────────┘
       │
       ▼
┌──────────────────────┐
│ Receive Response     │
└──────┬───────────────┘
       │
       ▼
┌─────────────────────────────────┐
│ Interceptor                     │
│ - Check Status Code             │
│ - Handle 401 (Unauthorized)     │
│ - Handle Errors                 │
│ - Log Response                  │
└──────┬──────────────────────────┘
       │
       ▼
┌──────────────────────┐
│ Return to Component  │
└──────────────────────┘
```

---

## Backend Architecture

### Layered Architecture

```
┌──────────────────────────────────┐
│   Presentation Layer             │
│   (Controllers)                  │
│ - HTTP Request Handling          │
│ - Response Formatting            │
│ - Request Validation             │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│   Business Logic Layer           │
│   (Services)                     │
│ - Business Rules                 │
│ - Data Processing                │
│ - Authorization                  │
│ - Validation                     │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│   Data Access Layer              │
│   (Repositories)                 │
│ - CRUD Operations                │
│ - Database Queries               │
│ - Entity Mapping                 │
└──────────────┬───────────────────┘
               │
               ▼
┌──────────────────────────────────┐
│   Persistence Layer              │
│   (Database)                     │
│ - Data Storage                   │
│ - Data Retrieval                 │
└──────────────────────────────────┘
```

### Request Processing Pipeline

```
HTTP Request
    │
    ▼
┌─────────────────────────────────────┐
│ DispatcherServlet                   │
│ (Spring MVC Entry Point)            │
└────────────────┬────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────┐
│ Security Filters                    │
│ - JWT Token Validation              │
│ - Authentication                    │
│ - Authorization                     │
└────────────────┬────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────┐
│ CORS Filter                         │
│ (Cross-Origin Resource Sharing)     │
└────────────────┬────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────┐
│ Route Mapping & Controller          │
│ - Match URL to Controller Method    │
│ - Parameter Extraction              │
└────────────────┬────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────┐
│ Controller Method                   │
│ - Validate Input                    │
│ - Call Service                      │
│ - Prepare Response                  │
└────────────────┬────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────┐
│ Service Implementation              │
│ - Execute Business Logic            │
│ - Access Data via Repository        │
│ - Process Result                    │
└────────────────┬────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────┐
│ Repository/JPA                      │
│ - Execute Database Query            │
│ - Map Entity Objects                │
│ - Return Results                    │
└────────────────┬────────────────────┘
                 │
                 ▼
         MySQL Database
                 │
    ┌────────────┴────────────┐
    │                         │
    ▼                         ▼
 Response Processing      Entity Mapping
    │                         │
    └────────────┬────────────┘
                 │
                 ▼
        Return to Service
                 │
                 ▼
        Return to Controller
                 │
                 ▼
    Format JSON Response
                 │
                 ▼
        HTTP Response
```

### Entity Relationship Diagram

```
┌──────────────┐         ┌──────────────┐
│   Users      │         │    Roles     │
├──────────────┤         ├──────────────┤
│ id (PK)      │────┐    │ id (PK)      │
│ username     │    └───►│ role         │
│ password     │         │              │
│ email        │         └──────────────┘
│ phone        │
│ address      │
│ roleId (FK)  │
│ isDeleted    │
└──────────────┘

┌──────────────┐         ┌──────────────┐
│    Meals     │         │  MealTypes   │
├──────────────┤         ├──────────────┤
│ id (PK)      │────┐    │ id (PK)      │
│ name         │    └───►│ name         │
│ description  │         │ image        │
│ price        │         │ isDeleted    │
│ image        │         └──────────────┘
│ mealTypeId   │
│ isDeleted    │
└──────────────┘

┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│ FinalOrders  │    │ OrderItems   │    │    Meals     │
├──────────────┤    ├──────────────┤    ├──────────────┤
│ id (PK)      │    │ id (PK)      │    │ id (PK)      │
│ userId (FK)  │◄───│ orderId (FK) │    │ ...          │
│ totalPrice   │    │ mealId (FK)  ├───►│              │
│ address      │    │ quantity     │    └──────────────┘
│ phone        │    │ price        │
│ statusId     │    │              │
│ createdAt    │    └──────────────┘
│              │
└──────────────┘    ┌──────────────┐
       │            │   Status     │
       └───────────►├──────────────┤
                    │ id (PK)      │
                    │ status       │
                    │              │
                    └──────────────┘
```

---

## Database Design

### Schema Overview

#### Users Table
```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    phone VARCHAR(20),
    address VARCHAR(500),
    is_deleted BOOLEAN DEFAULT FALSE,
    role_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (role_id) REFERENCES roles(id)
);

CREATE INDEX idx_username ON users(username);
CREATE INDEX idx_email ON users(email);
```

#### Meals Table
```sql
CREATE TABLE meals (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    price DECIMAL(10, 2) NOT NULL,
    image LONGBLOB,
    is_deleted BOOLEAN DEFAULT FALSE,
    meal_type_id INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (meal_type_id) REFERENCES meal_types(id)
);

CREATE INDEX idx_meal_type_id ON meals(meal_type_id);
```

#### FinalOrders Table
```sql
CREATE TABLE final_orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    total_price DECIMAL(10, 2) NOT NULL,
    address VARCHAR(500) NOT NULL,
    phone VARCHAR(20) NOT NULL,
    status_id INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id),
    FOREIGN KEY (status_id) REFERENCES status(id)
);

CREATE INDEX idx_user_id ON final_orders(user_id);
CREATE INDEX idx_created_at ON final_orders(created_at);
```

---

## API Design

### REST Endpoints Structure

```
/api/v1
├── /auth
│   ├── POST   /login         - User login
│   ├── POST   /register      - User registration
│   └── POST   /logout        - User logout
│
├── /meals
│   ├── GET    /              - Get all meals (with pagination)
│   ├── GET    /{id}          - Get meal by ID
│   ├── POST   /              - Create meal (Admin)
│   ├── PUT    /{id}          - Update meal (Admin)
│   └── DELETE /{id}          - Delete meal (Admin)
│
├── /meal-types
│   ├── GET    /              - Get all categories
│   ├── GET    /{id}          - Get category by ID
│   ├── POST   /              - Create category (Admin)
│   ├── PUT    /{id}          - Update category (Admin)
│   └── DELETE /{id}          - Delete category (Admin)
│
├── /orders
│   ├── GET    /              - Get user orders
│   ├── GET    /{id}          - Get order by ID
│   ├── POST   /              - Create new order
│   ├── PUT    /{id}          - Update order status
│   ├── DELETE /{id}          - Delete order (Admin)
│   ├── GET    /history       - View order history
│   └── GET    /active        - View active orders
│
├── /users
│   ├── GET    /              - Get all users (Admin)
│   ├── GET    /{id}          - Get user by ID
│   ├── PUT    /{id}          - Update user profile
│   ├── DELETE /{id}          - Delete user (Admin)
│   └── GET    /{id}/orders   - Get user orders
│
└── /employees
    ├── GET    /              - Get all employees (Admin)
    ├── POST   /              - Create employee (Admin)
    ├── PUT    /{id}          - Update employee (Admin)
    └── DELETE /{id}          - Delete employee (Admin)
```

### Request/Response Format

```
Request:
{
  "method": "POST",
  "url": "/api/users/login",
  "headers": {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  "body": {
    "username": "john_doe",
    "password": "password123"
  }
}

Response:
{
  "statusCode": 200,
  "message": "Login successful",
  "data": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com",
    "role": "USER",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "tokenExpiresIn": 3600
  },
  "timestamp": "2024-01-07T10:30:00Z"
}
```

---

## Security Architecture

### Authentication Flow

```
User
  │ Username & Password
  ▼
┌─────────────────────────────────┐
│ Login Endpoint                  │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│ Validate Credentials            │
│ - Check username exists         │
│ - Verify password (BCrypt)      │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│ Generate JWT Token              │
│ - Secret Key                    │
│ - Expiration Time (1 hour)      │
│ - Claims (user id, role)        │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│ Return Token to Client          │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│ Store Token in Browser          │
│ localStorage.setItem('token')   │
└────────────────────────────────┘
```

### Request Authorization Flow

```
Protected Endpoint Request
  │ Include JWT Token in Header
  ▼
┌─────────────────────────────────┐
│ Security Filter                 │
│ Extract Token from Header       │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│ Validate Token                  │
│ - Verify Signature              │
│ - Check Expiration              │
│ - Extract Claims                │
└────────────┬────────────────────┘
             │
      ┌──────┴──────┐
      │             │
   Valid        Invalid
      │             │
      ▼             ▼
  Continue    Return 401
  Request    Unauthorized
```

### Role-Based Access Control (RBAC)

```
Request
  │
  ▼
┌─────────────────────────────────┐
│ Extract User Role from Token    │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│ Check Required Role             │
│ @RolesAllowed("ADMIN")          │
└────────────┬────────────────────┘
             │
      ┌──────┴──────┐
      │             │
   Allowed      Denied
      │             │
      ▼             ▼
  Process       Return 403
  Request       Forbidden
```

### Security Measures

1. **Password Security**
   - BCrypt hashing algorithm
   - Salt rounds: 10
   - Never store plain text passwords

2. **JWT Token Security**
   - HS256 signature algorithm
   - Token expiration: 1 hour
   - Refresh token support
   - Claims: userId, username, role

3. **Input Validation**
   - Server-side validation (never trust client)
   - Regex validation for emails, phones
   - Length validation
   - SQL injection prevention (JPA parameterized queries)

4. **CORS Protection**
   - Allowed origins configured
   - Allowed methods: GET, POST, PUT, DELETE
   - Credentials support

5. **Data Protection**
   - HTTPS in production
   - Sensitive data logging disabled
   - Secure session management
   - CSRF protection

---

## Deployment Architecture

### Production Deployment

```
┌────────────────┐
│   CDN Layer    │
│ (Static Files) │
└────────┬───────┘
         │
         ▼
┌──────────────────────────────────────┐
│    Load Balancer / Reverse Proxy     │
│    (Nginx / Apache)                  │
│    - SSL/TLS Termination             │
│    - Request Routing                 │
│    - Compression                     │
└────────┬───────────────────────────┬─┘
         │                           │
         ▼                           ▼
┌──────────────────────┐  ┌──────────────────────┐
│  Frontend Container  │  │  Backend Container   │
│  (React App)         │  │  (Spring Boot App)   │
│  Port: 3000          │  │  Port: 8080          │
│  - Static Assets     │  │  - API Endpoints     │
│  - SPA Routing       │  │  - Business Logic    │
└──────┬───────────────┘  └──────────┬──────────┘
       │                             │
       └──────────────┬──────────────┘
                      │
                      ▼
         ┌────────────────────────┐
         │   API Gateway Layer    │
         └────────────┬───────────┘
                      │
                      ▼
         ┌────────────────────────┐
         │   MySQL Database       │
         │   - Primary Database   │
         │   - Backup Replication │
         └────────────────────────┘

         ┌────────────────────────┐
         │  Monitoring & Logging  │
         │  - Application Logs    │
         │  - Error Tracking      │
         │  - Performance Metrics │
         └────────────────────────┘

         ┌────────────────────────┐
         │  Backup & Recovery     │
         │  - Daily Backups       │
         │  - Point-in-time       │
         │  - Disaster Recovery   │
         └────────────────────────┘
```

---

## Performance Optimization

### Frontend Optimization
- Code splitting and lazy loading
- Image optimization
- CSS/JS minification and bundling
- Caching strategies
- CDN for static assets

### Backend Optimization
- Database indexing
- Query optimization
- Connection pooling
- Caching (Redis)
- Response compression

---

## Scaling Strategy

### Horizontal Scaling
- Multiple backend instances
- Load balancing
- Session replication
- Distributed caching

### Vertical Scaling
- Increase server resources
- Optimize application code
- Database optimization
- Cache optimization

---

**Last Updated:** January 2026

For more information, refer to the main [README.md](README.md) file.
