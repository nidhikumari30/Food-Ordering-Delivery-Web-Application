# 🚀 Complete Setup Guide

This guide provides step-by-step instructions to get the Food-Ordering-Delivery-Web-Application running on your local machine.

## 📋 Prerequisites

Before starting, ensure you have the following installed:

### Required Software

1. **Node.js and npm**
   - Download: https://nodejs.org/
   - Verify installation: `node --version` and `npm --version`
   - Minimum version: Node.js v14.0.0

2. **Java Development Kit (JDK) 17**
   - Download: https://www.oracle.com/java/technologies/downloads/
   - Set JAVA_HOME environment variable
   - Verify installation: `java -version`

3. **Maven 3.6+**
   - Download: https://maven.apache.org/download.cgi
   - Set MAVEN_HOME environment variable
   - Verify installation: `mvn --version`

4. **MySQL Server 8.0+**
   - Download: https://www.mysql.com/downloads/
   - Start MySQL service
   - Verify installation: `mysql --version`

5. **Git**
   - Download: https://git-scm.com/
   - Verify installation: `git --version`

## 🔧 Step-by-Step Setup

### Step 1: Clone the Repository

```bash
# Open terminal/command prompt
cd your_desired_directory

# Clone the repository
git clone https://github.com/nidhikumari30/Food-Ordering-Delivery-Web-Application.git

# Navigate to project directory
cd Food-Ordering-Delivery-Web-Application
```

### Step 2: Database Setup

#### Create Database

1. **Open MySQL Command Line or MySQL Workbench**

2. **Create the database:**
   ```sql
   CREATE DATABASE food_ordering_db;
   USE food_ordering_db;
   ```

3. **Verify creation:**
   ```sql
   SHOW DATABASES;
   ```

#### Configure Connection

1. **Navigate to backend configuration:**
   ```
   food-ordering-app/food-order-back/src/main/resources/application.properties
   ```

2. **Update database credentials:**
   ```properties
   # MySQL Database Configuration
   spring.datasource.url=jdbc:mysql://localhost:3306/food_ordering_db
   spring.datasource.username=root
   spring.datasource.password=your_mysql_password
   spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
   
   # JPA/Hibernate Configuration
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=false
   spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
   ```

3. **If you changed the password**, update the password field above

### Step 3: Backend Setup

#### Navigate to Backend Directory
```bash
cd food-ordering-app/food-order-back
```

#### Build the Project
```bash
# Clean and build
mvn clean install

# This will:
# - Download dependencies
# - Compile Java code
# - Run tests
# - Create executable JAR
```

#### Run the Backend
```bash
mvn spring-boot:run
```

**Expected Output:**
```
Tomcat started on port(s): 8080 (http)
Started FoodOrderBackApplication in X.XXX seconds
```

**Backend URL:** http://localhost:8080

**API Endpoints Available:**
- http://localhost:8080/api/meals
- http://localhost:8080/api/meal-types
- http://localhost:8080/api/users
- etc.

### Step 4: Frontend Setup

#### Open New Terminal Window

#### Navigate to Frontend Directory
```bash
cd food-ordering-app/food-ordering-front
```

#### Install Dependencies
```bash
npm install

# This will:
# - Download all npm packages
# - Create node_modules folder
# - Setup React environment
```

#### Start the Development Server
```bash
npm start
```

**Expected Output:**
```
Compiled successfully!

You can now view food-ordering-front in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://your_ip:3000
```

**Frontend URL:** http://localhost:3000

## ✅ Verification

### Check if Everything is Running

