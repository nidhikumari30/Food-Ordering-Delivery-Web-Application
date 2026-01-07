# 🆘 Troubleshooting Guide

Common issues and their solutions.

## Frontend Issues

### Issue: Cannot connect to backend API

**Error Message:**
```
GET http://localhost:8080/api/meals 500 (Internal Server Error)
Failed to fetch
```

**Solutions:**
1. Verify backend is running on port 8080
   ```bash
   netstat -ano | findstr :8080
   ```

2. Check CORS configuration in backend
   - Ensure `http://localhost:3000` is allowed

3. Clear browser cache
   - Press: Ctrl+Shift+Delete

4. Check network tab in browser DevTools
   - F12 → Network → Check requests

### Issue: Blank white page

**Solutions:**
1. Check console for errors
   - Press: F12 → Console

2. Verify React is compiled
   - Check build folder
   - Look for errors in terminal

3. Clear node_modules and reinstall
   ```bash
   rm -r node_modules
   npm install
   npm start
   ```

### Issue: Token expired / Login loop

**Solutions:**
1. Clear localStorage
   ```javascript
   localStorage.clear();
   ```

2. Check token expiration time
   - Default: 1 hour

3. Refresh browser and login again

### Issue: Images not loading

**Solutions:**
1. Verify image server path
2. Check CORS headers for image endpoint
3. Verify image format (PNG, JPG, GIF)
4. Check file size (max recommended: 5MB)

### Issue: Cart data lost on refresh

**Solutions:**
1. Verify Redux-Persist is configured
   - Check `store.js`

2. Check localStorage quotas
   - Storage might be full

3. Check browser's private mode
   - localStorage disabled in incognito

## Backend Issues

### Issue: Cannot start Spring Boot application

**Error Message:**
```
Exception in thread "main" org.springframework.beans.factory.BeanCreationException
```

**Solutions:**
1. Check Java version
   ```bash
   java -version
   ```
   Should be Java 17+

2. Check Maven configuration
   ```bash
   mvn -version
   ```

3. Clear Maven cache
   ```bash
   mvn clean
   rm -r ~/.m2/repository
   mvn install
   ```

4. Check `pom.xml` for syntax errors

### Issue: Cannot connect to MySQL database

**Error Message:**
```
java.sql.SQLException: Communications link failure
Could not create connection to database server
```

**Solutions:**
1. Verify MySQL service is running
   ```bash
   # Windows
   sc query mysql80
   
   # macOS
   brew services list
   
   # Linux
   systemctl status mysql
   ```

