# 🚀 Quick Start Guide

Get the Food-Ordering-Delivery-Web-Application running in 5 minutes!

## Prerequisites Check (2 mins)

Ensure you have installed:
- ✅ Node.js v14+ ([Download](https://nodejs.org/))
- ✅ Java 17 ([Download](https://www.oracle.com/java/technologies/downloads/))
- ✅ Maven 3.6+ ([Download](https://maven.apache.org/download.cgi))
- ✅ MySQL 8.0+ ([Download](https://www.mysql.com/downloads/))
- ✅ Git ([Download](https://git-scm.com/))

Verify installations:
```bash
node --version
java -version
mvn --version
mysql --version
git --version
```

---

## 5-Minute Quick Start

### Step 1: Clone & Navigate (30 seconds)

```bash
git clone https://github.com/nidhikumari30/Food-Ordering-Delivery-Web-Application.git
cd Food-Ordering-Delivery-Web-Application
```

### Step 2: Setup Database (1 minute)

```bash
# Open MySQL
mysql -u root -p

# Create database
CREATE DATABASE food_ordering_db;
exit
```

**Update database credentials:**
Open: `food-ordering-app/food-order-back/src/main/resources/application.properties`

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/food_ordering_db
spring.datasource.username=root
spring.datasource.password=YOUR_MYSQL_PASSWORD
```

### Step 3: Start Backend (1 minute)

Open Terminal 1:
```bash
cd food-ordering-app/food-order-back
mvn spring-boot:run
```

Wait for message: `Started FoodOrderBackApplication`

### Step 4: Start Frontend (1 minute)

Open Terminal 2:
```bash
cd food-ordering-app/food-ordering-front
npm install
npm start
```

Browser opens automatically to: `http://localhost:3000`

### Step 5: Test & Explore (30 seconds)

**Default Login Credentials:**
- **Admin:** admin / admin123
- **Employee:** employee / employee123
- **User:** testuser / user123

---

## Common Commands

### Backend Commands
```bash
# Navigate to backend
cd food-ordering-app/food-order-back

# Run application
mvn spring-boot:run

# Build JAR
mvn clean package

# Run tests
mvn test

# Clean build
mvn clean
```

### Frontend Commands
```bash
# Navigate to frontend
cd food-ordering-app/food-ordering-front

# Install dependencies
npm install

# Start development server
npm start

# Build for production
npm run build

# Run tests
npm test
```

### Database Commands
```bash
# Login to MySQL
mysql -u root -p

# Create database
CREATE DATABASE food_ordering_db;

# Show databases
SHOW DATABASES;

# Use database
USE food_ordering_db;

# Show tables
SHOW TABLES;

# Exit MySQL
exit
```

---

## Quick Links

| Resource | URL |
|----------|-----|
| **Application** | http://localhost:3000 |
| **API Base URL** | http://localhost:8080 |
| **Full README** | [README.md](README.md) |
| **Setup Guide** | [SETUP_GUIDE.md](SETUP_GUIDE.md) |
| **Architecture** | [ARCHITECTURE.md](ARCHITECTURE.md) |
| **Troubleshooting** | [TROUBLESHOOTING.md](TROUBLESHOOTING.md) |

---

## Useful Features to Try

### As Guest User
1. Select meal category
2. Browse available meals
3. Add items to cart
4. Place order with address & phone
5. Get tracking link

### As Logged-In User
1. Login with: `testuser` / `user123`
2. Edit profile
3. Browse meals
4. Place order (auto-fills address)
5. View active orders
6. View order history

### As Employee
1. Login with: `employee` / `employee123`
2. View incoming orders
3. Update order status
4. View order history

### As Admin
1. Login with: `admin` / `admin123`
2. Manage meals (Create, Edit, Delete)
3. Manage meal types
4. Manage users
5. Manage employees
6. View all orders

---

## Project Structure Overview

```
Food-Ordering-Delivery-Web-Application/
├── food-ordering-app/
│   ├── food-order-back/         # Spring Boot Backend (Java)
│   └── food-ordering-front/     # React Frontend (JavaScript)
├── README.md                    # Main documentation
├── SETUP_GUIDE.md              # Detailed setup
├── ARCHITECTURE.md              # Architecture details
└── TROUBLESHOOTING.md          # Common issues & fixes
```

---

## Development Tips

### Hot Reload
- **Frontend:** Changes auto-reload (React Dev Server)
- **Backend:** Changes auto-reload with DevTools

### Debugging
- **Frontend:** Press F12 for DevTools
- **Backend:** Check terminal output for logs

### API Testing
- Use Postman or Insomnia
- Or use browser Network tab (F12)

---

## Next Steps

After getting started:

1. **Read full documentation**
   - [README.md](README.md) - Complete overview

2. **Understand architecture**
   - [ARCHITECTURE.md](ARCHITECTURE.md) - System design

3. **Learn folder structure**
   - [FOLDER_STRUCTURE.md](FOLDER_STRUCTURE.md) - Code organization

4. **Setup development environment**
   - [SETUP_GUIDE.md](SETUP_GUIDE.md) - Detailed setup

5. **Troubleshoot issues**
   - [TROUBLESHOOTING.md](TROUBLESHOOTING.md) - Common issues

---

## Troubleshooting Quick Fixes

| Issue | Quick Fix |
|-------|-----------|
| Port 8080 in use | Change in application.properties to 8081 |
| Port 3000 in use | Set PORT=3001 before npm start |
| Can't connect MySQL | Verify username/password in application.properties |
| Blank page | Press F12, check Console for errors |
| Can't login | Try default: admin/admin123 |
| Database not found | Run: `CREATE DATABASE food_ordering_db;` |

---

## Environment Defaults

| Service | URL | Port | Credentials |
|---------|-----|------|-------------|
| Frontend | http://localhost:3000 | 3000 | N/A |
| Backend API | http://localhost:8080 | 8080 | N/A |
| MySQL | localhost | 3306 | root / (password) |
| Admin | N/A | N/A | admin / admin123 |
| Employee | N/A | N/A | employee / employee123 |
| User | N/A | N/A | testuser / user123 |

---

## Tips for Success

✅ **Do:**
- Create a MySQL database before starting
- Update credentials in application.properties
- Check both terminals for error messages
- Clear browser cache if having issues
- Read full README before reporting issues

❌ **Don't:**
- Use spaces in database names
- Change default port numbers unless necessary
- Skip MySQL setup
- Delete import.sql file
- Forget to update credentials

---

## Need Help?

| Issue | Solution |
|-------|----------|
| Stuck on setup | See [SETUP_GUIDE.md](SETUP_GUIDE.md) |
| Application error | Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md) |
| Understand architecture | Read [ARCHITECTURE.md](ARCHITECTURE.md) |
| Code organization | Check [FOLDER_STRUCTURE.md](FOLDER_STRUCTURE.md) |
| Contributing | See [CONTRIBUTING.md](CONTRIBUTING.md) |

---

## Contact Developer

👤 **Nidhi Kumari**
- 📧 Email: [nidhikumari934181@gmail.com](mailto:nidhikumari934181@gmail.com)
- 💼 LinkedIn: [linkedin.com/in/nidhi-kumari-4648692b2](https://linkedin.com/in/nidhi-kumari-4648692b2)
- 💻 GitHub: [github.com/nidhikumari30](https://github.com/nidhikumari30)

---

**Happy Coding! 🎉**

⭐ If this project helps you, please give it a star on GitHub!

---

**Last Updated:** January 2026
