# 🍕 Food-Ordering-Delivery-Web-Application

> A full-stack web application for ordering food online with real-time order tracking and management.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [User Roles & Capabilities](#user-roles--capabilities)
- [Installation & Setup](#installation--setup)
- [Running the Application](#running-the-application)
- [Database Configuration](#database-configuration)
- [API Documentation](#api-documentation)
- [Project Architecture](#project-architecture)
- [Contributing](#contributing)
- [License](#license)
- [Developer Info](#developer-info)

---

## 🎯 Overview

**Food-Ordering-Delivery-Web-Application** is a comprehensive full-stack solution for online food ordering and delivery management. Built during bachelor's studies and continuously improved, this application enables users to browse restaurant menus, place orders, and track delivery status in real-time.

The system supports three distinct user roles (Admin, Employee, User) with role-based access control and implements modern security practices with JWT authentication.

---

## ✨ Features

### 🌐 General Features
- **Responsive Design**: Fully responsive UI for desktop, tablet, and mobile devices
- **JWT Authentication**: Secure token-based authentication system
- **Role-Based Access Control**: Three-tier permission system (Admin, Employee, User)
- **Real-time Order Tracking**: Track order status from placement to delivery
- **Image Upload**: Support for meal and meal type images
- **Discount System**: Registered users receive 10% discount on orders
- **User-Friendly Interface**: Intuitive navigation and smooth user experience

### 👤 Guest/Unregistered Users
- Browse restaurant menu by meal categories
- View complete meal offerings with details and prices
- Add items to shopping cart with custom quantities
- Place orders with delivery address and phone number
- Receive tracking link via email
- Track order status without login

### 👨‍💼 Registered Users (USER Role)
- User registration and account management
- Update personal information and delivery addresses
- Place orders without re-entering address/phone (saved in profile)
- Automatic 10% discount on all orders
- View active orders (ORDERED, IN PREPARATION status)
- View order history (IN DELIVERY status)
- Order management and reorder functionality

### 👔 Employee Users (EMPLOYEE Role)
- Dashboard for incoming orders
- Update order status (ORDERED → IN PREPARATION → IN DELIVERY)
- View complete order history
- Order filtering and search capabilities
- Real-time order notifications

### 🔐 Admin Users (ADMIN Role)
- Complete meal type management (Create, Read, Update, Delete)
- Complete meal management with image uploads
- User management (view, logically delete, restore)
- Employee management (Create, update, delete staff)
- Order management and deletion
- View analytics and order history
- System configuration and maintenance

---

## 🛠 Tech Stack

### Frontend
- **React 18** - UI library with React Hooks
- **Redux & Redux-Persist** - State management
- **React Router v6** - Client-side routing
- **Axios** - HTTP client for API calls
- **Bootstrap 5** - UI framework
- **React-Bootstrap** - Bootstrap components for React
- **Styled Components** - CSS-in-JS styling
- **SweetAlert2** - Beautiful alerts and modals
- **JWT-Decode** - JWT token decoding
- **Moment.js** - Date/time manipulation
- **React Icons** - Icon library

### Backend
- **Java 17** - Programming language
- **Spring Boot 2.7.0** - Framework
- **Spring Data JPA** - Database ORM
- **Spring Security** - Authentication & Authorization
- **MySQL** - Database
- **Hibernate** - ORM framework
- **JWT (jjwt)** - Token generation
- **Lombok** - Boilerplate reduction
- **Maven** - Build tool
- **JSON** - Data format

---

## 📁 Project Structure

```
Food-Ordering-Delivery-Web-Application/
│
├── food-ordering-app/
│   │
│   ├── food-order-back/                    # Backend (Spring Boot)
│   │   ├── src/
│   │   │   ├── main/
│   │   │   │   ├── java/com/example/foodorderback/
│   │   │   │   │   ├── controller/        # REST API endpoints
│   │   │   │   │   │   ├── FinalOrderController.java
│   │   │   │   │   │   ├── LoginController.java
│   │   │   │   │   │   ├── MealController.java
│   │   │   │   │   │   ├── MealTypeController.java
│   │   │   │   │   │   └── UserController.java
│   │   │   │   │   ├── service/           # Business logic interfaces
│   │   │   │   │   │   ├── LoginService.java
│   │   │   │   │   │   ├── MealService.java
│   │   │   │   │   │   ├── MealTypeService.java
│   │   │   │   │   │   └── UserService.java
│   │   │   │   │   ├── serviceImpl/        # Service implementations
│   │   │   │   │   ├── model/             # Entity classes
│   │   │   │   │   │   ├── User.java
│   │   │   │   │   │   ├── Meal.java
│   │   │   │   │   │   ├── MealType.java
│   │   │   │   │   │   ├── FinalOrder.java
│   │   │   │   │   │   ├── OrderItem.java
│   │   │   │   │   │   ├── Role.java
│   │   │   │   │   │   ├── Status.java
│   │   │   │   │   │   └── Login.java
│   │   │   │   │   ├── repository/        # Data access layer
│   │   │   │   │   ├── dto/               # Data Transfer Objects
│   │   │   │   │   ├── security/          # JWT & Security config
│   │   │   │   │   └── FoodOrderBackApplication.java
│   │   │   │   └── resources/
│   │   │   │       ├── application.properties
│   │   │   │       └── import.sql
│   │   │   └── test/java/com/           # Unit tests
│   │   │
│   │   ├── pom.xml                       # Maven configuration
│   │   ├── mvnw                          # Maven wrapper (Unix)
│   │   └── mvnw.cmd                      # Maven wrapper (Windows)
│   │
│   └── food-ordering-front/               # Frontend (React)
│       ├── public/
│       │   ├── index.html
│       │   ├── manifest.json
│       │   └── robots.txt
│       ├── src/
│       │   ├── components/               # React components
│       │   │   ├── active-final-orders/
│       │   │   ├── cart/
│       │   │   ├── employee/
│       │   │   ├── final-order-by-id/
│       │   │   ├── footer/
│       │   │   ├── interceptor/         # HTTP interceptors
│       │   │   ├── login/
│       │   │   ├── meal/
│       │   │   ├── meal-type/
│       │   │   ├── meals-by-meal-type/
│       │   │   ├── menu/
│       │   │   ├── my-active-final-orders/
│       │   │   ├── my-delivered-final-orders/
│       │   │   ├── my-profile/
│       │   │   ├── navbar/
│       │   │   ├── order-history/
│       │   │   ├── registration/
│       │   │   └── user/
│       │   ├── services/                 # API services
│       │   │   ├── LoginService.js
│       │   │   ├── MealService.js
│       │   │   ├── MealTypeService.js
│       │   │   ├── TokenService.js
│       │   │   └── UserService.js
│       │   ├── store-redux/             # Redux store configuration
│       │   │   ├── store.js
│       │   │   └── cart/
│       │   ├── images/                   # Application images
│       │   ├── App.js                    # Main app component
│       │   ├── App.css
│       │   ├── index.js                  # Entry point
│       │   └── index.css
│       ├── package.json
│       ├── package-lock.json
│       └── README.md
│
└── README.md                             # This file

```

---

## 👥 User Roles & Capabilities

### 1. **GUEST** (Unregistered Users)
Unregistered visitors can:
- ✅ Browse restaurant menu by category
- ✅ View meal details and prices
- ✅ Add items to cart with quantities
- ✅ Place orders with delivery address & phone
- ✅ Receive order tracking link via email
- ✅ Track order status in real-time
- ❌ Cannot save orders to history
- ❌ No discount benefits

### 2. **USER** (Registered Customers)
Registered users with USER role can:
- ✅ All guest capabilities
- ✅ Create account and update profile
- ✅ Auto-fill address and phone from saved profile
- ✅ Enjoy **10% discount** on every order
- ✅ View active orders (ORDERED, IN PREPARATION)
- ✅ View order history (IN DELIVERY status)
- ✅ Manage multiple delivery addresses
- ✅ Reorder from previous orders

### 3. **EMPLOYEE** (Order Fulfillment Staff)
Employee users can:
- ✅ View all incoming orders dashboard
- ✅ Update order status: ORDERED → IN PREPARATION
- ✅ Update order status: IN PREPARATION → IN DELIVERY
- ✅ View complete order history
- ✅ Filter and search orders
- ✅ Monitor order preparation time
- ✅ Print order details

### 4. **ADMIN** (System Administrator)
Admin users have full system control:

**Meal Management:**
- ✅ Create new meals with images
- ✅ Update existing meals
- ✅ Logically delete meals
- ✅ View meal inventory

**Meal Type Management:**
- ✅ Create meal categories (Pizza, Burger, etc.)
- ✅ Upload category images
- ✅ Update category details
- ✅ Delete meal types

**User Management:**
- ✅ View all users
- ✅ Logically delete users
- ✅ Restore deleted users
- ✅ View user order history
- ✅ Manage user discounts

**Employee Management:**
- ✅ Create employee accounts
- ✅ Update employee details
- ✅ Deactivate employees
- ✅ Assign roles and permissions

**Order Management:**
- ✅ View all orders (active & history)
- ✅ Filter orders by status/date
- ✅ Delete orders and order items
- ✅ View order analytics

---

## 📦 Installation & Setup

### Prerequisites
- **Node.js** (v14 or higher) - [Download](https://nodejs.org/)
- **Java 17** - [Download](https://www.oracle.com/java/technologies/downloads/)
- **Maven 3.6+** - [Download](https://maven.apache.org/download.cgi)
- **MySQL 8.0+** - [Download](https://www.mysql.com/downloads/)
- **Git** - [Download](https://git-scm.com/)

### Step 1: Clone Repository
```bash
git clone https://github.com/nidhikumari30/Food-Ordering-Delivery-Web-Application.git
cd Food-Ordering-Delivery-Web-Application
```

### Step 2: Setup Backend

#### Configure MySQL Database
1. Create a new MySQL database:
```sql
CREATE DATABASE food_ordering_db;
USE food_ordering_db;
```

2. Update database credentials in `food-order-back/src/main/resources/application.properties`:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/food_ordering_db
spring.datasource.username=root
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

#### Build Backend
```bash
cd food-ordering-app/food-order-back
mvn clean install
mvn spring-boot:run
```

The backend API will run on: `http://localhost:8080`

### Step 3: Setup Frontend

```bash
cd ../food-ordering-front
npm install
npm start
```

The frontend will run on: `http://localhost:3000`

---

## 🚀 Running the Application

### Development Mode

**Terminal 1 - Backend:**
```bash
cd food-ordering-app/food-order-back
mvn spring-boot:run
```

**Terminal 2 - Frontend:**
```bash
cd food-ordering-app/food-ordering-front
npm start
```

### Production Build

**Frontend Build:**
```bash
cd food-ordering-app/food-ordering-front
npm run build
```

**Backend Build:**
```bash
cd food-ordering-app/food-order-back
mvn clean package
```

---

## 🗄️ Database Configuration

### Initial Setup
The application includes `import.sql` that pre-populates the database with:
- Meal types (categories)
- Sample meals
- Default admin user

### Database Schema
Key entities in the system:
- **User** - Customer and employee accounts
- **Meal** - Individual menu items
- **MealType** - Meal categories
- **FinalOrder** - Customer orders
- **OrderItem** - Items within an order
- **Role** - User role definitions (ADMIN, EMPLOYEE, USER)
- **Status** - Order status (ORDERED, IN_PREPARATION, IN_DELIVERY, DELIVERED)

### Connection Properties
Located in: `food-order-back/src/main/resources/application.properties`
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/food_ordering_db
spring.datasource.username=root
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=false
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
```

---

## 🔌 API Documentation

### Authentication Endpoints
```
POST   /api/login              - User login
POST   /api/register           - User registration
POST   /api/logout             - User logout
```

### Meal Management
```
GET    /api/meals              - Get all meals
GET    /api/meals/{id}         - Get meal by ID
POST   /api/meals              - Create meal (Admin)
PUT    /api/meals/{id}         - Update meal (Admin)
DELETE /api/meals/{id}         - Delete meal (Admin)
```

### Meal Type Management
```
GET    /api/meal-types         - Get all categories
GET    /api/meal-types/{id}    - Get category by ID
POST   /api/meal-types         - Create category (Admin)
PUT    /api/meal-types/{id}    - Update category (Admin)
DELETE /api/meal-types/{id}    - Delete category (Admin)
```

### Order Management
```
GET    /api/orders             - Get user orders
GET    /api/orders/{id}        - Get order by ID
POST   /api/orders             - Create new order
PUT    /api/orders/{id}        - Update order status (Employee/Admin)
DELETE /api/orders/{id}        - Delete order (Admin)
GET    /api/orders/history     - View order history (User)
```

### User Management
```
GET    /api/users              - Get all users (Admin)
GET    /api/users/{id}         - Get user by ID
PUT    /api/users/{id}         - Update user profile
DELETE /api/users/{id}         - Logically delete user (Admin)
```

### Employee Management
```
GET    /api/employees          - Get all employees (Admin)
POST   /api/employees          - Create employee (Admin)
PUT    /api/employees/{id}     - Update employee (Admin)
DELETE /api/employees/{id}     - Remove employee (Admin)
```

---

## 🏗️ Project Architecture

### Frontend Architecture (React)

**Component Structure:**
- **Presentational Components** - Reusable UI components
- **Container Components** - Smart components with business logic
- **Service Layer** - API communication (Axios)
- **Redux Store** - Global state management
- **Router** - Client-side navigation with React Router v6

**State Management:**
- Redux for global state (cart, authentication, user data)
- Redux-Persist for local storage persistence
- Component state for local UI state

**HTTP Interceptor:**
- Automatic JWT token injection in request headers
- Token refresh and error handling
- Request/response logging

### Backend Architecture (Spring Boot)

**Layered Architecture:**
```
Controllers
    ↓
Services (Interfaces)
    ↓
Service Implementations
    ↓
Repositories (Data Access)
    ↓
Database
```

**Key Patterns:**
- **MVC Pattern** - Model-View-Controller separation
- **DAO Pattern** - Data Access Objects
- **DTO Pattern** - Data Transfer Objects for API
- **Service Layer** - Business logic encapsulation
- **Repository Pattern** - Database abstraction

**Security:**
- JWT token-based authentication
- Spring Security filters
- Role-based access control (RBAC)
- Password encoding with BCrypt
- CORS configuration

---

## 🛡️ Security Features

- ✅ **JWT Authentication** - Stateless token-based auth
- ✅ **Password Encryption** - BCrypt hashing
- ✅ **Role-Based Access Control** - Fine-grained permissions
- ✅ **CORS Configuration** - Cross-origin request handling
- ✅ **Input Validation** - Backend validation on all inputs
- ✅ **Secure Headers** - Security headers in responses
- ✅ **Token Refresh** - Automatic token renewal
- ✅ **Logout Functionality** - Token invalidation

---

## 📝 Development Guidelines

### Code Structure Best Practices
1. **Separation of Concerns** - Each class has a single responsibility
2. **DRY Principle** - Don't Repeat Yourself
3. **SOLID Principles** - Clean and maintainable code
4. **Naming Conventions** - Clear, descriptive names
5. **Documentation** - Comments for complex logic
6. **Error Handling** - Try-catch blocks and proper error messages
7. **Logging** - Debug and error logging

### Git Workflow
```bash
# Create feature branch
git checkout -b feature/feature-name

# Make changes and commit
git add .
git commit -m "Descriptive commit message"

# Push to remote
git push origin feature/feature-name

# Create Pull Request on GitHub
```

---

## 🐛 Troubleshooting

### Common Issues

**Backend won't connect to MySQL:**
- Verify MySQL service is running
- Check database URL and credentials in `application.properties`
- Ensure database exists: `CREATE DATABASE food_ordering_db;`

**Frontend can't connect to backend:**
- Verify backend is running on `http://localhost:8080`
- Check CORS settings in backend configuration
- Clear browser cache and localStorage

**Port already in use:**
- Change Spring Boot port: Add `server.port=8081` to `application.properties`
- Change React port: Set `PORT=3001` environment variable before `npm start`

**Database migration issues:**
- Check `import.sql` file in resources folder
- Verify Hibernate DDL settings in `application.properties`

---

## 📚 Additional Resources

- [React Documentation](https://react.dev/)
- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [Redux Documentation](https://redux.js.org/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [JWT Introduction](https://jwt.io/introduction)
- [REST API Best Practices](https://restfulapi.net/)

---

## 📄 License

This project is open source and available under the MIT License.

---

## 👨‍💻 Developer Info

**Project:** Food-Ordering-Delivery-Web-Application

**Developed by:** Nidhi Kumari

**Contact & Social:**

📧 **Email:** [nidhikumari934181@gmail.com](mailto:nidhikumari934181@gmail.com)

💼 **LinkedIn:** [linkedin.com/in/nidhi-kumari-4648692b2](https://linkedin.com/in/nidhi-kumari-4648692b2)

💻 **GitHub:** [github.com/nidhikumari30](https://github.com/nidhikumari30)

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 🙏 Acknowledgments

- Thanks to the Spring Boot and React communities
- Special thanks to all contributors
- Gratitude to users providing feedback and suggestions

---

**Last Updated:** January 2026

⭐ If you find this project helpful, please consider giving it a star! ⭐

After choosing category (meal type), available meals (offers) will be listed.

![4](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/cbb4d2dc-efcd-4bbd-870a-91b98ef6167b)

![5](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/605b88ed-3bae-45e5-9073-3aba13ec63ee)
![6](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/c2d284cf-2ba6-4d75-ac5f-c9a206ee0b7c)

Users can add items (meals) to the cart after they specify quantity. Default and minimum value for quantity is 1 and users can't go below that value. 
After clicking on *Confirm* button, item is successfully added to the cart.

![7](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/6fc5fd43-ad76-4041-9f6b-16a9ee7b058a)
![8](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/947abcfe-86f2-41e3-9479-1bc9b043f9e7)

![9](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/f3e7ada8-e794-468c-9b85-f29edb5d9778)
![10](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/3707e695-44ee-434c-b5df-5fb9e3c06791)

Clicking on the cart button or icon in the navigation, users can see items from the cart.

![11](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/e24b2caf-209a-4574-9bad-bb80c5fc9bc5)

![12](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/deb62c95-2bc2-4df5-9c69-156232fdbe9f)
![13](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/d5c3b2af-260e-4821-b864-f7e96a4325da)

Users that are not logged-in, need to insert details such as address and phone number.

![14](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/73eb8ed0-5dae-4931-9f1e-2df35dba8680)

Without inserting details, not logged-in users can't confirm the final order 

![15](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/c8059b1b-f5bb-4ff6-8add-9d55bc821304)

Validation if inserted phone number is a number or it has less than 5 digits

![16](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/ae42d4f4-e96b-4c32-ac98-8bb6d83638fe)

![17](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/51bac0a0-9985-402c-bab8-874b9c511a15)

After valid input, final order will be confirmed and not logged-in users can track their order status clicking on the link.

![18](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/527d6246-6903-4c15-a322-606aeeecee9b)

![19](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/970363e4-eaa5-433e-94c2-312b287e7c3a)

![20](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/bf234304-f9db-4a28-a955-db52a6af64c6)

Clicking on *Show items* button, user can see all items from the (final) order that he ordered.

![21](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/fd532af9-7204-4696-91d4-bbe10db6700f)
![22](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/94171e40-5d5f-431d-a0d6-e8b1aed71897)

![23](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/ae737b0a-c365-43d3-925e-58e44aef56e7)
![24](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/cc1f19a9-9f63-4623-a4a0-feeb709f7948)

Logged-in users get 10% discount on the final price of their order. Also they don't need to insert details, such as address and phone number, because it's stored in the database after registration. Logged-in users also have more tabs and options.

![25](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/b5f8cb96-1e13-4687-a115-e2881c3b7501)

![26](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/d727a736-33c9-4f1c-80a8-80f478f742a0)
![27](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/968a80a1-16da-42be-ad36-bc2271993cc4)

Logged-in users can track their active orders (*IN PREPARATION* and *ORDERED* status) clicking on *My active orders tab*. Final orders with *IN DELIVERY* status will be visible clicking on *My order history* tab.

Clicking on *Show items* button, user can see his ordered items

![28](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/75066e84-1303-438a-8035-1c8c84ee7c10)

![29](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/2fbfacc1-b8e8-40b1-869b-d6848f0ce8b3)

![30](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/01e06d25-ad76-48eb-9b7d-910a90b5ed55)
![31](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/95388b1b-b65d-47f7-8fbf-605c59542898)

Admin have option to delete final order and all its ordered items from the database, but he doesn't have an option to change status as employee can do (same component shows for both roles, but they don't have same available actions).

![exc-admin-delete](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/09b9db37-eddc-4921-9841-05ff9cb6ae2a)
![exc-admin-delete-2](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/6b2599bb-689d-412b-918f-3a773325242d)

Employee can see and change status of the final order depending on real status of the order, which user can track (but they can't delete them as Admin can do).

![32](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/b22727a1-598a-43e9-8b2c-a6637b45f3a8)

Clicking on *Show items* button, employee can see all items from the (final) order.

![33](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/58fdc043-a19a-4f72-94ae-fc493a9c4416)

All orders with status *IN DELIVERY* are placed in order history, they aren't considered active anymore

![34](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/3b0dcca3-8371-4ec5-b537-3bffc42ec52e)

Login component shows when the app starts.

![35](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/b3d0bf70-23cd-464f-b277-569a95550971)

![36](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/ad44cd0f-dc62-4c45-8bd2-4949930de848)
![37](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/d31f8600-59a3-4980-99d2-3b9cac4b6a5f)

Logged-in users can access their profile page where they edit profile or change password if necessary.

![38](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/c6a1e444-e785-44a6-93f0-ade0ab594084)

Edit profile

![39](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/73e35977-3052-4c5c-b342-49750021eeed)

![40](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/67f96241-9455-44e0-9317-1cd0c07630b0)
![41](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/2ff5e2c8-74ad-4e43-81b4-09c45e34ab5c)

When user wants to change password, he needs to insert old password as well.

![42](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/9289d332-6d87-4965-9fe8-68c7f941528b)

If inserted old password and password from the database don't match, he won't be allowed to save new password.

![43](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/79e784eb-c404-4160-9dab-cb7464c78487)

If they match, new password will be saved successfully (will be encripted and saved in the database)

![44](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/d7541c6c-40a8-4d2c-bba8-e7fb9db4cc09)

Registration (unregistered users can sign up and they will have 10% off on every order)

![45](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/95c8ed46-8986-4635-b9f2-079b3e67e0de)

Validation and alert if username already exists in the database.

![46](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/1c33944a-f51c-44dc-8f73-2935c6e4cc65)

Validation and alert if email already exists in the database

![47](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/84a6ec13-2b36-4dab-b203-26a39ecff789)

Registration design for mobile screen size

![48](https://github.com/bujakkristijan/food-ordering-app/assets/76042091/9f52480d-5d50-4b00-a388-a36117da8088)