1. **Backend Check:**
   - Open: http://localhost:8080/api/meals
   - Should return JSON data of meals
   - Or error if no data (that's OK for first setup)

2. **Frontend Check:**
   - Open: http://localhost:3000
   - Should see the application interface
   - Menu should be visible

3. **Database Check:**
   ```bash
   mysql -u root -p
   USE food_ordering_db;
   SHOW TABLES;
   ```

   You should see tables:
   - users
   - meals
   - meal_types
   - final_orders
   - order_items
   - roles
   - status

## 🔐 Initial Login Credentials

After setup, the database is populated with default data via `import.sql`:

### Admin Account
- **Username:** admin
- **Password:** admin123
- **Role:** ADMIN

### Employee Account
- **Username:** employee
- **Password:** employee123
- **Role:** EMPLOYEE

### Test User Account
- **Username:** testuser
- **Password:** user123
- **Role:** USER

**⚠️ IMPORTANT:** Change these credentials in production!

## 📁 Project Structure

```
Food-Ordering-Delivery-Web-Application/
├── food-ordering-app/
│   ├── food-order-back/          # Spring Boot Backend
│   │   ├── src/
│   │   ├── pom.xml              # Maven configuration
│   │   └── mvnw                 # Maven wrapper
│   │
│   └── food-ordering-front/      # React Frontend
│       ├── src/
│       ├── public/
│       ├── package.json          # npm dependencies
│       └── node_modules/
│
└── README.md                     # Main documentation
```

## 🛠️ Troubleshooting

### Issue: Port 8080 Already in Use

**Solution:**
```bash
# Change backend port in application.properties
server.port=8081

# Or kill the process using the port (Windows)
netstat -ano | findstr :8080
taskkill /PID <PID> /F

# Or kill the process (macOS/Linux)
lsof -ti:8080 | xargs kill -9
```

### Issue: Port 3000 Already in Use

**Solution:**
```bash
# Set different port before npm start
set PORT=3001  # Windows
export PORT=3001  # macOS/Linux

npm start
```

### Issue: Cannot Connect to MySQL

**Solution:**
1. Verify MySQL is running
   ```bash
   # Windows
   services.msc  # Check MySQL80
   
   # macOS
   brew services list
   
   # Linux
   sudo service mysql status
   ```

2. Check credentials in `application.properties`

3. Test connection:
   ```bash
   mysql -u root -p
   ```

### Issue: Database Tables Not Created

**Solution:**
```bash
# Manually run the import.sql file
mysql -u root -p food_ordering_db < src/main/resources/import.sql

# Or ensure spring.jpa.hibernate.ddl-auto=update in application.properties
```

### Issue: Dependencies Not Downloaded

**Solution:**
```bash
# Clear Maven cache
mvn clean

# Clear npm cache
npm cache clean --force

# Reinstall
mvn install
npm install
```

### Issue: CORS Error in Browser Console

**Solution:**
- Make sure backend is running on http://localhost:8080
- Check CORS configuration in backend
- Clear browser cache (Ctrl+Shift+Delete)

## 📊 Database Schema Overview

### Key Tables

**users**
- id, username, password, email, phone, address, isDeleted, roleId

**meals**
- id, name, description, price, image, isDeleted, mealTypeId

**meal_types**
- id, name, image, isDeleted

**final_orders**
- id, userId, totalPrice, address, phone, statusId, createdAt

**order_items**
- id, orderId, mealId, quantity, price

**roles**
- id, role (ADMIN, EMPLOYEE, USER)

**status**
- id, status (ORDERED, IN_PREPARATION, IN_DELIVERY, DELIVERED)

## 🔄 Development Workflow

### Making Changes

#### Backend Changes
1. Make code changes in `food-order-back/src`
2. Changes auto-reload with Spring DevTools
3. Refresh your browser

#### Frontend Changes
1. Make code changes in `food-ordering-front/src`
2. Changes auto-reload with React
3. Browser auto-refreshes

### Testing Changes

#### Backend
```bash
mvn test
```

#### Frontend
```bash
npm test
```

## 📦 Building for Production

### Frontend Build
```bash
cd food-ordering-app/food-ordering-front
npm run build
```

Output: `build/` folder with optimized files

### Backend Build
```bash
cd food-ordering-app/food-order-back
mvn clean package
```

Output: `target/food-order-back-0.0.1-SNAPSHOT.jar`

## 🚀 Deployment

### Quick Deployment Checklist
- [ ] Update database credentials
- [ ] Change default user passwords
- [ ] Set `spring.jpa.hibernate.ddl-auto=validate` (not update)
- [ ] Update API URLs in frontend config
- [ ] Set environment variables
- [ ] Enable HTTPS
- [ ] Configure firewall rules
- [ ] Setup backups

## 📞 Need Help?

- **Email:** nidhikumari934181@gmail.com
- **LinkedIn:** linkedin.com/in/nidhi-kumari-4648692b2
- **GitHub Issues:** Open an issue on GitHub

## 📚 Additional Resources

- [React Documentation](https://react.dev/)
- [Spring Boot Guide](https://spring.io/guides)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [Maven Tutorial](https://maven.apache.org/guides/)

---

**Congratulations! Your Food-Ordering-Delivery-Web-Application is now running! 🎉**

Start exploring the application and make your first order! 🍕