2. Check database credentials
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/food_ordering_db
   spring.datasource.username=root
   spring.datasource.password=your_password
   ```

3. Verify database exists
   ```sql
   SHOW DATABASES;
   ```

4. Check connection with MySQL CLI
   ```bash
   mysql -h localhost -u root -p
   ```

5. Verify port 3306 is accessible
   ```bash
   netstat -ano | findstr :3306
   ```

### Issue: Port 8080 already in use

**Solutions:**
1. Find process using port
   ```bash
   # Windows
   netstat -ano | findstr :8080
   taskkill /PID <PID> /F
   
   # macOS/Linux
   lsof -i :8080
   kill -9 <PID>
   ```

2. Change port in `application.properties`
   ```properties
   server.port=8081
   ```

### Issue: Database tables not created

**Error Message:**
```
java.sql.SQLException: Table 'food_ordering_db.users' doesn't exist
```

**Solutions:**
1. Verify `import.sql` exists in resources folder

2. Check Hibernate DDL setting
   ```properties
   spring.jpa.hibernate.ddl-auto=update
   ```

3. Manually run SQL script
   ```bash
   mysql -u root -p food_ordering_db < import.sql
   ```

4. Check database logs
   ```bash
   # Check MySQL error log
   ```

### Issue: JWT token validation fails

**Error Message:**
```
401 Unauthorized
JWT token is invalid or expired
```

**Solutions:**
1. Verify JWT secret in SecurityConfig
   ```java
   private static final String SECRET = "your_secret_key";
   ```

2. Check token expiration time
   ```java
   long expirationTimeInMillis = 3600000; // 1 hour
   ```

3. Verify token format
   ```
   Authorization: Bearer <token>
   ```

4. Check token in request header
   - Use browser DevTools

### Issue: CORS error in browser

**Error Message:**
```
Access to XMLHttpRequest blocked by CORS policy
```

**Solutions:**
1. Check CORS configuration
   ```java
   @Configuration
   public class CorsConfig implements WebMvcConfigurer {
       @Override
       public void addCorsMappings(CorsRegistry registry) {
           registry.addMapping("/api/**")
               .allowedOrigins("http://localhost:3000")
               .allowedMethods("GET", "POST", "PUT", "DELETE")
               .allowCredentials(true);
       }
   }
   ```

2. Verify frontend URL is in allowed origins

3. Check OPTIONS request preflight response

## Database Issues

### Issue: MySQL won't start

**Solutions:**
1. Check MySQL error log
   ```bash
   # Windows
   C:\ProgramData\MySQL\MySQL Server 8.0\Data\
   
   # macOS
   /var/log/mysql/
   ```

2. Check disk space
   ```bash
   df -h
   ```

3. Verify data folder permissions

4. Restart MySQL service
   ```bash
   # Windows
   net stop MySQL80
   net start MySQL80
   ```

### Issue: Data not persisting

**Solutions:**
1. Verify transactions are committed
   ```java
   @Transactional
   public void saveData() {
       // Data saving logic
   }
   ```

2. Check @Transactional annotations

3. Verify JPA cascade settings
   ```java
   @OneToMany(cascade = CascadeType.ALL)
   ```

### Issue: Slow database queries

**Solutions:**
1. Add database indexes
   ```sql
   CREATE INDEX idx_user_id ON final_orders(user_id);
   CREATE INDEX idx_meal_type_id ON meals(meal_type_id);
   ```

2. Use query profiling
   ```sql
   SET PROFILING = 1;
   SELECT * FROM users;
   SHOW PROFILES;
   ```

3. Check query execution plans
   ```sql
   EXPLAIN SELECT * FROM meals WHERE meal_type_id = 1;
   ```

## Network Issues

### Issue: Cannot reach localhost:3000

**Solutions:**
1. Check if React dev server is running
   ```bash
   netstat -ano | findstr :3000
   ```

2. Check firewall settings
   - Allow Node.js through firewall

3. Try different URL
   ```
   http://127.0.0.1:3000
   http://your_ip:3000
   ```

### Issue: Cannot reach localhost:8080

**Solutions:**
1. Check if Spring Boot is running
   ```bash
   netstat -ano | findstr :8080
   ```

2. Check terminal output for errors

3. Verify application started successfully
   - Look for "Started FoodOrderBackApplication" message

## Git Issues

### Issue: Large file size when pushing

**Solutions:**
1. Add `node_modules` and `target` to `.gitignore`
   ```
   node_modules/
   target/
   build/
   .env
   ```

2. Remove large files
   ```bash
   git rm --cached node_modules -r
   git commit -m "Remove node_modules"
   ```

3. Use Git LFS for images
   ```bash
   git lfs install
   git lfs track "*.jar"
   ```

## Performance Issues

### Frontend Slow

**Solutions:**
1. Check React DevTools Profiler
   - Identify slow components

2. Use lazy loading
   ```javascript
   const LazyComponent = lazy(() => import('./Component'));
   ```

3. Optimize renders
   - Use `React.memo()`
   - Use `useMemo()` and `useCallback()`

### Backend Slow

**Solutions:**
1. Check Spring Boot Actuator
   - `/actuator/metrics`

2. Enable SQL logging
   ```properties
   logging.level.org.hibernate.SQL=DEBUG
   ```

3. Check CPU and memory usage
   - Monitor with system tools

## Deployment Issues

### Issue: Application crashes in production

**Solutions:**
1. Check application logs
   ```bash
   tail -f /var/log/app.log
   ```

2. Monitor system resources
   ```bash
   top
   free -h
   ```

3. Check database connectivity
   - Verify connection string

4. Enable debug mode temporarily
   ```properties
   logging.level.root=DEBUG
   ```

## Getting Help

If you can't find a solution:

1. **Check Error Logs**
   - Browser console (F12)
   - Terminal output
   - Application logs

2. **Search Stack Overflow**
   - Format error message clearly

3. **Contact Developer**
   - Email: nidhikumari934181@gmail.com
   - LinkedIn: linkedin.com/in/nidhi-kumari-4648692b2

4. **Create GitHub Issue**
   - Include error logs
   - Include steps to reproduce
   - Include environment details

---

**Last Updated:** January 2026

For more help, visit [README.md](README.md) or [SETUP_GUIDE.md](SETUP_GUIDE.md).
