# 📝 Folder Structure Guidelines

This document explains the current folder structure and best practices for organizing code.

## Frontend Folder Structure

```
food-ordering-app/food-ordering-front/
│
├── public/                          # Static files served by React
│   ├── index.html                   # Main HTML file
│   ├── manifest.json                # PWA manifest
│   └── robots.txt                   # SEO robots file
│
├── src/
│   ├── components/                  # Reusable React components
│   │   ├── [feature-name]/          # Feature-based component folders
│   │   │   ├── [Component].js       # Main component
│   │   │   ├── [Component].css      # Component styles
│   │   │   └── index.js             # Barrel export
│   │   │
│   │   ├── active-final-orders/     # Admin: View active orders
│   │   ├── cart/                    # Shopping cart management
│   │   ├── employee/                # Employee management (Admin)
│   │   ├── final-order-by-id/       # Order tracking
│   │   ├── footer/                  # Footer component
│   │   ├── interceptor/             # HTTP interceptors
│   │   ├── login/                   # User login
│   │   ├── meal/                    # Meal management (Admin)
│   │   ├── meal-type/               # Meal type management (Admin)
│   │   ├── meals-by-meal-type/      # Browse meals by category
│   │   ├── menu/                    # Main menu
│   │   ├── my-active-final-orders/  # User: Active orders
│   │   ├── my-delivered-final-orders/# User: Delivered orders
│   │   ├── my-profile/              # User profile management
│   │   ├── navbar/                  # Navigation bar
│   │   ├── order-history/           # Order history
│   │   ├── registration/            # User registration
│   │   └── user/                    # User management (Admin)
│   │
│   ├── services/                    # API communication services
│   │   ├── LoginService.js          # Authentication API
│   │   ├── MealService.js           # Meal API calls
│   │   ├── MealTypeService.js       # Meal type API calls
│   │   ├── TokenService.js          # Token management
│   │   ├── UserService.js           # User API calls
│   │   └── axiosConfig.js           # Axios configuration
│   │
│   ├── store-redux/                 # Redux store configuration
│   │   ├── store.js                 # Redux store setup
│   │   ├── cart/                    # Cart reducer and actions
│   │   │   ├── cartSlice.js         # Cart Redux slice
│   │   │   └── actions.js           # Cart actions
│   │   └── middleware/              # Custom middleware
│   │
│   ├── images/                      # Application images and assets
│   │   ├── logo.png
│   │   ├── icons/
│   │   └── backgrounds/
│   │
│   ├── utils/                       # Utility functions (optional)
│   │   ├── constants.js             # Constants
│   │   ├── helpers.js               # Helper functions
│   │   └── validators.js            # Validation functions
│   │
│   ├── App.js                       # Main app component with routing
│   ├── App.css                      # Global app styles
│   ├── index.js                     # React entry point
│   ├── index.css                    # Global styles
│   └── reportWebVitals.js           # Performance monitoring
│
├── package.json                     # NPM dependencies
├── package-lock.json                # Dependency lock file
├── .env                             # Environment variables
├── .gitignore                       # Git ignore rules
└── README.md                        # Frontend documentation
```

## Backend Folder Structure

```
food-ordering-app/food-order-back/
│
├── src/
│   ├── main/
│   │   ├── java/com/example/foodorderback/
│   │   │   │
│   │   │   ├── controller/          # REST API Controllers
│   │   │   │   ├── FinalOrderController.java     # Order endpoints
│   │   │   │   ├── LoginController.java          # Auth endpoints
│   │   │   │   ├── MealController.java           # Meal endpoints
│   │   │   │   ├── MealTypeController.java       # Category endpoints
│   │   │   │   └── UserController.java           # User endpoints
│   │   │   │
│   │   │   ├── service/             # Service Interfaces
│   │   │   │   ├── FinalOrderService.java
│   │   │   │   ├── LoginService.java
│   │   │   │   ├── MealService.java
│   │   │   │   ├── MealTypeService.java
│   │   │   │   └── UserService.java
│   │   │   │
│   │   │   ├── serviceImpl/          # Service Implementations
│   │   │   │   ├── FinalOrderServiceImpl.java
│   │   │   │   ├── LoginServiceImpl.java
│   │   │   │   ├── MealServiceImpl.java
│   │   │   │   ├── MealTypeServiceImpl.java
│   │   │   │   └── UserServiceImpl.java
│   │   │   │
│   │   │   ├── model/               # Entity Classes (JPA)
│   │   │   │   ├── User.java                 # User entity
│   │   │   │   ├── Meal.java                 # Meal entity
│   │   │   │   ├── MealType.java             # Category entity
│   │   │   │   ├── FinalOrder.java           # Order entity
│   │   │   │   ├── OrderItem.java            # Order item entity
│   │   │   │   ├── Role.java                 # Role entity
│   │   │   │   ├── Status.java               # Status entity
│   │   │   │   └── Login.java                # Login entity
│   │   │   │
│   │   │   ├── repository/          # Data Access Layer
│   │   │   │   ├── FinalOrderRepository.java
│   │   │   │   ├── LoginRepository.java
│   │   │   │   ├── MealRepository.java
│   │   │   │   ├── MealTypeRepository.java
│   │   │   │   ├── UserRepository.java
│   │   │   │   ├── RoleRepository.java
│   │   │   │   ├── StatusRepository.java
│   │   │   │   └── OrderItemRepository.java
│   │   │   │
│   │   │   ├── dto/                 # Data Transfer Objects
│   │   │   │   ├── UserDTO.java
│   │   │   │   ├── MealDTO.java
│   │   │   │   ├── FinalOrderDTO.java
│   │   │   │   ├── OrderItemDTO.java
│   │   │   │   └── LoginDTO.java
│   │   │   │
│   │   │   ├── security/            # Security & JWT Configuration
│   │   │   │   ├── JwtTokenProvider.java      # Token generation
│   │   │   │   ├── JwtAuthenticationFilter.java # Request filter
│   │   │   │   ├── SecurityConfig.java        # Security configuration
│   │   │   │   └── CorsConfig.java            # CORS configuration
│   │   │   │
│   │   │   ├── exception/           # Custom Exceptions
│   │   │   │   ├── ResourceNotFoundException.java
│   │   │   │   ├── UnauthorizedException.java
│   │   │   │   ├── BadRequestException.java
│   │   │   │   └── GlobalExceptionHandler.java
│   │   │   │
│   │   │   ├── util/                # Utility Classes
│   │   │   │   ├── ImageProcessor.java
│   │   │   │   ├── ValidationUtil.java
│   │   │   │   └── Constants.java
│   │   │   │
│   │   │   └── FoodOrderBackApplication.java   # Main Application class
│   │   │
│   │   └── resources/
│   │       ├── application.properties          # Application config
│   │       ├── application-dev.properties      # Development config
│   │       ├── application-prod.properties     # Production config
│   │       ├── import.sql                      # Database initialization
│   │       ├── logback.xml                     # Logging configuration
│   │       └── static/                         # Static resources
│   │
│   └── test/
│       └── java/com/example/foodorderback/
│           ├── controller/          # Controller tests
│           ├── service/             # Service tests
│           ├── repository/          # Repository tests
│           └── integration/         # Integration tests
│
├── target/                          # Build output (auto-generated)
├── pom.xml                          # Maven configuration
├── mvnw                             # Maven wrapper (Unix)
├── mvnw.cmd                         # Maven wrapper (Windows)
├── .gitignore                       # Git ignore rules
└── README.md                        # Backend documentation
```

## File Naming Conventions

### Frontend (JavaScript/React)

| Type | Format | Example |
|------|--------|---------|
| Component | PascalCase | `UserProfileComponent.js` |
| Service | camelCase | `userService.js` |
| Hook | camelCase (use prefix) | `useAuthentication.js` |
| Utility | camelCase | `validators.js` |
| Constants | UPPER_SNAKE_CASE | `API_CONSTANTS.js` |
| Styles | [Component].css | `UserProfile.css` |

### Backend (Java)

| Type | Format | Example |
|------|--------|---------|
| Class | PascalCase | `UserService.java` |
| Interface | PascalCase | `IUserRepository.java` |
| Package | lowercase | `com.example.service` |
| Constant | UPPER_SNAKE_CASE | `DEFAULT_PAGE_SIZE` |
| Method | camelCase | `getUserById()` |
| Variable | camelCase | `userName` |

## Component Structure Best Practices

### Folder per Component (Frontend)

```
components/
└── user-profile/
    ├── UserProfileComponent.js      # Main component
    ├── UserProfileComponent.css     # Component styles
    ├── subcomponents/               # Child components
    │   └── ProfileForm.js
    └── index.js                     # Barrel export
```

### Barrel Export (index.js)
```javascript
export { default as UserProfileComponent } from './UserProfileComponent';
```

### Component Template
```javascript
import React, { useState, useEffect } from 'react';
import './UserProfileComponent.css';

const UserProfileComponent = ({ userId }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Component logic
  }, [userId]);

  return (
    <div className="user-profile">
      {/* JSX */}
    </div>
  );
};

export default UserProfileComponent;
```

## Backend Service Structure

### Service Interface
```java
public interface UserService {
    UserDTO getUserById(Long id);
    List<UserDTO> getAllUsers();
    UserDTO createUser(UserDTO userDTO);
    UserDTO updateUser(Long id, UserDTO userDTO);
    void deleteUser(Long id);
}
```

### Service Implementation
```java
@Service
@Transactional
public class UserServiceImpl implements UserService {
    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDTO getUserById(Long id) {
        User user = userRepository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("User not found"));
        return convertToDTO(user);
    }

    // Other methods...

    private UserDTO convertToDTO(User user) {
        // DTO conversion logic
    }
}
```

## Directory Structure Maintenance

### Adding New Features

1. **Create feature folder** in components/
2. **Create component file** with consistent naming
3. **Create CSS file** for styles
4. **Create index.js** for exports
5. **Create service** if API calls needed
6. **Update routing** in App.js

### Deleting Features

1. **Remove component folder**
2. **Remove from routing** in App.js
3. **Remove service** if applicable
4. **Remove Redux slices** if applicable
5. **Update documentation**

## Import Organization

### Recommended Order
```javascript
// 1. React imports
import React, { useState } from 'react';
import { useNavigate } from 'react-router-dom';

// 2. Third-party libraries
import axios from 'axios';
import { useDispatch } from 'react-redux';

// 3. Local components
import NavbarComponent from '../navbar/NavbarComponent';

// 4. Services
import UserService from '../../services/UserService';

// 5. Styles
import './UserProfileComponent.css';
```

## Documentation Files

```
root/
├── README.md                    # Main project documentation
├── SETUP_GUIDE.md               # Installation & setup instructions
├── ARCHITECTURE.md              # Architecture documentation
├── CONTRIBUTING.md              # Contributing guidelines
├── FOLDER_STRUCTURE.md          # This file
├── API_DOCUMENTATION.md         # API reference
├── TROUBLESHOOTING.md           # Troubleshooting guide
└── CHANGELOG.md                 # Version history
```

---

**Last Updated:** January 2026

For more information, refer to [README.md](README.md).
